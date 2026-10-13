---
tags:
  - 项目
类型: Agent
状态: 构思中
开始日期: 2026-10-12
截止日期:
关联知识:
关联资源:
---

# 1 README  


# 1 day 01  
## 1.1 确认 Git 推送成功  
配置 `.gitignore` 文件：  

```text
# Python  
.venv/  
__pycache__/  
*.pyc  
*.pyo  
.pytest_cache/  
  
# 环境变量  
.env  
  
# 数据库文件  
*.db  
*.sqlite3  
  
# Pycharm  
.idea/  
  
# 系统文件  
.DS_Store  
Thumb.db
```


``` bash
git add .
git commit -m "chore: 初始化项目结构"
git branch -M main
git remote add origin https://github.com/你的用户名/nl2sql-agent.git
git push -u origin main
```

常用的 Type 类型：  

|Type|含义|你的项目场景举例|
|---|---|---|
|**feat**|新增功能 (Feature)|`feat(agent): 添加 NL2SQL 核心解析逻辑`|
|**fix**|修复 Bug|`fix(api): 修复 FastAPI 路由参数校验失败的问题`|
|**docs**|文档变更|`docs: 更新 README 中的环境配置说明`|
|**style**|代码格式（不影响逻辑）|`style: 格式化 main.py 缩进`|
|**refactor**|重构（不是新增功能也不是修 Bug）|`refactor(db): 提取 SQLAlchemy 连接池配置`|
|**chore**|构建/工具/依赖变更|`chore: 更新 requirements.txt 依赖版本`|
|**test**|添加或修改测试|`test: 增加 NL2SQL 转换的单元测试`|

## 1.2 安装依赖  

``` bash
pip install openai pydantic sqlalchemy fastapi "uvicorn[standard]" python-dotenv
pip freeze > requirements.txt
```

```vtable
{"rows":[[{"t":"包","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1}],[{"t":"<code>openai</code>","rs":1,"cs":1},{"t":"OpenAI 官方 Python SDK，也可调用兼容 OpenAI 接口的模型服务","rs":1,"cs":1}],[{"t":"<code>pydantic</code>","rs":1,"cs":1},{"t":"数据校验、类型解析，FastAPI 的核心依赖之一","rs":1,"cs":1}],[{"t":"<code>sqlalchemy</code>","rs":1,"cs":1},{"t":"Python 主流 ORM / SQL 工具包，操作数据库","rs":1,"cs":1}],[{"t":"<code>fastapi</code>","rs":1,"cs":1},{"t":"高性能异步 Web 框架，适合做 API 后端","rs":1,"cs":1}],[{"t":"<code>uvicorn[standard]</code>","rs":1,"cs":1},{"t":"ASGI 服务器，<code>[standard]</code> 会额外安装 <code>uvloop</code>、<code>httptools</code>、<code>websockets</code>、<code>watchfiles</code> 等，提升性能并支持热重载","rs":1,"cs":1}],[{"t":"<code>python-dotenv</code>","rs":1,"cs":1},{"t":"从 <code>.env</code> 文件加载环境变量，避免把密钥写死在代码里","rs":1,"cs":1}]]}
```

``` bash
pip freeze > requirements.txt
```

- `pip freeze`：列出当前虚拟环境中**所有已安装的包及其精确版本号**（如 `fastapi==0.115.0`）。
- `>`：重定向符号，把输出写入文件而不是打印在屏幕上。
- `requirements.txt`：生成的依赖清单文件。

**这个文件的作用**：
当别人（或你部署到服务器）拿到你的代码时，只需执行：

``` bash
pip install -r requirements.txt
```

## 1.3 配置 API Key  
在根目录创建 `.env` 文件：  

```text
DEEPSEEK_API_KEY=你的真实key
```

再创建 `.env.example`：  

```text
DEEPSEEK_API_KEY=your_api_key_here
```

> `.env` 是自己用，`.env.example` 是他人用，将 `.env` 改为 `.env.example` ，填写 `api_key` 就可以使用。  

# 2 day 02  
## 2.1 写 init_db.py 创建数据库  

```python
import sqlite3

conn = sqlite3.connect("shop.db")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS products (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    category TEXT,
    price REAL,
    stock INTEGER
)
""")

cursor.execute("""
CREATE TABLE IF NOT EXISTS orders (
    id INTEGER PRIMARY KEY,
    product_id INTEGER,
    quantity INTEGER,
    order_date TEXT,
    FOREIGN KEY (product_id) REFERENCES products(id)
)
""")

cursor.executemany("INSERT OR IGNORE INTO products VALUES (?,?,?,?,?)", [
    (1, "iPhone 15", "电子产品", 5999.0, 100),
    (2, "MacBook Pro", "电子产品", 12999.0, 50),
    (3, "Python编程书", "图书", 89.0, 200),
    (4, "机械键盘", "配件", 399.0, 80),
])

cursor.executemany("INSERT OR IGNORE INTO orders VALUES (?,?,?,?)", [
    (1, 1, 2, "2025-01-15"),
    (2, 2, 1, "2025-01-20"),
    (3, 3, 5, "2025-02-01"),
    (4, 4, 3, "2025-02-10"),
])

conn.commit()
conn.close()
print("Database created: shop.db")
```

