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

## 1.4 验证 API  







