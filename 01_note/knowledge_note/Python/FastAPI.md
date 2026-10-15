---
tags:
  - knowledge
introduction: PythonWeb 基础
start_date: 2026-10-15
---

# 1 FastAPI入门

## 1-1 FastAPI 入门
### 1-1-1 FastAPI 简介
#### 1-1-1-1 什么是 FastAPI
FastAPI 是一个基于 Python 的高性能 Web 框架，用于快速构建 API（Application Programming Interface，应用程序接口）。  
它建立在 Starlette（ASGI 框架）和 Pydantic（数据验证库）之上，凭借原生异步支持与自动生成的交互式文档，成为当前 Python Web 开发中最热门的框架之一。  

> 注意：FastAPI 底层基于 Starlette（ASGI 规范），因此天然支持异步编程；基于 Pydantic，因此拥有强大的类型提示与数据校验能力。  

#### 1-1-1-2 原生异步支持

传统同步接口在遇到耗时操作（如 time.sleep）时会阻塞线程，一个请求必须等前一个请求处理完才能开始；而异步接口可以在等待期间切换去处理其他请求，从而大幅提升并发处理能力。  
下面以"处理 10 次耗时 1 秒的任务"为例，对比同步与异步的耗时差异。  

![同步与异步对比](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch1_sync_async.png)  

同步方式代码（串行执行）：  

```python
import time

def sync_task():
    for i in range(10):
        time.sleep(1)
        print(f"第 {i + 1} 次同步处理完成")
```

异步方式代码（并发执行）：  

```python
import asyncio

async def async_task(i):
    await asyncio.sleep(1)
    print(f"第 {i + 1} 次异步处理完成")

async def main():
    await asyncio.gather(*[async_task(i) for i in range(10)])
```

![同步流程](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch1_sync_flow.png)  

![异步流程](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch1_async_flow.png)  

两种方式的耗时对比：  

```vtable
{"rows": [[{"t": "对比项", "rs": 1, "cs": 1}, {"t": "同步方式", "rs": 1, "cs": 1}, {"t": "异步方式", "rs": 1, "cs": 1}], [{"t": "执行方式", "rs": 1, "cs": 1}, {"t": "串行执行，一个任务完成才执行下一个", "rs": 1, "cs": 1}, {"t": "交错执行，await 等待时让出控制权", "rs": 1, "cs": 1}], [{"t": "总耗时", "rs": 1, "cs": 1}, {"t": "10 个各耗时 1s 的任务共需约 10s", "rs": 1, "cs": 1}, {"t": "10 个任务同时等待，总耗时约 1s", "rs": 1, "cs": 1}], [{"t": "代码形式", "rs": 1, "cs": 1}, {"t": "普通 def + time.sleep", "rs": 1, "cs": 1}, {"t": "async def + await + asyncio.gather 并发调度", "rs": 1, "cs": 1}], [{"t": "适用场景", "rs": 1, "cs": 1}, {"t": "简单脚本、纯 CPU 计算", "rs": 1, "cs": 1}, {"t": "I/O 密集任务（网络请求、文件读写、数据库查询）", "rs": 1, "cs": 1}]]}
```

> 注意：只有耗时操作属于 I/O 密集（网络请求、文件读写、数据库查询等）时，异步才有明显优势；纯 CPU 计算依然会占用事件循环。  

#### 1-1-1-3 FastAPI 的三大优势

```vtable
{"rows": [[{"t": "优势", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "举例", "rs": 1, "cs": 1}], [{"t": "异步性能高", "rs": 1, "cs": 1}, {"t": "基于 ASGI 规范原生支持 async/await，高并发场景性能好", "rs": 1, "cs": 1}, {"t": "10 个 I/O 任务约 1s 完成，性能接近 Node.js 和 Go", "rs": 1, "cs": 1}], [{"t": "开发效率高", "rs": 1, "cs": 1}, {"t": "借助 Pydantic 类型提示与自动校验，减少手动编写校验代码", "rs": 1, "cs": 1}, {"t": "一个函数同时完成参数解析、数据校验与接口文档生成", "rs": 1, "cs": 1}], [{"t": "自动生成交互式文档", "rs": 1, "cs": 1}, {"t": "框架自动生成 /docs 在线接口文档，方便调试与前后端联调", "rs": 1, "cs": 1}, {"t": "浏览器访问 http://127.0.0.1:8000/docs 即可在线调试接口", "rs": 1, "cs": 1}]]}
```

### 1-1-2 第一个 FastAPI 程序

#### 1-1-2-1 创建项目

使用 PyCharm 创建 FastAPI 项目：New Project → 选择 FastAPI → 虚拟环境选择 Virtualenv → 点击 Create 创建。  
创建完成后，PyCharm 会自动安装 fastapi 与 uvicorn 等依赖。  

![创建项目](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch1_create_project.png)  

#### 1-1-2-2 运行项目

在终端中执行以下命令启动项目：  

```bash
uvicorn main:app --reload
```

其中 main 表示入口文件名（main.py），app 表示 FastAPI 实例名；--reload 表示代码变更后自动重启服务，开发阶段非常方便。  

#### 1-1-2-3 访问项目

服务启动后，浏览器访问：  

```text
http://127.0.0.1:8000
```

即可看到默认路由返回的内容；访问 http://127.0.0.1:8000/docs 可以打开 FastAPI 自动生成的交互式 API 文档，在页面上直接测试各个接口。  

![访问项目](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch1_access_project.png)  

#### 1-1-2-4 虚拟环境的作用

虚拟环境用于隔离不同项目之间的依赖，避免包版本冲突。  
例如项目 A 需要 fastapi 0.100，项目 B 需要 fastapi 0.115，如果安装在同一环境会互相覆盖；使用虚拟环境后各项目依赖相互独立，互不影响。  

### 1-1-3 路由

#### 1-1-3-1 什么是路由

路由是 URL 地址和处理函数之间的映射关系：当客户端访问某个 URL 时，框架根据路由找到对应的处理函数并执行。  

#### 1-1-3-2 路由的定义

路由通过装饰器定义，示例：  

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "hello world"}
```

一段路由由四部分组成：  

```vtable
{"rows": [[{"t": "组成", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "装饰器", "rs": 1, "cs": 1}, {"t": "@app.get(“/”)", "rs": 1, "cs": 1}, {"t": "指定请求方法与路径，是路由的核心", "rs": 1, "cs": 1}], [{"t": "FastAPI 实例", "rs": 1, "cs": 1}, {"t": "app", "rs": 1, "cs": 1}, {"t": "注册路由的应用对象，全局唯一", "rs": 1, "cs": 1}], [{"t": "请求方法", "rs": 1, "cs": 1}, {"t": "get", "rs": 1, "cs": 1}, {"t": "GET、POST、PUT、DELETE 等 HTTP 方法", "rs": 1, "cs": 1}], [{"t": "请求路径", "rs": 1, "cs": 1}, {"t": "/", "rs": 1, "cs": 1}, {"t": "客户端访问的 URL 路径，支持路径参数如 /book/{id}", "rs": 1, "cs": 1}], [{"t": "响应结果", "rs": 1, "cs": 1}, {"t": "return {“key”: “value”}", "rs": 1, "cs": 1}, {"t": "处理函数返回的数据，FastAPI 自动转 JSON", "rs": 1, "cs": 1}]]}
```

#### 1-1-3-3 路由练习

需求：访问路径 /user/hello，响应结果为 {"msg": "我正在学习 FastAPI ......"}。  
参考实现：  

```python
@app.get("/user/hello")
async def user_hello():
    return {"msg": "我正在学习 FastAPI ......"}
```

### 1-1-4 参数

#### 1-1-4-1 参数的作用

参数就是客户端发送请求时附带的额外信息和指令。  
参数的作用是让同一个接口能根据不同的输入，返回不同的输出，实现动态交互。例如访问 /book 时传入 book_id=1 返回图书 1 的信息，传入 book_id=2 返回图书 2 的信息。  

#### 1-1-4-2 参数分类

HTTP 请求中的参数按位置与用途分为三类：路径参数、查询参数、请求体。  

![参数分类](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch1_param_types.png)  

```vtable
{"rows": [[{"t": "类型", "rs": 1, "cs": 1}, {"t": "位置", "rs": 1, "cs": 1}, {"t": "作用", "rs": 1, "cs": 1}, {"t": "方法", "rs": 1, "cs": 1}, {"t": "语法示例", "rs": 1, "cs": 1}], [{"t": "路径参数", "rs": 1, "cs": 1}, {"t": "URL 路径的一部分，如 /book/{id}", "rs": 1, "cs": 1}, {"t": "指向唯一的、特定的资源", "rs": 1, "cs": 1}, {"t": "GET", "rs": 1, "cs": 1}, {"t": "@app.get(“/book/{id}”)，访问 /book/1", "rs": 1, "cs": 1}], [{"t": "查询参数", "rs": 1, "cs": 1}, {"t": "URL? 之后，如 k1=v1&k2=v2", "rs": 1, "cs": 1}, {"t": "对资源集合进行过滤、排序、分页等操作", "rs": 1, "cs": 1}, {"t": "GET", "rs": 1, "cs": 1}, {"t": "/book?page=1&pageSize=10", "rs": 1, "cs": 1}], [{"t": "请求体", "rs": 1, "cs": 1}, {"t": "HTTP 请求的消息体（body）中", "rs": 1, "cs": 1}, {"t": "创建、更新资源，携带大量数据如 JSON", "rs": 1, "cs": 1}, {"t": "POST、PUT 等", "rs": 1, "cs": 1}, {"t": "请求体 {“title”: “标题”, “content”: “正文”}", "rs": 1, "cs": 1}]]}
```

#### 1-1-4-3 路径参数

路径参数是 URL 路径的一部分，用于指向唯一、特定的资源，例如 /book/{id} 中的 id。  
在函数中声明同名参数并加类型注解即可：  

```python
@app.get("/book/{id}")
async def get_book(id: int):
    return {"id": id, "title": f"这是第{id}本书"}
```

访问 http://127.0.0.1:8000/book/666 时，返回 {"id": 666, "title": "这是第666本书"}。  

练习：以用户 id 为路径参数设计 URL，响应结果包含用户 id 和名称（普通用户 id）。  
参考实现：  

```python
@app.get("/user/{id}")
async def get_user(id: int):
    return {"id": id, "name": f"普通用户{id}"}
```

路径参数的类型注解有两种方式：Python 原生注解和 Path 注解。  

```python
# Python 原生注解
@app.get("/book/{id}")
async def get_book(id: int):
    return {"id": id, "title": f"这是第{id}本书"}

# Path 注解（可附加校验）
@app.get("/book/{id}")
async def get_book(id: int = Path()):
    return {"id": id, "title": f"这是第{id}本书"}