**外键是一张表的字段，指向另一张表的主键。它保证引用完整性——不能引用不存在的记录。在 NL 2 SQL 场景中，外键关系告诉模型两张表怎么关联，是生成 JOIN 语句的关键信息。**
### 2.1.1 占位符

```python
cursor.executemany("INSERT OR IGNORE INTO products VALUES (?,?,?,?,?)", [...])
```

**为什么用 `executemany` 而不是 `execute` **：`executemany` 一次插入多条记录，比循环调用 `execute` 更高效。  
**为什么用 `?` 占位符**：这是**参数化查询**。不要把值直接拼进 SQL 字符串，因为：  
1. **安全**：防止 SQL 注入。如果用户输入包含 `'; DROP TABLE products; --`，拼接字符串会把表删掉。
2. **省事**：不用手动处理引号和转义。

**面试考点**：什么是 SQL 注入？怎么防止？

> 标准答案：**SQL 注入是攻击者通过输入恶意 SQL 片段，改变原 SQL 的语义。防止方法是使用参数化查询（占位符 `?`），让数据库驱动处理值的转义，而不是字符串拼接。**

# 3 day 03  
## 3.1 一个最小的 NL 2 SQL 流程  

![Drawing 2026-10-13 13.21.07.excalidraw](../../../03%20附件/Excalidraw/项目/nl2sql_agent/Drawing%202026-10-13%2013.21.07.excalidraw.md)

# 4 day 04  
## 4.1 动手写最小 NL 2 SQL脚本  

```python
import os  
import sqlite3  
import json  
from dotenv import load_dotenv  
from openai import OpenAI  
from pydantic import BaseModel  
from openai.types.chat import ChatCompletionMessageParam  
  
load_dotenv()  
  
client = OpenAI(  
    api_key=os.environ.get("DEEPSEEK_API_KEY"),  
    base_url="https://api.deepseek.com",  
)  
  
DB_PATH = "shop.db"  
  
class SQLOutput(BaseModel):  
    sql: str  
    explanation: str  
  
def get_schema(db_path: str):  
    # 读取数据库所有表的结构，拼成文本  
    conn = sqlite3.connect(db_path)  
    cursor = conn.cursor()  
    cursor.execute("SELECT name FROM sqlite_master WHERE type='table'")  
    tables = [row[0] for row in cursor.fetchall()]  
    schema_parts = []  
    for table in tables:  
        cursor.execute(f"PRAGMA table_info({table})")  
        columns = cursor.fetchall()  
        cols = ",".join(f"{c[1]}{c[2]}" for c in columns)  
        schema_parts.append(f"表{table}: {cols}")  
    conn.close()  
    return "\n".join(schema_parts)  
  
def generate_sql(question: str, schema: str) -> SQLOutput:  
    # 调用模型，把问题翻译成 SQL
    prompt = f"""你是一个 SQL 专家。根据以下数据库结构，将用户的问题转换为 SQL 查询。  
    数据库表结构：    {schema}  
    用户问题：{question}  
    只输出 JSON，格式为：  
    {{"sql": "你的 SQL 语句"， "explanation": "简要说明"}}  
    """  
  
    messages: list[ChatCompletionMessageParam] = [  
        {"role": "user", "content": prompt}  
    ]  
  
    response = client.chat.completions.create(  
        model="deepseek-flash",  
        messages=messages,  
        response_format={"type": "json_object"}  
    )  
    raw = response.choices[0].message.content  
    return SQLOutput(**json.loads(raw))  
  
def execute_sql(sql: str, db_path: str):  
    conn = sqlite3.connect(db_path)  
    cursor = conn.cursor()  
    try:  
        cursor.execute(sql)  
        columns = [dosc[0] for dosc in cursor.description] if cursor.description else []  
        rows = cursor.fetchall()  
        return columns, rows  
    except Exception as e:  
        return [], [("SQL 执行错误", str(e))]  
    finally:  
        conn.close()  
  
if __name__ == "__main__":  
    schema = get_schema(DB_PATH)  
    question = input("请输入你的问题：")  
    result = generate_sql(question, schema)  
    print(f"\n生成的SQL: {result.sql}")  
    print(f"说明: {result.explanation}\n")  
  
    columns, rows = execute_sql(result.sql, DB_PATH)  
    print(f"列: {columns}")  
    for row in rows:  
        print(row)
```