```

Path 常用参数：  

```vtable
{"rows": [[{"t": "参数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}], [{"t": "...", "rs": 1, "cs": 1}, {"t": "必填", "rs": 1, "cs": 1}, {"t": "Path(...)", "rs": 1, "cs": 1}], [{"t": "gt / ge", "rs": 1, "cs": 1}, {"t": "大于 / 大于等于", "rs": 1, "cs": 1}, {"t": "Path(gt=1)", "rs": 1, "cs": 1}], [{"t": "lt / le", "rs": 1, "cs": 1}, {"t": "小于 / 小于等于", "rs": 1, "cs": 1}, {"t": "Path(le=100)", "rs": 1, "cs": 1}], [{"t": "description", "rs": 1, "cs": 1}, {"t": "描述信息，显示在接口文档中", "rs": 1, "cs": 1}, {"t": "Path(description=“书籍ID”)", "rs": 1, "cs": 1}], [{"t": "min_length / max_length", "rs": 1, "cs": 1}, {"t": "长度限制", "rs": 1, "cs": 1}, {"t": "Path(min_length=1, max_length=20)", "rs": 1, "cs": 1}]]}
```

练习：定义两个携带路径参数的接口并使用 Path 实现类型注解——接口 1 以新闻分类 id 为参数，id 范围为 1~100；接口 2 以新闻分类名称为参数，名称长度为 2~10。  
参考实现：  

```python
from fastapi import Path

@app.get("/news/category/{category_id}")
async def get_category(category_id: int = Path(..., ge=1, le=100, description="新闻分类ID")):
    return {"category_id": category_id}

@app.get("/news/category_name/{category_name}")
async def get_category_name(category_name: str = Path(..., min_length=2, max_length=10, description="新闻分类名称")):
    return {"category_name": category_name}
```

> 注意：ge/le 是"大于等于/小于等于"，不要误写成 gte/lte。  

#### 1-1-4-4 查询参数

当声明的参数不是路径参数时，路径操作函数会把该参数自动解释为查询参数。  
查询参数位于 URL? 之后，格式为 k1=v1&k2=v2，常用于对资源集合进行过滤、排序、分页等操作。  

```python
@app.get("/news/news_list")
async def get_news_list(skip: int, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

访问 http://127.0.0.1:8000/news/news_list?skip=0&limit=10 时，返回 {"skip": 0, "limit": 10}。  

查询参数的类型注解同样有两种：Python 原生注解和 Query 注解。  

```python
from fastapi import Query

@app.get("/user")
async def get_user(user_id: int = Query()):
    return {"id": user_id, "title": f"这是第{user_id}本书"}
```

Query 常用参数与 Path 一致：  

```vtable
{"rows": [[{"t": "参数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}], [{"t": "...", "rs": 1, "cs": 1}, {"t": "必填", "rs": 1, "cs": 1}, {"t": "Query(...)", "rs": 1, "cs": 1}], [{"t": "gt / ge", "rs": 1, "cs": 1}, {"t": "大于 / 大于等于", "rs": 1, "cs": 1}, {"t": "Query(ge=1)", "rs": 1, "cs": 1}], [{"t": "lt / le", "rs": 1, "cs": 1}, {"t": "小于 / 小于等于", "rs": 1, "cs": 1}, {"t": "Query(le=100)", "rs": 1, "cs": 1}], [{"t": "description", "rs": 1, "cs": 1}, {"t": "描述信息，显示在接口文档中", "rs": 1, "cs": 1}, {"t": "Query(description=“页码”)", "rs": 1, "cs": 1}], [{"t": "min_length / max_length", "rs": 1, "cs": 1}, {"t": "长度限制", "rs": 1, "cs": 1}, {"t": "Query(min_length=2, max_length=20)", "rs": 1, "cs": 1}]]}
```

练习：设计接口查询图书，携带两个查询参数——图书分类（默认值为 Python 开发，长度限制 5~255）和价格（限制大小范围 50~100）。  
参考实现：  

```python
@app.get("/books")
async def get_books(
    category: str = Query("Python开发", min_length=5, max_length=255, description="图书分类"),
    price: float = Query(..., ge=50, le=100, description="图书价格")
):
    return {"category": category, "price": price}
```

#### 1-1-4-5 请求体参数

请求体位于 HTTP 请求的消息体（body）中，用于创建、更新资源，可携带大量数据（如 JSON）。  
在 HTTP 协议中，一个完整的请求由三部分组成：  

```vtable
{"rows": [[{"t": "组成", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}], [{"t": "请求行", "rs": 1, "cs": 1}, {"t": "包含方法、URL、协议版本", "rs": 1, "cs": 1}, {"t": "GET /user/info HTTP/1.1", "rs": 1, "cs": 1}], [{"t": "请求头", "rs": 1, "cs": 1}, {"t": "元数据信息（Content-Type、Authorization 等）", "rs": 1, "cs": 1}, {"t": "Content-Type: application/json", "rs": 1, "cs": 1}], [{"t": "请求体", "rs": 1, "cs": 1}, {"t": "实际要发送的数据内容", "rs": 1, "cs": 1}, {"t": "{“username”: “daqiu”, “password”: “123456”}", "rs": 1, "cs": 1}]]}
```

使用请求体参数分两步：先用 Pydantic 的 BaseModel 定义类型，再在接口函数中做类型注解。  

```python
from pydantic import BaseModel

# 1. 定义类型
class User(BaseModel):
    username: str
    password: str

# 2. 类型注解
@app.post("/register")
async def register(user: User):
    return user
```

对应的 curl 请求示例：  

```bash
curl -X 'POST' \
  'http://127.0.0.1:8000/register' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "username": "daqiu",
  "password": "123456"
}'
```

请求体字段的类型注解同样有两种：Python 原生注解和 Field 注解。  

```python
from pydantic import BaseModel, Field

class User(BaseModel):
    username: str = Field(...)
    password: str = Field(...)
```

Field 常用参数：  

```vtable
{"rows": [[{"t": "参数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}], [{"t": "...", "rs": 1, "cs": 1}, {"t": "必填", "rs": 1, "cs": 1}, {"t": "Field(...)", "rs": 1, "cs": 1}], [{"t": "gt / ge", "rs": 1, "cs": 1}, {"t": "大于 / 大于等于", "rs": 1, "cs": 1}, {"t": "Field(gt=0)", "rs": 1, "cs": 1}], [{"t": "lt / le", "rs": 1, "cs": 1}, {"t": "小于 / 小于等于", "rs": 1, "cs": 1}, {"t": "Field(le=120)", "rs": 1, "cs": 1}], [{"t": "default", "rs": 1, "cs": 1}, {"t": "默认值", "rs": 1, "cs": 1}, {"t": "Field(default=0)", "rs": 1, "cs": 1}], [{"t": "description", "rs": 1, "cs": 1}, {"t": "描述信息，显示在接口文档中", "rs": 1, "cs": 1}, {"t": "Field(description=“年龄”)", "rs": 1, "cs": 1}], [{"t": "min_length / max_length", "rs": 1, "cs": 1}, {"t": "长度限制", "rs": 1, "cs": 1}, {"t": "Field(min_length=2, max_length=20)", "rs": 1, "cs": 1}]]}
```

练习：设计接口新增图书，图书信息包含书名、作者、出版社、售价，具体要求为：书名不能为空、长度 2~20；作者长度 2~10；出版社默认值"黑马出版社"；售价不能为空、价格大于 0 元。  
参考实现：  

```python
from pydantic import BaseModel, Field

class Book(BaseModel):
    title: str = Field(..., min_length=2, max_length=20, description="书名")
    author: str = Field(..., min_length=2, max_length=10, description="作者")
    press: str = Field("黑马出版社", description="出版社")
    price: float = Field(..., gt=0, description="售价")

@app.post("/books")
async def add_book(book: Book):
    return book
```

### 1-1-5 请求与响应

#### 1-1-5-1 请求与响应模型

Web 开发中，客户端（浏览器、App 等）向服务器发送 Request（请求），服务器处理后返回 Response（响应），一次完整的交互即"请求-响应"模型。  
FastAPI 默认会自动将路径操作函数返回的 Python 对象（字典、列表、Pydantic 模型等），经由 jsonable_encoder 转换为 JSON 兼容格式，并包装为 JSONResponse 返回，省去了手动序列化的步骤。  

#### 1-1-5-2 FastAPI 内置响应类型

如果需要返回非 JSON 数据（如 HTML、文件流），FastAPI 提供了丰富的响应类型：  

```vtable
{"rows": [[{"t": "响应类型", "rs": 1, "cs": 1}, {"t": "用途", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}, {"t": "导入", "rs": 1, "cs": 1}], [{"t": "JSONResponse", "rs": 1, "cs": 1}, {"t": "默认响应，返回 JSON 数据", "rs": 1, "cs": 1}, {"t": "return {“key”: “value”}", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import JSONResponse", "rs": 1, "cs": 1}], [{"t": "HTMLResponse", "rs": 1, "cs": 1}, {"t": "返回 HTML 内容", "rs": 1, "cs": 1}, {"t": "return HTMLResponse(html_content)", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import HTMLResponse", "rs": 1, "cs": 1}], [{"t": "PlainTextResponse", "rs": 1, "cs": 1}, {"t": "返回纯文本", "rs": 1, "cs": 1}, {"t": "return PlainTextResponse(“text”)", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import PlainTextResponse", "rs": 1, "cs": 1}], [{"t": "FileResponse", "rs": 1, "cs": 1}, {"t": "返回文件下载", "rs": 1, "cs": 1}, {"t": "return FileResponse(path)", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import FileResponse", "rs": 1, "cs": 1}], [{"t": "StreamingResponse", "rs": 1, "cs": 1}, {"t": "流式响应，边生成边返回", "rs": 1, "cs": 1}, {"t": "生成器函数逐段返回数据", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import StreamingResponse", "rs": 1, "cs": 1}], [{"t": "RedirectResponse", "rs": 1, "cs": 1}, {"t": "重定向", "rs": 1, "cs": 1}, {"t": "return RedirectResponse(url)", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import RedirectResponse", "rs": 1, "cs": 1}]]}
```

#### 1-1-5-3 响应类型设置方式

设置响应类型有两种方式。  

方式一：装饰器中指定响应类，适用于固定返回类型（HTML、纯文本等）。  

```python
from fastapi.responses import HTMLResponse

@app.get("/html", response_class=HTMLResponse)
async def get_html():
    return "<h1>Hello World</h1>"
```

访问 http://127.0.0.1:8000/html 即可在浏览器中看到渲染后的标题页面。  

方式二：返回响应对象，适用于文件下载、图片、流式响应等场景。  

```python
from fastapi.responses import FileResponse

@app.get("/file")
async def get_file():
    file_path = "./files/1.jpeg"
    return FileResponse(file_path)
```

FileResponse 是 FastAPI 专门用于高效返回文件内容（图片、PDF、Excel、音视频等）的响应类，能智能处理文件路径、媒体类型推断、范围请求和缓存头部，是服务静态文件的推荐方式。  

#### 1-1-5-4 自定义响应数据格式

除了直接返回字典，还可以使用 response_model 参数严格定义接口的输出格式。  
response_model 是路径操作装饰器（如 @app.get、@app.post）的关键参数，它通过一个 Pydantic 模型严格定义和约束 API 端点的输出格式，在提供自动数据验证和序列化的同时，也是保障数据安全性的第一道防线（例如避免把内部敏感字段返回给前端）。  

```python
from pydantic import BaseModel

class News(BaseModel):
    id: int
    title: str
    content: str

@app.get("/news/{id}", response_model=News)
async def get_news(id: int):
    return {
        "id": id,
        "title": f"这是第{id}本书",
        "content": "这是一本好书"
    }
```

> 注意：定义响应模型时只声明要返回给前端的字段，内部敏感字段（如密码哈希值）不要写进响应模型。  

#### 1-1-5-5 异常处理

对于客户端引发的错误（4xx，如资源未找到、认证失败），应使用 fastapi.HTTPException 中断正常处理流程，并返回标准错误响应。  

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

@app.get('/news/{id}')
async def get_news(id: int):
    id_list = [1, 2, 3, 4, 5, 6]
    if id not in id_list:
        raise HTTPException(status_code=404, detail="当前id不存在")
    return {"id": id}
```

访问 /news/100 时，接口返回 404 状态码，响应体为 {"detail": "当前id不存在"}。


# 2 FastAPI进阶

## 2-2 FastAPI 进阶

### 2-2-1 中间件

#### 2-2-1-1 使用中间件的场景

后端开发中经常遇到这样的需求：多个接口都需要验证用户身份，多个接口都需要记录日志、性能数据。  
如果每个接口都重复编写这些逻辑，代码会非常冗余，这时就可以使用中间件为每个请求前后添加统一的处理逻辑。  

中间件可统一处理的常见功能：日志记录、身份认证、跨域处理、响应头处理、性能监控。  

#### 2-2-1-2 什么是中间件

中间件（Middleware）是一个在每次请求进入 FastAPI 应用时都会被执行的函数。  
它在请求到达实际的路径操作（路由处理函数）之前运行，并且在响应返回给客户端之前再运行一次。  

![中间件执行流程](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch2_middleware_flow.png)  

请求进入后依次经过中间件 A、中间件 B，最终到达路由处理函数；响应则按相反路径逐级返回客户端，执行顺序为自下而上。  

#### 2-2-1-3 定义中间件

在函数顶部使用装饰器 @app.middleware("http") 即可定义一个中间件：  

```python
@app.middleware("http")
async def middleware(request, call_next):
    print('中间件开始处理 -- start')
    response = await call_next(request)
    print('中间件处理完成 -- end')
    return response
```

其中 call_next 接收 request 并返回 response：await call_next(request) 表示把请求传递给路径处理函数，拿到响应后再执行中间件后续逻辑（如统一加响应头、记录耗时等）。  

#### 2-2-1-4 多个中间件的执行顺序

多个中间件同时存在时，执行顺序是自下而上：请求从下往上穿过各中间件到达路由处理函数，响应再从上往下返回。  
即先注册的中间件后执行请求阶段逻辑，但先执行响应阶段逻辑。  

小结：  

```vtable
{"rows":[[{"t":"问题","rs":1,"cs":1},{"t":"答案","rs":1,"cs":1}],[{"t":"中间件作用是什么？","rs":1,"cs":1},{"t":"为每个请求添加统一的处理逻辑（日志、认证、跨域、响应头、性能监控等）","rs":1,"cs":1}],[{"t":"中间件怎么定义？","rs":1,"cs":1},{"t":"函数顶部使用装饰器 @app.middleware(“http”)，函数内 yield 之后写响应后处理逻辑","rs":1,"cs":1}],[{"t":"多个中间件的执行顺序？","rs":1,"cs":1},{"t":"请求阶段自下而上执行，响应阶段自上而下返回","rs":1,"cs":1}],[{"t":"典型应用有哪些？","rs":1,"cs":1},{"t":"请求日志记录、统一认证、跨域处理、自定义响应头、接口耗时统计","rs":1,"cs":1}]]}
```

### 2-2-2 依赖注入

#### 2-2-2-1 为什么需要依赖注入

看下面三个接口，它们的分页参数定义和分页逻辑几乎完全一样，代码重复严重：  

```python
@app.get('/news/news_list')
async def get_news_list(
    skip: int = Query(0, ge=0),
    limit: int = Query(10, le=60)
):
    # 分页逻辑...
    return {"list": "新闻列表"}

@app.get("/users/user_list")
async def get_user_list(
    skip: int = Query(0, ge=0),
    limit: int = Query(10, le=60)
):
    # 分页逻辑...
    return {"users": "用户列表"}

@app.get("/news/category")
async def get_category(
    skip: int = Query(0, ge=0),
    limit: int = Query(10, le=60)
):
    # 分页逻辑...
    return {"category": "新闻分类"}
```

使用依赖注入系统可以共享通用逻辑，减少代码重复。  

#### 2-2-2-2 依赖注入的概念与优点

依赖项：可重用的组件（函数/类），负责提供某种功能或数据。  
注入：FastAPI 自动帮你调用依赖项，并将结果"注入"到路径操作函数中。  

依赖注入的优点：  

```vtable
{"rows": [[{"t": "优点", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}], [{"t": "代码复用", "rs": 1, "cs": 1}, {"t": "一次编写，多处使用", "rs": 1, "cs": 1}, {"t": "get_db 会话依赖在多个路由中重复注入", "rs": 1, "cs": 1}], [{"t": "解耦", "rs": 1, "cs": 1}, {"t": "业务逻辑与基础设施代码分离", "rs": 1, "cs": 1}, {"t": "路由不关心数据库会话如何创建与关闭", "rs": 1, "cs": 1}], [{"t": "易于测试", "rs": 1, "cs": 1}, {"t": "轻松地用模拟依赖替换真实依赖进行测试", "rs": 1, "cs": 1}, {"t": "测试时把数据库依赖替换为内存数据库", "rs": 1, "cs": 1}], [{"t": "可组合", "rs": 1, "cs": 1}, {"t": "小依赖可以互相嵌套，按需组装", "rs": 1, "cs": 1}, {"t": "get_current_user 内部再依赖 get_db", "rs": 1, "cs": 1}]]}
```

#### 2-2-2-3 依赖注入的应用场景

![依赖注入应用场景](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch2_di_scene.png)  

```vtable
{"rows": [[{"t": "场景", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}], [{"t": "处理请求参数", "rs": 1, "cs": 1}, {"t": "从请求中提取和验证参数（路径参数、查询参数、请求体）", "rs": 1, "cs": 1}, {"t": "参数对象直接作为函数入参注入", "rs": 1, "cs": 1}], [{"t": "共享业务逻辑", "rs": 1, "cs": 1}, {"t": "抽取封装多个路由公用的逻辑代码", "rs": 1, "cs": 1}, {"t": "通用分页参数依赖 Query(1, ge=1)", "rs": 1, "cs": 1}], [{"t": "共享数据库连接", "rs": 1, "cs": 1}, {"t": "管理数据库会话的创建、使用、关闭", "rs": 1, "cs": 1}, {"t": "async with AsyncSessionLocal() 会话上下文", "rs": 1, "cs": 1}], [{"t": "安全和认证", "rs": 1, "cs": 1}, {"t": "验证用户身份、检查权限和角色要求等", "rs": 1, "cs": 1}, {"t": "get_current_user 依赖统一校验 Token", "rs": 1, "cs": 1}]]}
```

#### 2-2-2-4 使用依赖注入三步

使用依赖注入分三步：创建依赖项 → 导入 Depends → 声明依赖项。  

```python
from fastapi import Depends

# 1. 创建依赖项
async def common_parameters(
    skip: int = Query(0, ge=0),
    limit: int = Query(10, le=60)
):
    return {"skip": skip, "limit": limit}

# 3. 声明依赖项
@app.get("/news/news_list")
async def get_news_list(
    commons = Depends(common_parameters)
):
    return commons
```

FastAPI 会自动调用 common_parameters，并把返回的字典注入到 commons 参数中，三个接口只需各自声明一行 Depends 即可复用同一套分页逻辑。  

#### 2-2-2-5 中间件与依赖注入的区别

中间件控制谁？Everyone——每个请求都会经过中间件。  
依赖注入控制谁？我说了算——只有声明了 Depends 的接口才会执行对应依赖，由开发者按需控制。  

### 2-2-3 ORM（SQLAlchemy）

#### 2-2-3-1 ORM 简介

ORM（Object-Relational Mapping，对象关系映射）是一种编程技术，用于在面向对象编程语言和关系型数据库之间建立映射。  
它允许开发者通过操作对象的方式与数据库进行交互，而无需直接编写复杂的 SQL 语句。  

ORM 的优势：  

```vtable
{"rows": [[{"t": "优势", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "减少重复的 SQL 代码", "rs": 1, "cs": 1}, {"t": "通过模型对象操作数据库，无需手写 SQL 语句", "rs": 1, "cs": 1}], [{"t": "代码更简洁易读", "rs": 1, "cs": 1}, {"t": "表结构即模型类，语义清晰", "rs": 1, "cs": 1}], [{"t": "自动处理数据库连接和事务", "rs": 1, "cs": 1}, {"t": "会话管理与事务由框架接管", "rs": 1, "cs": 1}], [{"t": "自动防止 SQL 注入攻击", "rs": 1, "cs": 1}, {"t": "参数化查询天然免疫拼接注入", "rs": 1, "cs": 1}], [{"t": "跨数据库兼容", "rs": 1, "cs": 1}, {"t": "切换 MySQL、PostgreSQL、SQLite 只需修改连接字符串", "rs": 1, "cs": 1}]]}
```

#### 2-2-3-2 ORM 分类

主流 Python ORM 工具对比：  

```vtable
{"rows": [[{"t": "排名", "rs": 1, "cs": 1}, {"t": "ORM 工具", "rs": 1, "cs": 1}, {"t": "特点", "rs": 1, "cs": 1}, {"t": "适应场景", "rs": 1, "cs": 1}], [{"t": "1", "rs": 1, "cs": 1}, {"t": "SQLAlchemy ORM", "rs": 1, "cs": 1}, {"t": "功能最强、最灵活、企业级", "rs": 1, "cs": 1}, {"t": "各类 API、微服务、数据应用", "rs": 1, "cs": 1}], [{"t": "2", "rs": 1, "cs": 1}, {"t": "Django ORM", "rs": 1, "cs": 1}, {"t": "封装好、上手快、自带 Admin", "rs": 1, "cs": 1}, {"t": "Django 项目、管理后台", "rs": 1, "cs": 1}], [{"t": "3", "rs": 1, "cs": 1}, {"t": "Tortoise ORM", "rs": 1, "cs": 1}, {"t": "全异步", "rs": 1, "cs": 1}, {"t": "异步 Web 服务、高并发 API", "rs": 1, "cs": 1}], [{"t": "4", "rs": 1, "cs": 1}, {"t": "SQLModel", "rs": 1, "cs": 1}, {"t": "FastAPI 作者出品，Pydantic 与 SQLAlchemy 结合", "rs": 1, "cs": 1}, {"t": "FastAPI 快速开发数据层", "rs": 1, "cs": 1}], [{"t": "5", "rs": 1, "cs": 1}, {"t": "Peewee", "rs": 1, "cs": 1}, {"t": "轻量、简单易用", "rs": 1, "cs": 1}, {"t": "小型项目与脚本工具", "rs": 1, "cs": 1}]]}
```

> 注意：SQLAlchemy 是企业应用最多、社区最活跃的 ORM，本课程全程使用 SQLAlchemy 异步版。  

#### 2-2-3-3 ORM 使用流程

![ORM 使用流程](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch2_orm_flow.png)  

ORM 使用分三步：安装 → 建库、建表 → 操作数据（查询、新增、修改、删除）。  

第一步：安装依赖。  

```bash
pip install "sqlalchemy[asyncio]" aiomysql
```

其中 sqlalchemy[asyncio] 是异步 ORM，aiomysql 是 MySQL 的异步数据库驱动。  

#### 2-2-3-4 建库建表

先手动创建数据库：  

```sql
create database fastapi_test;
```

ORM 建表流程：创建数据库引擎 → 定义模型类 → 启动应用时建表。  

创建异步引擎：  

```python
from sqlalchemy.ext.asyncio import create_async_engine

ASYNC_DATABASE_URL = "mysql+aiomysql://root:123456@localhost:3306/fastapi_test?charset=utf8"

# 创建异步引擎
async_engine = create_async_engine(
    ASYNC_DATABASE_URL,
    echo=True,        # 可选：输出 SQL 日志
    pool_size=10,     # 设置连接池中保持的持久连接数
    max_overflow=20   # 设置连接池允许创建的额外连接数
)
```

定义模型类分两步：先定义基类（继承 DeclarativeBase，包含通用属性和字段的映射），再定义数据库表对应的模型类。  

```python
from sqlalchemy import String, DateTime, func
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column
from datetime import datetime

# 1. 基类，继承 DeclarativeBase
class Base(DeclarativeBase):
    create_time: Mapped[datetime] = mapped_column(
        DateTime, insert_default=func.now(), default=datetime.now, comment="创建时间")
    update_time: Mapped[datetime] = mapped_column(
        DateTime, insert_default=func.now(), onupdate=func.now(), default=datetime.now, comment="修改时间")

# 2. 定义数据库表对应的模型类
class Book(Base):
    __tablename__ = "book"

    id: Mapped[int] = mapped_column(primary_key=True)
    bookname: Mapped[str] = mapped_column(String(255))
    author: Mapped[str] = mapped_column(String(255))
```

启动应用时建表：  

```python
@app.on_event("startup")
async def create_tables():
    async with async_engine.begin() as conn:
        await conn.run_sync(Base.metadata.create_all)
```

练习：定义用户表模型（id 主键、用户名、密码、创建时间、更新时间）。  
参考实现：  

```python
class User(Base):
    __tablename__ = "user"

    id: Mapped[int] = mapped_column(primary_key=True)
    username: Mapped[str] = mapped_column(String(50), comment="用户名")
    password: Mapped[str] = mapped_column(String(100), comment="密码")
```

其中创建时间 create_time、更新时间 update_time 由基类 Base 统一提供，无需重复定义。  

#### 2-2-3-5 路由中使用 ORM

在路由中使用 ORM 需要三件套：异步引擎、会话工厂、会话依赖。  

创建会话工厂：  

```python
from sqlalchemy.ext.asyncio import AsyncSession, async_sessionmaker

AsyncSessionLocal = async_sessionmaker(
    bind=async_engine,
    class_=AsyncSession,
    expire_on_commit=False
)
```

expire_on_commit=False 表示提交后不立即过期对象属性，提交后仍能安全访问模型属性。  

定义会话依赖：  

```python
async def get_database():
    async with AsyncSessionLocal() as session:
        try:
            yield session
            await session.commit()
        except Exception:
            await session.rollback()
            raise
        finally:
            await session.close()
```

路由中通过 Depends 声明会话：  

```python
from fastapi import Depends

@app.get("/books")
async def get_books(db: AsyncSession = Depends(get_database)):
    # 使用 db 执行查询
    ...
```

> 注意：依赖项中的 yield 前后逻辑分别在请求前和请求后执行——yield 之前准备资源，yield 之后做提交/回滚/关闭等收尾工作。  

#### 2-2-3-6 数据查询

普通查询：  

```python
from sqlalchemy import select

# 查询全部
result = await db.execute(select(Book))
books = result.scalars().all()

# 查询单条
book = result.scalars().first()          # 第一条
book = result.scalars().one_or_none()    # 唯一一条，多条则报错
book = await db.get(Book, 1)             # 按主键查询

# 聚合标量（count/sum 等单值结果）
total = result.scalar()
```

查询条件 where()：  

```python
# 比较运算：==、>、<、>=、<=
where(Book.id == 1, Book.price > 50)

# 模糊查询：like，% 匹配多个字符，_ 匹配单个字符
where(Book.bookname.like("%Python%"))
where(Book.bookname.like("_ython"))

# 与 / 或 / 非：&、|、~
where(Book.id > 5, Book.is_delete == False)
where((Book.id > 5) | (Book.price < 20))
where(~Book.is_delete)

# 包含：in_
where(Book.id.in_([1, 2, 3]))
```

聚合函数：  

```python
from sqlalchemy import func

result = await db.execute(select(func.count(Book.id)))
total = result.scalar()

result = await db.execute(select(func.avg(Book.price)))
avg_price = result.scalar()
```

分页查询：  

```python
skip = (page - 1) * page_size
result = await db.execute(
    select(Book).offset(skip).limit(page_size)
)
```

其中 offset 表示跳过的条数，limit 表示取出的条数；skip 由页码换算：offset = (页码 - 1) * 每页数量。  

#### 2-2-3-7 新增、修改、删除

新增：  

```python
new_book = Book(**book.__dict__)   # 由 Pydantic 模型转 ORM 模型
db.add(new_book)
await db.commit()
```

修改：先查再改，重新赋值后提交。  

```python
book = await db.get(Book, id)
if book is None:
    raise HTTPException(status_code=404, detail="Book not found")
book.bookname = "新书名"
await db.commit()
```

删除：  

```python
book = await db.get(Book, id)
if book is None:
    raise HTTPException(status_code=404, detail="Book not found")
await db.delete(book)
await db.commit()
```

> 注意：修改与删除前都要先查询目标对象并判断是否存在，不存在时抛出 HTTPException，避免操作无效数据。  

#### 2-2-3-8 本章总结

```vtable
{"rows": [[{"t": "操作类型", "rs": 1, "cs": 1}, {"t": "方法", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}], [{"t": "条件查询", "rs": 1, "cs": 1}, {"t": "where(条件1, 条件2, ...)", "rs": 1, "cs": 1}, {"t": "select(User).where(User.username == “daqiu”)", "rs": 1, "cs": 1}], [{"t": "模糊查询", "rs": 1, "cs": 1}, {"t": "like / ilike", "rs": 1, "cs": 1}, {"t": "News.title.like(“%AI%”)", "rs": 1, "cs": 1}], [{"t": "范围查询", "rs": 1, "cs": 1}, {"t": "in_", "rs": 1, "cs": 1}, {"t": "News.category_id.in_([1, 2, 3])", "rs": 1, "cs": 1}], [{"t": "聚合", "rs": 1, "cs": 1}, {"t": "func.count / avg / max / min / sum", "rs": 1, "cs": 1}, {"t": "select(func.count(News.id))", "rs": 1, "cs": 1}], [{"t": "排序", "rs": 1, "cs": 1}, {"t": "order_by(字段.asc() / .desc())", "rs": 1, "cs": 1}, {"t": "order_by(News.views.desc())", "rs": 1, "cs": 1}], [{"t": "分页", "rs": 1, "cs": 1}, {"t": "offset(skip).limit(limit)", "rs": 1, "cs": 1}, {"t": "offset((page - 1) * size).limit(size)", "rs": 1, "cs": 1}]]}
```


# 3 项目实战-AI掘金头条（新闻模块）

## 3-3 项目实战 - AI 掘金头条（新闻模块）

### 3-3-1 项目介绍

AI 掘金头条是一个前后端分离的新闻资讯项目，后端使用 FastAPI 实现。  
项目整体功能包含三大模块：新闻模块、用户模块、收藏和浏览历史模块，本笔记将分章节逐一实现。  

![项目介绍](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch3_project_intro.png)  

配套物料包括：前端 Vue 代码、接口规范文档、MySQL SQL 文件、设计说明文档。  
前端运行方式：安装 Node 环境后，进入前端项目目录执行 npm run dev 启动开发服务器（默认端口 5173）。  

### 3-3-2 工程结构

后端项目 toutiao_backend 采用分层结构，各目录职责清晰：  

```vtable
{"rows": [[{"t": "目录", "rs": 1, "cs": 1}, {"t": "职责", "rs": 1, "cs": 1}, {"t": "示例文件", "rs": 1, "cs": 1}], [{"t": "crud/", "rs": 1, "cs": 1}, {"t": "数据库增删改查逻辑", "rs": 1, "cs": 1}, {"t": "news_crud.py", "rs": 1, "cs": 1}], [{"t": "models/", "rs": 1, "cs": 1}, {"t": "SQLAlchemy ORM 模型类", "rs": 1, "cs": 1}, {"t": "news.py、user.py", "rs": 1, "cs": 1}], [{"t": "routers/", "rs": 1, "cs": 1}, {"t": "路由层，按模块拆分", "rs": 1, "cs": 1}, {"t": "news.py、user.py、favorite.py、history.py", "rs": 1, "cs": 1}], [{"t": "schemas/", "rs": 1, "cs": 1}, {"t": "Pydantic 数据验证模型", "rs": 1, "cs": 1}, {"t": "news_schema.py、user_schema.py", "rs": 1, "cs": 1}], [{"t": "utils/", "rs": 1, "cs": 1}, {"t": "工具类（通用响应封装等）", "rs": 1, "cs": 1}, {"t": "response.py", "rs": 1, "cs": 1}], [{"t": "config/db_conf.py", "rs": 1, "cs": 1}, {"t": "数据库配置（引擎、会话）", "rs": 1, "cs": 1}, {"t": "异步引擎与 get_db 依赖", "rs": 1, "cs": 1}], [{"t": "main.py", "rs": 1, "cs": 1}, {"t": "应用入口，注册各模块路由", "rs": 1, "cs": 1}, {"t": "include_router 汇总注册", "rs": 1, "cs": 1}], [{"t": "test_main.http", "rs": 1, "cs": 1}, {"t": "接口测试文件", "rs": 1, "cs": 1}, {"t": "IDEA 中直接运行请求", "rs": 1, "cs": 1}]]}
```

![工程结构](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch3_structure.png)  

### 3-3-3 模块化路由

项目采用 APIRouter 按模块拆分路由，避免所有接口都堆在 main.py 中。  
以新闻模块为例：  

```python
# routers/news.py
from fastapi import APIRouter

news = APIRouter(prefix="/api/news", tags=["news"])
```

在 main.py 中注册：  

```python
# main.py
from routers.news import news

app = FastAPI()
app.include_router(news.router)
```

prefix="/api/news" 为路由统一前缀，tags=["news"] 用于 API 文档分组。  
模块化路由的优势：结构清晰、易于维护、避免 main.py 越来越庞大（main.py 爆炸）。  

### 3-3-4 配置 ORM

#### 3-3-4-1 安装依赖

```bash
pip install "sqlalchemy[asyncio]" aiomysql
```

#### 3-3-4-2 导入数据库

在 PyCharm 的 Database 面板中，通过 Run SQL Script 导入项目自带的 database.sql 文件。  
数据库名为 news_app，包含 8 张表：ai_chat、favorite、history、news、news_category、related_news、user、user_token。  

![导入 SQL 文件](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch3_import_sql.png)  

#### 3-3-4-3 配置异步引擎与会话

```python
# config/db_conf.py
from sqlalchemy.ext.asyncio import create_async_engine, async_sessionmaker, AsyncSession

ASYNC_DATABASE_URL = "mysql+aiomysql://root:123456@localhost:3306/news_app?charset=utf8mb4"

# 创建异步引擎
async_engine = create_async_engine(
    ASYNC_DATABASE_URL,
    echo=True,        # 输出 SQL 日志
    pool_size=10,     # 持久连接数
    max_overflow=20   # 额外连接数
)

# 创建会话工厂
AsyncSessionLocal = async_sessionmaker(
    bind=async_engine,
    class_=AsyncSession,
    expire_on_commit=False
)

# 数据库会话依赖
async def get_db():
    async with AsyncSessionLocal() as session:
        try:
            yield session
            await session.commit()
        except Exception:
            await session.rollback()
            raise
        finally:
            await session.close()
```

> 注意：charset=utf8mb4 才能完整支持中文与 emoji 表情，与建库时的字符集保持一致。  

#### 3-3-4-4 定义模型类

模型类参照数据库表结构定义，News 模型如下（完整模板见《7. ORM 模板代码》）：  

```python
# models/news.py
from datetime import datetime
from typing import Optional

from sqlalchemy import String, Text, DateTime, ForeignKey, Index
from sqlalchemy.orm import Mapped, mapped_column

class News(Base):
    """新闻表"""
    __tablename__ = "news"

    id: Mapped[int] = mapped_column(primary_key=True, comment="主键ID")
    title: Mapped[str] = mapped_column(String(255), nullable=False, comment="新闻标题")
    description: Mapped[Optional[str]] = mapped_column(String(500), comment="新闻简介")
    content: Mapped[str] = mapped_column(Text, comment="新闻内容")
    image: Mapped[Optional[str]] = mapped_column(String(255), comment="封面图片")
    author: Mapped[Optional[str]] = mapped_column(String(50), comment="作者")
    category_id: Mapped[int] = mapped_column(ForeignKey("news_category.id"), nullable=False, comment="分类ID")
    views: Mapped[int] = mapped_column(default=0, comment="浏览量")
    publish_time: Mapped[datetime] = mapped_column(DateTime, default=datetime.now, comment="发布时间")
```

新闻分类模型 NewsCategory 参照表 news_category：id（name 自增）、name varchar(50)、sort_order int 默认 0、created_at、updated_at。  

表索引通过 __table_args__ 声明，提高查询效率：  

```python
class News(Base):
    __table_args__ = (
        Index('fk_news_category_idx', 'category_id'),
        Index('idx_publish_time', 'publish_time'),
    )
```

### 3-3-5 接口实现流程

每个业务模块的接口开发都遵循固定四步：  

```vtable
{"rows": [[{"t": "步骤", "rs": 1, "cs": 1}, {"t": "内容", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "第一步", "rs": 1, "cs": 1}, {"t": "模块化路由", "rs": 1, "cs": 1}, {"t": "APIRouter(prefix=“/api/news”, tags=[“新闻”]) 定义路由对象，main.py 中 include_router 注册", "rs": 1, "cs": 1}], [{"t": "第二步", "rs": 1, "cs": 1}, {"t": "定义模型类", "rs": 1, "cs": 1}, {"t": "models/news.py 中字段、类型与 database.sql 表结构一一对应", "rs": 1, "cs": 1}], [{"t": "第三步", "rs": 1, "cs": 1}, {"t": "数据库 CRUD 逻辑", "rs": 1, "cs": 1}, {"t": "crud/ 中封装增删改查，路由层复用", "rs": 1, "cs": 1}], [{"t": "第四步", "rs": 1, "cs": 1}, {"t": "路由调用逻辑", "rs": 1, "cs": 1}, {"t": "Depends(get_db) 注入会话，组装响应结果返回", "rs": 1, "cs": 1}]]}
```

### 3-3-6 新闻分类列表

接口文档：GET /api/news/categories，查询参数 skip、limit（分页）。  
响应格式：{"code": 200, "message": "success", "data": [...]}，这是整个项目统一的响应结构。  

```python
@router.get("/categories")
async def get_categories(
    skip: int = 0,
    limit: int = 20,
    db: AsyncSession = Depends(get_db)
):
    result = await db.execute(
        select(NewsCategory).offset(skip).limit(limit)
    )
    categories = result.scalars().all()
    return success_response(data=categories)
```

### 3-3-7 新闻列表

#### 3-3-7-1 接口文档

GET /api/news/list，请求参数：  

```vtable
{"rows": [[{"t": "参数名", "rs": 1, "cs": 1}, {"t": "类型", "rs": 1, "cs": 1}, {"t": "必填", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "校验规则", "rs": 1, "cs": 1}], [{"t": "categoryId", "rs": 1, "cs": 1}, {"t": "integer", "rs": 1, "cs": 1}, {"t": "是", "rs": 1, "cs": 1}, {"t": "分类ID", "rs": 1, "cs": 1}, {"t": "Query(..., alias=“categoryId”) 必填", "rs": 1, "cs": 1}], [{"t": "page", "rs": 1, "cs": 1}, {"t": "integer", "rs": 1, "cs": 1}, {"t": "否", "rs": 1, "cs": 1}, {"t": "页码，默认为 1", "rs": 1, "cs": 1}, {"t": "Query(1, ge=1) 最小为 1", "rs": 1, "cs": 1}], [{"t": "pageSize", "rs": 1, "cs": 1}, {"t": "integer", "rs": 1, "cs": 1}, {"t": "否", "rs": 1, "cs": 1}, {"t": "每页显示的新闻数量，默认为 10", "rs": 1, "cs": 1}, {"t": "Query(10, ge=1, le=100, alias=“pageSize”) 最大 100", "rs": 1, "cs": 1}]]}
```

请求示例：  

```text
GET /api/news/list?categoryId=1
GET /api/news/list?categoryId=1&page=2&pageSize=20
```

响应示例：  

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "list": [
      {"id": 1, "category": null, "title": "新闻标题", "description": "新闻简介", "content": "新闻内容"}
    ],
    "total": 100,
    "hasMore": true
  }
}
```

![获取新闻列表](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch3_news_list_flow.png)  

#### 3-3-7-2 接口实现

新闻列表的查询功能 = 列表数据 + 总量统计 + hasMore 判断。  
hasMore 的计算公式：hasMore = (offset + 当前列表条数) < total，即"已取出的数据是否还没取完"。  

```python
@router.get("/list")
async def get_news(
    category_id: int = Query(..., alias="categoryId"),
    page: int = 1,
    page_size: int = Query(10, le=100, alias="pageSize"),
    db: AsyncSession = Depends(get_db)
):
    # 计算分页偏移
    offset = (page - 1) * page_size

    # 1. 查询当前页新闻列表
    result = await db.execute(
        select(News)
        .where(News.category_id == category_id)
        .offset(offset)
        .limit(page_size)
    )
    news_list = result.scalars().all()

    # 2. 查询总数
    total_result = await db.execute(
        select(func.count(News.id)).where(News.category_id == category_id)
    )
    total = total_result.scalar()

    # 3. 是否还有更多
    has_more = (offset + len(news_list)) < total

    return {
        "code": 200,
        "message": "success",
        "data": {
            "list": news_list,
            "total": total,
            "hasMore": has_more
        }
    }
```

> 注意：前端传参是驼峰命名 categoryId、pageSize，接口参数通过 alias="categoryId"、alias="pageSize" 与前端对齐；page 直接用小写即可。  

### 3-3-8 新闻详情与相关推荐

接口文档：GET /api/news/detail?id=xxx。  
业务流程：查询新闻 → 浏览量 +1（update 后通过 rowcount 判断是否命中）→ 查询相关推荐。  

![获取新闻详情](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch3_news_detail_flow.png)  

```python
@router.get("/detail")
async def get_news_detail(
    news_id: int = Query(...),
    db: AsyncSession = Depends(get_db)
):
    # 1. 查询新闻
    result = await db.execute(select(News).where(News.id == news_id))
    news = result.scalars().first()
    if news is None:
        raise HTTPException(status_code=404, detail="新闻不存在")

    # 2. 浏览量 +1
    update_result = await db.execute(
        update(News).where(News.id == news_id).values(views=News.views + 1)
    )
    # rowcount 大于 0 表示更新命中记录
    if update_result.rowcount > 0:
        await db.commit()

    # 3. 相关推荐：同分类下排除当前新闻，按浏览量倒序
    related_result = await db.execute(
        select(News)
        .where(News.id != news_id, News.category_id == news.category_id)
        .order_by(News.views.desc())
        .limit(5)
    )
    related_list = related_result.scalars().all()

    return {
        "code": 200,
        "message": "success",
        "data": {
            "news": news,
            "related_list": related_list
        }
    }
```

排序说明：select().order_by(News.views.desc()) 按浏览量降序；默认是升序（asc），desc 表示降序。  

> 注意：浏览量自增用 update 语句 + values(views=News.views + 1) 实现，比"先查出来再改值"少一次查询，也更安全。  

### 3-3-9 跨域资源共享 CORS

#### 3-3-9-1 同源三条件

跨域资源共享（CORS）是一种浏览器安全机制，用于允许运行在一个源（Origin）的 Web 应用，通过浏览器向另一个源的服务器发起跨域 HTTP 请求，并在服务器授权的前提下获取资源。  
判断是否同源看三个条件：协议、域名、端口，三者完全一致才叫同源。  

![跨域判断](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch3_cors.png)  

```vtable
{"rows": [[{"t": "前端地址", "rs": 1, "cs": 1}, {"t": "后端地址", "rs": 1, "cs": 1}, {"t": "是否跨域", "rs": 1, "cs": 1}, {"t": "原因", "rs": 1, "cs": 1}], [{"t": "http://localhost:5173", "rs": 1, "cs": 1}, {"t": "http://localhost:8000", "rs": 1, "cs": 1}, {"t": "跨域", "rs": 1, "cs": 1}, {"t": "端口不同（5173 vs 8000）", "rs": 1, "cs": 1}], [{"t": "http://example.com", "rs": 1, "cs": 1}, {"t": "http://api.example.com", "rs": 1, "cs": 1}, {"t": "跨域", "rs": 1, "cs": 1}, {"t": "域名不同（example.com vs api.example.com）", "rs": 1, "cs": 1}], [{"t": "http://example.com", "rs": 1, "cs": 1}, {"t": "https://example.com", "rs": 1, "cs": 1}, {"t": "跨域", "rs": 1, "cs": 1}, {"t": "协议不同（http vs https）", "rs": 1, "cs": 1}], [{"t": "http://example.com", "rs": 1, "cs": 1}, {"t": "http://example.com", "rs": 1, "cs": 1}, {"t": "不跨域", "rs": 1, "cs": 1}, {"t": "协议、域名、端口三者完全一致", "rs": 1, "cs": 1}]]}
```

本项目前端运行在 http://localhost:5173，后端运行在 http://127.0.0.1:8000，端口不同属于跨域。  
浏览器会拦截跨域响应并报错：No 'Access-Control-Allow-Origin' header。  

#### 3-3-9-2 使用 CORSMiddleware 解决跨域

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],       # 允许的源，* 表示全部
    allow_credentials=True,    # 允许携带凭证（Cookie 等）
    allow_methods=["*"],       # 允许的请求方法
    allow_headers=["*"]        # 允许的请求头
)
```

> 注意：allow_origins=["*"] 仅适合开发环境；生产环境应改为具体的前端域名列表，避免任意网站都能调用接口。  

### 3-3-10 本章总结

本章完成了新闻模块的三个核心接口（分类、列表、详情）与跨域配置，要点如下：  

```vtable
{"rows": [[{"t": "要点", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "接口实现四步", "rs": 1, "cs": 1}, {"t": "模块化路由 → 定义模型类 → 数据库 CRUD → 路由调用逻辑", "rs": 1, "cs": 1}], [{"t": "模型类参照库表", "rs": 1, "cs": 1}, {"t": "models 中的字段、类型、约束与 database.sql 一一对应", "rs": 1, "cs": 1}], [{"t": "hasMore 判断", "rs": 1, "cs": 1}, {"t": "hasMore = (offset + 当前列表条数) < total", "rs": 1, "cs": 1}], [{"t": "浏览量自增", "rs": 1, "cs": 1}, {"t": "update + values(views=News.views + 1)，rowcount 判断命中", "rs": 1, "cs": 1}], [{"t": "相关推荐", "rs": 1, "cs": 1}, {"t": "同类目按浏览量倒序 order_by(News.views.desc()).limit(3)", "rs": 1, "cs": 1}], [{"t": "CORS 同源三条件", "rs": 1, "cs": 1}, {"t": "协议、域名、端口全部一致才算同源", "rs": 1, "cs": 1}]]}
```


# 4 项目实战-AI掘金头条（用户模块）

## 4-4 项目实战 - AI 掘金头条（用户模块）

### 4-4-1 用户模块功能

用户模块包含注册、登录、获取用户信息、修改用户信息、修改密码五个核心功能，并配套 Token 认证、passlib 密码加密、通用成功响应封装、全局异常处理等支撑组件。  

![用户模块界面](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch4_user_ui.png)  

### 4-4-2 用户注册

#### 4-4-2-1 接口文档

POST /api/user/register，请求体：  

```json
{
  "username": "daqiu",
  "password": "123456"
}
```

响应：{"code": 200, "message": "注册成功", "data": {"token": "xxx", "userInfo": {"bio": "...", "avatar": "..."}}}。  

#### 4-4-2-2 注册业务流程

![注册业务流程](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch4_register_flow.png)  

注册流程分三步：先查询用户名是否已存在（查重）；不存在则创建用户（密码用 passlib 哈希加密后入库）；最后用 uuid 生成 Token 并返回给前端。  

#### 4-4-2-3 接口实现

```python
@router.post("/register")
async def register(
    user: UserRegisterRequest,
    db: AsyncSession = Depends(get_db)
):
    # 1. 查重：用户名已存在则报错
    result = await db.execute(
        select(User).where(User.username == user.username)
    )
    if result.scalars().first() is not None:
        raise HTTPException(status_code=400, detail="用户名已存在")

    # 2. 创建用户，密码哈希加密
    hashed_password = pwd_context.hash(user.password)
    new_user = User(
        username=user.username,
        password=hashed_password,
        bio="这个人很懒，什么都没留下",   # 默认个性签名
        avatar="https://example.com/cat.png"   # 默认头像
    )
    db.add(new_user)
    await db.commit()

    # 3. 生成 Token
    token = str(uuid.uuid4())

    return success_response(
        message="注册成功",
        data=UserAuthResponse(
            token=token,
            user_info=UserInfoResponse.model_validate(new_user)
        )
    )
```

#### 4-4-2-4 passlib 密码加密

安装指定版本（bcrypt 方案）：  

```bash
pip install "passlib[bcrypt]==1.7.4"
```

使用三步：创建加密上下文 → 加密 → 校验。  

```python
from passlib.context import CryptContext

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

# 加密：注册时使用
hashed_password = pwd_context.hash("123456")

# 校验：登录时使用
result = pwd_context.verify("123456", hashed_password)
```

> 注意：用户密码绝不能明文存储，必须哈希后入库；校验使用 verify（明文 + 哈希值），而不是把哈希值解密。  

#### 4-4-2-5 Token 认证

Token 是服务器发给客户端的一串字符串，用于解决 HTTP 无状态问题——HTTP 每次请求相互独立，服务器无法记住客户端，而 Token 可以让客户端"在每次请求中自我证明身份"。  

Token 工作流程：  

![Token 工作流程](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch4_token_flow.png)  

登录/注册 → 后端生成 Token → 返回给前端 → 前端保存 → 每次请求携带 → 后端验证。  

Token 在请求头中的位置：Authorization: Bearer <token>。  

```vtable
{"rows": [[{"t": "组成部分", "rs": 1, "cs": 1}, {"t": "含义", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}], [{"t": "Authorization", "rs": 1, "cs": 1}, {"t": "请求头键名，标识该请求头存放的是认证数据", "rs": 1, "cs": 1}, {"t": "Authorization: Bearer xxxxx", "rs": 1, "cs": 1}], [{"t": "Bearer", "rs": 1, "cs": 1}, {"t": "持有者令牌，固定前缀，表示后面跟着的是 Token 字符串", "rs": 1, "cs": 1}, {"t": "Bearer 与 Token 之间用空格分隔", "rs": 1, "cs": 1}], [{"t": "token", "rs": 1, "cs": 1}, {"t": "身份凭证，服务器下发的令牌本体", "rs": 1, "cs": 1}, {"t": "str(uuid.uuid4()) 生成的随机字符串", "rs": 1, "cs": 1}]]}
```

### 4-4-3 用户登录

POST /api/user/login，业务流程：查用户 → 存在则用 CryptContext.verify 校验密码 → 密码不一致或用户不存在返回错误 → 校验通过生成 Token → 返回"登录成功"与 userInfo{nickname, avatar, bio}。  

![登录业务流程](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch4_login_flow.png)  

```python
@router.post("/login")
async def login(
    user: UserLoginRequest,
    db: AsyncSession = Depends(get_db)
):
    # 1. 查询用户
    result = await db.execute(
        select(User).where(User.username == user.username)
    )
    db_user = result.scalars().first()

    # 2. 校验密码：用户不存在或密码错误都返回统一错误
    if db_user is None or not pwd_context.verify(user.password, db_user.password):
        raise HTTPException(status_code=400, detail="用户名或密码错误")

    # 3. 生成 Token
    token = str(uuid.uuid4())

    return success_response(
        message="登录成功",
        data=UserAuthResponse(
            token=token,
            user_info=UserInfoResponse.model_validate(db_user)
        )
    )
```

### 4-4-4 获取用户信息

GET /api/user/info，需要认证：从请求头 Authorization 中取 Token，查询 user_token 表验证令牌有效性（存在且未过期），再查询用户信息返回。  

使用 Header 工具从请求头取 Token：  

```python
from fastapi import Header

@router.get("/info")
async def get_user_info(
    authorization: str = Header(...),
    db: AsyncSession = Depends(get_db)
):
    # authorization 形如 "Bearer xxxxx"，取空格后的一段
    token = authorization.split(" ")[-1]

    # 验证 Token 有效性
    token_result = await db.execute(
        select(UserToken).where(UserToken.token == token)
    )
    db_token = token_result.scalars().first()
    if db_token is None:
        raise HTTPException(status_code=401, detail="登录已失效")

    # 查询用户并返回
    user_result = await db.execute(
        select(User).where(User.id == db_token.user_id)
    )
    user = user_result.scalars().first()
    return success_response(data=user)
```

请求头的作用：携带身份信息、请求控制、数据格式、客户端环境等元数据。  

> 注意：Header(...) 表示 Authorization 请求头必填；未登录或 Token 无效时应返回 401 状态码。  

### 4-4-5 修改用户信息

PUT /api/user/update，需要认证。认证通过后查询用户，修改 nickname、avatar、gender、bio、phone 字段并提交。  

```python
@router.put("/update")
async def update_user(
    body: UserUpdateRequest,
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    # 已通过 get_current_user 认证，直接修改字段
    user.nickname = body.nickname if body.nickname else user.nickname
    user.avatar = body.avatar if body.avatar else user.avatar
    user.gender = body.gender
    user.bio = body.bio
    user.phone = body.phone
    await db.commit()

    return success_response(message="更新成功")
```

get_current_user 是复用的认证依赖：取出 Authorization 请求头 → 验证 Token → 查询用户 → 返回当前用户对象；未认证时抛出 401 异常，避免每个接口重复编写认证逻辑。  

### 4-4-6 修改密码

PUT /api/user/password，请求体包含 oldPassword、newPassword。  
业务流程：认证 → 验证用户原密码（pwd_context.verify）→ 原密码正确则把新密码转成密文 → 更新密码字段。  

```python
@router.put("/password")
async def update_password(
    body: UserPasswordRequest,
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    # 1. 校验原密码
    if not pwd_context.verify(body.old_password, user.password):
        raise HTTPException(status_code=400, detail="原密码错误")

    # 2. 新密码转密文并更新
    user.password = pwd_context.hash(body.new_password)
    await db.commit()

    return success_response(message="修改密码成功")
```

### 4-4-7 封装通用成功响应格式

为了让所有接口返回结构统一（code/message/data），封装通用成功响应，分三步。  

第一步：封装函数 success_response。  

```python
from fastapi.responses import JSONResponse
from fastapi.encoders import jsonable_encoder

def success_response(message="success", data=None):
    return JSONResponse(
        jsonable_encoder({
            "code": 200,
            "message": message,
            "data": data
        })
    )
```

第二步：定义响应模型 UserAuthResponse，通过 ConfigDict(from_attributes=True) 支持自动序列化 ORM 对象。  

```python
from pydantic import BaseModel, ConfigDict

class UserAuthResponse(BaseModel):
    token: str
    user_info: UserInfoResponse

    model_config = ConfigDict(from_attributes=True)
```

第三步：调用 success_response 并传入响应模型实例。  

```python
return success_response(
    message="注册成功",
    data=UserAuthResponse(
        token=token,
        user_info=UserInfoResponse.model_validate(user)
    )
)
```

![封装通用成功响应](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch4_response_encap.png)  

### 4-4-8 全局异常处理器

FastAPI 允许在应用级别注册异常处理器，统一捕获业务层、数据库层、系统层的异常并返回统一格式的响应。  

```python
# 定义业务异常类
class BusinessException(Exception):
    def __init__(self, message="业务异常"):
        self.message = message

# 定义异常处理函数
async def business_exception_handler(request, exc):
    return JSONResponse(
        status_code=400,
        content={"code": 400, "message": exc.message, "data": None}
    )

# 注册异常处理器
app.add_exception_handler(BusinessException, business_exception_handler)
```

注册顺序有讲究：  

```vtable
{"rows": [[{"t": "注册顺序", "rs": 1, "cs": 1}, {"t": "异常类型", "rs": 1, "cs": 1}, {"t": "典型示例", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "1", "rs": 1, "cs": 1}, {"t": "业务异常（自定义）", "rs": 1, "cs": 1}, {"t": "BusinessException", "rs": 1, "cs": 1}, {"t": "最具体的异常优先注册", "rs": 1, "cs": 1}], [{"t": "2", "rs": 1, "cs": 1}, {"t": "数据约束异常（子类）", "rs": 1, "cs": 1}, {"t": "IntegrityError（唯一约束、外键约束）", "rs": 1, "cs": 1}, {"t": "子类异常优先于父类", "rs": 1, "cs": 1}], [{"t": "3", "rs": 1, "cs": 1}, {"t": "数据库异常（父类）", "rs": 1, "cs": 1}, {"t": "SQLAlchemyError", "rs": 1, "cs": 1}, {"t": "覆盖常见数据库错误", "rs": 1, "cs": 1}], [{"t": "4", "rs": 1, "cs": 1}, {"t": "所有异常（Exception）", "rs": 1, "cs": 1}, {"t": "Exception", "rs": 1, "cs": 1}, {"t": "兜底捕获，统一响应", "rs": 1, "cs": 1}]]}
```

> 注意：异常处理器的注册顺序是"先子类后父类"——先注册具体异常，再注册通用异常，否则父类处理器会拦截所有子类异常。  

### 4-4-9 本章总结

```vtable
{"rows": [[{"t": "要点", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "Token 生成", "rs": 1, "cs": 1}, {"t": "str(uuid.uuid4()) 生成随机字符串作为身份凭证", "rs": 1, "cs": 1}], [{"t": "Header 获取认证", "rs": 1, "cs": 1}, {"t": "authorization: str = Header(...) 从请求头取 Token", "rs": 1, "cs": 1}], [{"t": "passlib 加密三步", "rs": 1, "cs": 1}, {"t": "安装 passlib[bcrypt] → CryptContext 创建上下文 → hash 加密 / verify 校验", "rs": 1, "cs": 1}], [{"t": "成功响应三步", "rs": 1, "cs": 1}, {"t": "success_response 封装函数 → UserAuthResponse 响应模型 → model_validate 序列化调用", "rs": 1, "cs": 1}], [{"t": "全局异常处理器", "rs": 1, "cs": 1}, {"t": "定义异常类 + 处理函数 + app.add_exception_handler 注册（先子类后父类）", "rs": 1, "cs": 1}], [{"t": "修改信息与密码", "rs": 1, "cs": 1}, {"t": "PUT /api/user/update、PUT /api/user/password，均需认证", "rs": 1, "cs": 1}], [{"t": "默认值兜底", "rs": 1, "cs": 1}, {"t": "新用户默认个性签名与默认头像，避免前端显示空白", "rs": 1, "cs": 1}]]}
```


# 5 项目实战-AI掘金头条（收藏和浏览历史）

## 5-5 项目实战 - AI 掘金头条（收藏和浏览历史）

### 5-5-1 收藏模块

收藏模块共五个接口，所有接口都需要用户认证：路由参数声明 user: User = Depends(get_current_user)，未登录时 get_current_user 会抛出 401 异常。  

#### 5-5-1-1 检查收藏状态

GET /api/favorite/check?newsId=xxx，查询当前用户是否已收藏该新闻，返回 {"isFavorite": true/false}。  

```python
@router.get("/check")
async def check_favorite(
    news_id: int = Query(..., alias="newsId"),
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    result = await db.execute(
        select(Favorite).where(
            Favorite.user_id == user.id,
            Favorite.news_id == news_id
        )
    )
    is_favorite = result.scalars().first() is not None
    return {"isFavorite": is_favorite}
```

#### 5-5-1-2 添加收藏

POST /api/favorite/add，请求体 FavoriteAddRequest{newsId}，添加收藏记录后返回"收藏成功"。  

```python
@router.post("/add")
async def add_favorite(
    body: FavoriteAddRequest,
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    favorite = Favorite(user_id=user.id, news_id=body.news_id)
    db.add(favorite)
    await db.commit()
    return success_response(message="收藏成功")
```

#### 5-5-1-3 取消收藏

DELETE /api/favorite/remove?newsId=xxx，删除收藏记录后返回"取消收藏成功"。  

```python
@router.delete("/remove")
async def remove_favorite(
    news_id: int = Query(..., alias="newsId"),
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    result = await db.execute(
        select(Favorite).where(
            Favorite.user_id == user.id,
            Favorite.news_id == news_id
        )
    )
    favorite = result.scalars().first()
    if favorite is not None:
        await db.delete(favorite)
        await db.commit()
    return success_response(message="取消收藏成功")
```

#### 5-5-1-4 获取收藏列表

GET /api/favorite/list?page&pageSize，返回当前用户的收藏新闻列表，包含总量与 hasMore，列表项带收藏时间 favoriteTime。  
实现要点是 ORM 联表查询：select(News).join(Favorite)。  

![我的收藏界面](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch5_favorite_ui.png)  

```python
@router.get("/list")
async def get_favorite_list(
    page: int = Query(1, ge=1),
    page_size: int = Query(10, ge=1, le=100, alias="pageSize"),
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    offset = (page - 1) * page_size

    # 1. 联表查询当前页收藏的新闻
    result = await db.execute(
        select(News)
        .join(Favorite, Favorite.news_id == News.id)
        .where(Favorite.user_id == user.id)
        .offset(offset)
        .limit(page_size)
    )
    news_list = result.scalars().all()

    # 2. 统计总数
    total_result = await db.execute(
        select(func.count(Favorite.id)).where(Favorite.user_id == user.id)
    )
    total = total_result.scalar()

    # 3. 是否还有更多
    has_more = (offset + len(news_list)) < total

    return {
        "code": 200,
        "message": "success",
        "data": {
            "list": news_list,
            "total": total,
            "hasMore": has_more
        }
    }
```

#### 5-5-1-5 清空收藏

DELETE /api/favorite/clear，删除当前用户的全部收藏，通过 result.rowcount 统计删除条数并返回"清空xx条收藏记录"。  

```python
@router.delete("/clear")
async def clear_favorite(
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    result = await db.execute(
        delete(Favorite).where(Favorite.user_id == user.id)
    )
    await db.commit()
    return success_response(message=f"清空{result.rowcount}条收藏记录")
```

### 5-5-2 浏览历史

浏览历史模块共四个接口，同样全部需要用户认证。  

#### 5-5-2-1 添加浏览记录

POST /api/history/add，请求体 {newsId}。  
业务逻辑：先查询该用户是否已浏览过这条新闻——已浏览过则更新浏览时间；未浏览过则新增记录。  

```python
@router.post("/add")
async def add_history(
    body: HistoryAddRequest,
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    result = await db.execute(
        select(History).where(
            History.user_id == user.id,
            History.news_id == body.news_id
        )
    )
    history = result.scalars().first()

    if history is not None:
        # 已浏览过：更新浏览时间
        history.view_time = datetime.now()
    else:
        # 未浏览过：新增记录
        db.add(History(user_id=user.id, news_id=body.news_id))
    await db.commit()
    return success_response(message="添加成功")
```

#### 5-5-2-2 获取浏览历史列表

GET /api/history/list?page&pageSize，联表 select(News).join(History) 查询当前用户的浏览记录，列表项带浏览时间 viewTime，同样包含 total 与 hasMore。  

![浏览历史界面](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch5_history_ui.png)  

```python
@router.get("/list")
async def get_history_list(
    page: int = Query(1, ge=1),
    page_size: int = Query(10, ge=1, le=100, alias="pageSize"),
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    offset = (page - 1) * page_size

    result = await db.execute(
        select(News)
        .join(History, History.news_id == News.id)
        .where(History.user_id == user.id)
        .offset(offset)
        .limit(page_size)
    )
    news_list = result.scalars().all()

    total_result = await db.execute(
        select(func.count(History.id)).where(History.user_id == user.id)
    )
    total = total_result.scalar()

    has_more = (offset + len(news_list)) < total

    return {
        "code": 200,
        "message": "success",
        "data": {
            "list": news_list,
            "total": total,
            "hasMore": has_more
        }
    }
```

#### 5-5-2-3 删除单条浏览记录

DELETE /api/history/delete/{history_id}，路径参数指定要删除的记录 id，删除后通过命中数量判断并返回"删除成功"。  

```python
@router.delete("/delete/{history_id}")
async def delete_history(
    history_id: int,
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    result = await db.execute(
        delete(History).where(
            History.id == history_id,
            History.user_id == user.id
        )
    )
    await db.commit()
    if result.rowcount == 0:
        raise HTTPException(status_code=404, detail="记录不存在")
    return success_response(message="删除成功")
```

#### 5-5-2-4 清空浏览历史

DELETE /api/history/clear，删除当前用户的全部浏览记录，返回"清空成功"。  

```python
@router.delete("/clear")
async def clear_history(
    user: User = Depends(get_current_user),
    db: AsyncSession = Depends(get_db)
):
    await db.execute(
        delete(History).where(History.user_id == user.id)
    )
    await db.commit()
    return success_response(message="清空成功")
```

### 5-5-3 收藏 VS 浏览历史

![收藏与浏览历史对比](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch5_compare.png)  

```vtable
{"rows": [[{"t": "维度", "rs": 1, "cs": 1}, {"t": "收藏", "rs": 1, "cs": 1}, {"t": "浏览历史", "rs": 1, "cs": 1}], [{"t": "触发方式", "rs": 1, "cs": 1}, {"t": "用户主动点击收藏按钮", "rs": 1, "cs": 1}, {"t": "用户看过新闻即自动记录", "rs": 1, "cs": 1}], [{"t": "去重方式", "rs": 1, "cs": 1}, {"t": "user_id + news_id 唯一约束，重复收藏报错", "rs": 1, "cs": 1}, {"t": "重复浏览只更新浏览时间", "rs": 1, "cs": 1}], [{"t": "时间字段", "rs": 1, "cs": 1}, {"t": "favoriteTime（收藏时间）", "rs": 1, "cs": 1}, {"t": "viewTime（浏览时间）", "rs": 1, "cs": 1}], [{"t": "接口数量", "rs": 1, "cs": 1}, {"t": "5 个（check/add/remove/list/clear）", "rs": 1, "cs": 1}, {"t": "4 个（add/list/delete/clear）", "rs": 1, "cs": 1}], [{"t": "列表实现", "rs": 1, "cs": 1}, {"t": "select(News).join(Favorite) 联表查询", "rs": 1, "cs": 1}, {"t": "select(News).join(History) 联表查询", "rs": 1, "cs": 1}], [{"t": "删除粒度", "rs": 1, "cs": 1}, {"t": "单条 remove + 清空 clear", "rs": 1, "cs": 1}, {"t": "单条 delete/{history_id} + 清空 clear", "rs": 1, "cs": 1}], [{"t": "认证要求", "rs": 1, "cs": 1}, {"t": "全部接口 Depends(get_current_user)", "rs": 1, "cs": 1}, {"t": "全部接口 Depends(get_current_user)", "rs": 1, "cs": 1}]]}
```

### 5-5-4 本章总结

ORM 联表查询：把收藏时间、收藏 id 等字段一起查出，通过 label 起别名。  

```python
select(
    News,
    Favorite.created_at.label("favorite_time"),
    Favorite.id.label("favorite_id")
).join(Favorite, Favorite.news_id == News.id)
```

唯一约束：防止同一用户重复收藏同一新闻，使用 UniqueConstraint 在表级声明。  

```python
class Favorite(Base):
    __tablename__ = "favorite"

    __table_args__ = (
        UniqueConstraint('user_id', 'news_id', name='user_news_unique'),
    )
```

收藏与浏览历史两类接口的统一模式：认证依赖 get_current_user → 分页参数 Query(1, ge=1) / Query(10, ge=1, le=100, alias="pageSize") → 联表查询 + func.count() 统计 + hasMore 判断。  

> 注意：列表接口的分页参数建议统一写法：page: int = Query(1, ge=1)，page_size: int = Query(10, ge=1, le=100, alias="pageSize")，保证所有列表接口行为一致。


# 6 项目实战-AI掘金头条（缓存与模型调用）

## 6-6 项目实战 - AI 掘金头条（缓存与模型调用）

### 6-6-1 缓存

#### 6-6-1-1 什么是缓存

缓存是一种高速临时数据存储机制：临时存储数据或计算结果，避免重复耗时获取。  
在项目中的作用：提升性能、降低延迟；减轻服务器和数据库负载；降低网络延迟；节省资源成本。  

#### 6-6-1-2 缓存架构

![缓存架构](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_cache_arch.png)  

用户/前端 → FastAPI 服务器（业务逻辑控制中心）→ 高速临时数据（取的快）+ 数据库（权威真实数据，存得住）。  
缓存负责快速读取，数据库负责数据持久化，两者配合各取所长。  

#### 6-6-1-3 项目中的缓存流程

![项目中的缓存流程](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_cache_flow.png)  

前端请求数据 → 服务器先查缓存 → 有缓存则直接返回数据；无缓存则查询数据库 → 将数据写入缓存 → 再返回给前端。  

### 6-6-2 Redis

#### 6-6-2-1 Redis 是什么

Redis 是一种高性能的 Key-Value 存储系统，它将数据存储在内存中，因此读写速度极快，非常适合作为应用层的缓存服务。  
在 FastAPI 这样的后端框架中，通常在应用层使用像 Redis 这样的内存数据存储作为缓存，默认端口号为 6379。  

![Redis 四步总览](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_redis_steps.png)  

使用 Redis 做缓存分四步：安装 Redis 服务端 → 配置 Redis 客户端 → 封装缓存操作 → 设计缓存策略。  

#### 6-6-2-2 安装 Redis 服务端

![安装 Redis 服务端](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_redis_install.png)  

Mac 系统：  

```bash
brew install redis
redis-server    # 验证：启动服务
```

Windows 系统：双击 .msi 安装文件完成安装，验证命令：  

```bash
redis-cli ping
```

返回 PONG 表示 Redis 服务正常运行。  

#### 6-6-2-3 配置 Redis 客户端

安装 Python 客户端：  

```bash
pip install redis
```

配置客户端：  

```python
import redis.asyncio as redis

redis_client = redis.Redis(
    host="127.0.0.1",
    port=6379,
    db=0,
    decode_responses=True
)
```

![配置 Redis 客户端](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_redis_client.png)  

配置参数说明：  

```vtable
{"rows": [[{"t": "参数", "rs": 1, "cs": 1}, {"t": "默认值", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "host", "rs": 1, "cs": 1}, {"t": "127.0.0.1", "rs": 1, "cs": 1}, {"t": "Redis 服务器地址，本机开发用 localhost", "rs": 1, "cs": 1}], [{"t": "port", "rs": 1, "cs": 1}, {"t": "6379", "rs": 1, "cs": 1}, {"t": "Redis 默认端口号", "rs": 1, "cs": 1}], [{"t": "db", "rs": 1, "cs": 1}, {"t": "0", "rs": 1, "cs": 1}, {"t": "数据库编号（0~15），不同业务可隔离", "rs": 1, "cs": 1}], [{"t": "decode_responses", "rs": 1, "cs": 1}, {"t": "False", "rs": 1, "cs": 1}, {"t": "True 时 get 直接返回字符串，否则返回 bytes 需手动 decode", "rs": 1, "cs": 1}]]}
```

> 注意：decode_responses=True 时 get 直接返回字符串，否则返回 bytes 字节流，需要手动 decode。  

#### 6-6-2-4 封装缓存操作

缓存操作就是围绕 Redis 做"存、取、删、判断、过期"等操作，让数据访问更快、数据库压力更小。  
Redis 存储数据的形式：key - value。  

![封装缓存操作](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_cache_ops.png)  

```vtable
{"rows": [[{"t": "方法", "rs": 1, "cs": 1}, {"t": "参数", "rs": 1, "cs": 1}, {"t": "返回值", "rs": 1, "cs": 1}, {"t": "描述", "rs": 1, "cs": 1}], [{"t": "setex(key, expire, value)", "rs": 1, "cs": 1}, {"t": "key: str，expire: int（秒），value: str", "rs": 1, "cs": 1}, {"t": "无", "rs": 1, "cs": 1}, {"t": "设置缓存并指定过期时间（秒）", "rs": 1, "cs": 1}], [{"t": "get(key)", "rs": 1, "cs": 1}, {"t": "key: str", "rs": 1, "cs": 1}, {"t": "字符串或 None", "rs": 1, "cs": 1}, {"t": "获取缓存值，若缓存不存在返回 None", "rs": 1, "cs": 1}], [{"t": "delete(key)", "rs": 1, "cs": 1}, {"t": "key: str", "rs": 1, "cs": 1}, {"t": "删除的键数量（int）", "rs": 1, "cs": 1}, {"t": "删除指定的缓存键", "rs": 1, "cs": 1}], [{"t": "exists(key)", "rs": 1, "cs": 1}, {"t": "key: str", "rs": 1, "cs": 1}, {"t": "True / False", "rs": 1, "cs": 1}, {"t": "检查缓存键是否存在，返回布尔值", "rs": 1, "cs": 1}]]}
```

封装示例：  

```python
# 设置缓存并配置过期时间
await redis_client.setex("news:list:1:1:10", 600, json.dumps(data, ensure_ascii=False))

# 获取缓存（不存在返回 None）
data = await redis_client.get("news:list:1:1:10")

# 删除缓存
await redis_client.delete("news:list:1:1:10")

# 判断缓存是否存在
exists = await redis_client.exists("news:list:1:1:10")
```

#### 6-6-2-5 设计缓存策略（旁路缓存 Cache-Aside）

最常见的缓存策略是旁路缓存（Cache-Aside）：  

```vtable
{"rows": [[{"t": "方向", "rs": 1, "cs": 1}, {"t": "流程", "rs": 1, "cs": 1}, {"t": "关键点", "rs": 1, "cs": 1}], [{"t": "读", "rs": 1, "cs": 1}, {"t": "先查缓存 → 命中直接返回；未命中 → 查数据库 → 写缓存 → 返回", "rs": 1, "cs": 1}, {"t": "未命中时先写缓存再返回，并设置过期时间 TTL", "rs": 1, "cs": 1}], [{"t": "写", "rs": 1, "cs": 1}, {"t": "更新数据库后，更新缓存或删除缓存", "rs": 1, "cs": 1}, {"t": "优先删除缓存，下次读取时重建，避免写脏数据", "rs": 1, "cs": 1}]]}
```

![缓存策略](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_cache_strategy.png)  

以新闻分类为例的完整流程：  

```python
async def get_categories(db):
    # 1. 先查缓存
    cached = await get_cached_categories()
    if cached is not None:
        return cached

    # 2. 未命中，查数据库
    result = await db.execute(select(Category))
    categories = result.scalars().all()

    # 3. 写缓存
    await set_cached_categories(jsonable_encoder(categories))
    return categories
```

不同类型的数据需要设置不同的缓存时间，否则会出现缓存雪崩；原则是数据越稳定缓存越久、数据变化越快缓存越短。  

![缓存时长设计](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_cache_ttl.png)  

```vtable
{"rows": [[{"t": "类型", "rs": 1, "cs": 1}, {"t": "时间", "rs": 1, "cs": 1}, {"t": "Key 示例", "rs": 1, "cs": 1}], [{"t": "分类、配置", "rs": 1, "cs": 1}, {"t": "7200（2小时）", "rs": 1, "cs": 1}, {"t": "news:category:list", "rs": 1, "cs": 1}], [{"t": "列表数据", "rs": 1, "cs": 1}, {"t": "600（10分钟）", "rs": 1, "cs": 1}, {"t": "news:list:1:1:10", "rs": 1, "cs": 1}], [{"t": "详情数据", "rs": 1, "cs": 1}, {"t": "1800（30分钟）", "rs": 1, "cs": 1}, {"t": "news:detail:101", "rs": 1, "cs": 1}], [{"t": "验证码", "rs": 1, "cs": 1}, {"t": "120（2分钟）", "rs": 1, "cs": 1}, {"t": "sms:code:13800001111", "rs": 1, "cs": 1}]]}
```

新闻列表的缓存 Key 设计：news:list:分类ID:页码:每页数量，Value 为新闻列表数据。  

> 注意：缓存 Key 必须包含查询的关键维度（分类、页码、每页数量），否则不同条件会命中同一份错误数据。  

### 6-6-3 调用 QWen 大模型

#### 6-6-3-1 获取调用凭证

调用阿里云通义千问大模型的路径：登录阿里云百炼模型广场 → 选择模型（通义千问 3-Max）→ 查看 API 参考 → 获取 HTTP 请求地址和 API Key。  

#### 6-6-3-2 前端配置 api.js

前端在 src/config/api.js 中配置模型调用的地址、密钥与模型名：  

```javascript
// src/config/api.js
export const apiEndpoint = 'https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions'
export const apiKey = 'sk-9c4d89982a6a4bd3b7494d94751fe81c'
export const model = 'qwen3-max-preview'
```

> 注意：apiKey 是课程演示值，生产环境必须由后端保管，绝不能明文写在浏览器前端代码中，否则会被任意用户窃取盗用。  

#### 6-6-3-3 AI 问答界面

前端提供"首页 / AI 问答 / 我的"三个页面，AI 问答页支持与通义千问对话。  
对话示例：用户提问"我想学习 FastAPI 相关内容"，AI 输出 FastAPI 的定义——基于 Starlette（ASGI 规范）和 Pydantic，性能接近 Node.js 和 Go。  

![AI 问答界面](../../../03%20附件/attachments/知识附件/Python/FastAPI/ch6_ai_chat_ui.png)  

### 6-6-4 本章总结

```vtable
{"rows": [[{"t": "要点", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "Redis 四步", "rs": 1, "cs": 1}, {"t": "安装服务端 → 配置客户端 → 封装缓存操作 → 设计缓存策略", "rs": 1, "cs": 1}], [{"t": "旁路缓存策略", "rs": 1, "cs": 1}, {"t": "读：先查缓存再查库写缓存；写：更新数据库后更新或删除缓存", "rs": 1, "cs": 1}], [{"t": "缓存雪崩预防", "rs": 1, "cs": 1}, {"t": "不同类型数据差异化缓存时长，数据越稳定缓存越久", "rs": 1, "cs": 1}], [{"t": "缓存 Key 设计", "rs": 1, "cs": 1}, {"t": "news:list:分类ID:页码:每页数量，维度完整避免错乱", "rs": 1, "cs": 1}], [{"t": "QWen 调用路径", "rs": 1, "cs": 1}, {"t": "模型广场选模型 → API 参考 → 请求地址 + API Key → 前端配置调用", "rs": 1, "cs": 1}], [{"t": "API Key 安全", "rs": 1, "cs": 1}, {"t": "演示密钥仅用于学习，生产环境必须由后端保管", "rs": 1, "cs": 1}]]}
```


# 7 ORM模板代码

## 7-7 ORM 模板代码

本章汇总项目实战中反复使用的 ORM 模板代码，包括依赖安装、ORM 配置与 News 模型类，可直接复制到项目中按需修改。  

### 7-7-1 安装依赖

```bash
pip install "sqlalchemy[asyncio]"
pip install aiomysql
```

sqlalchemy[asyncio]：SQLAlchemy 异步扩展；aiomysql：MySQL 异步驱动，两者缺一不可。  

### 7-7-2 ORM 配置（config/db_conf.py）

```python
from sqlalchemy.ext.asyncio import create_async_engine, async_sessionmaker, AsyncSession

# 数据库连接地址：驱动 + 用户名:密码 + 主机:端口 + 库名 + 字符集
ASYNC_DATABASE_URL = "mysql+aiomysql://root:123456@localhost:3306/news_app?charset=utf8mb4"

# 创建异步引擎
async_engine = create_async_engine(
    ASYNC_DATABASE_URL,
    echo=True,          # 输出 SQL 日志
    pool_size=10,       # 连接池中保持的持久连接数
    max_overflow=20     # 连接池允许创建的额外连接数
)

# 创建异步会话工厂
AsyncSessionLocal = async_sessionmaker(
    bind=async_engine,
    class_=AsyncSession,
    expire_on_commit=False
)

# 数据库会话依赖：yield 会话，异常回滚，最终关闭
async def get_db():
    async with AsyncSessionLocal() as session:
        try:
            yield session
            await session.commit()
        except Exception:
            await session.rollback()
            raise
        finally:
            await session.close()
```

三个引擎参数说明：  

```vtable
{"rows": [[{"t": "参数", "rs": 1, "cs": 1}, {"t": "默认值", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "echo=True", "rs": 1, "cs": 1}, {"t": "False", "rs": 1, "cs": 1}, {"t": "输出 SQL 日志，便于调试，生产环境建议关闭", "rs": 1, "cs": 1}], [{"t": "pool_size=10", "rs": 1, "cs": 1}, {"t": "5", "rs": 1, "cs": 1}, {"t": "连接池中保持的持久连接数", "rs": 1, "cs": 1}], [{"t": "max_overflow=20", "rs": 1, "cs": 1}, {"t": "10", "rs": 1, "cs": 1}, {"t": "连接池允许创建的额外连接数，超出后排队等待", "rs": 1, "cs": 1}]]}
```

> 注意：ASYC_DATABASE_URL 中的用户名、密码、库名请按本机实际配置修改；charset=utf8mb4 用于完整支持中文与 emoji。  

### 7-7-3 News 模型类（models/news.py）

```python
from datetime import datetime
from typing import Optional

from sqlalchemy import String, Text, DateTime, ForeignKey
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column


class Base(DeclarativeBase):
    """所有模型类的基类"""
    pass


class News(Base):
    """新闻表"""
    __tablename__ = "news"

    id: Mapped[int] = mapped_column(primary_key=True, comment="主键ID")
    title: Mapped[str] = mapped_column(String(255), nullable=False, comment="新闻标题")
    description: Mapped[Optional[str]] = mapped_column(String(500), comment="新闻简介")
    content: Mapped[str] = mapped_column(Text, comment="新闻内容")
    image: Mapped[Optional[str]] = mapped_column(String(255), comment="封面图片")
    author: Mapped[Optional[str]] = mapped_column(String(50), comment="作者")
    category_id: Mapped[int] = mapped_column(ForeignKey("news_category.id"), nullable=False, comment="分类ID")
    views: Mapped[int] = mapped_column(default=0, comment="浏览量")
    publish_time: Mapped[datetime] = mapped_column(DateTime, default=datetime.now, comment="发布时间")

    def __repr__(self):
        return f"<News(id={self.id}, title={self.title})>"
```

字段要点：  

```vtable
{"rows": [[{"t": "字段", "rs": 1, "cs": 1}, {"t": "类型", "rs": 1, "cs": 1}, {"t": "约束/默认", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "id", "rs": 1, "cs": 1}, {"t": "int", "rs": 1, "cs": 1}, {"t": "primary_key=True", "rs": 1, "cs": 1}, {"t": "主键，自增", "rs": 1, "cs": 1}], [{"t": "title", "rs": 1, "cs": 1}, {"t": "String(255)", "rs": 1, "cs": 1}, {"t": "nullable=False", "rs": 1, "cs": 1}, {"t": "新闻标题，必填", "rs": 1, "cs": 1}], [{"t": "description / image / author", "rs": 1, "cs": 1}, {"t": "Optional + String", "rs": 1, "cs": 1}, {"t": "可空", "rs": 1, "cs": 1}, {"t": "可空字段，使用 Optional 泛型标注", "rs": 1, "cs": 1}], [{"t": "content", "rs": 1, "cs": 1}, {"t": "Text", "rs": 1, "cs": 1}, {"t": "可空", "rs": 1, "cs": 1}, {"t": "新闻正文，长文本", "rs": 1, "cs": 1}], [{"t": "category_id", "rs": 1, "cs": 1}, {"t": "ForeignKey(“news_category.id”)", "rs": 1, "cs": 1}, {"t": "nullable=False", "rs": 1, "cs": 1}, {"t": "外键关联新闻分类表", "rs": 1, "cs": 1}], [{"t": "views", "rs": 1, "cs": 1}, {"t": "int", "rs": 1, "cs": 1}, {"t": "default=0", "rs": 1, "cs": 1}, {"t": "浏览量，默认 0", "rs": 1, "cs": 1}], [{"t": "publish_time", "rs": 1, "cs": 1}, {"t": "DateTime", "rs": 1, "cs": 1}, {"t": "default=datetime.now", "rs": 1, "cs": 1}, {"t": "发布时间，默认当前时间", "rs": 1, "cs": 1}]]}
```

> 注意：模型类字段必须与数据库表结构（database.sql）保持一致，否则建表或查询会报错；可空字段的类型注解使用 Optional[str]，对应数据库 NULL。

