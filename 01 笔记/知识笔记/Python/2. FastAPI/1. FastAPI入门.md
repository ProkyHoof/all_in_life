---
tags:
  - 知识
类型: 计算机
领域: Python_FastAPI
来源: 黑马程序员FastAPI基础到实战课程（本地PDF课件）
日期: 2026-10-12
关联:
---

# 1 FastAPI 入门

## 1.1 FastAPI 简介

### 1.1.1 什么是 FastAPI

FastAPI 是一个基于 Python 的高性能 Web 框架，用于快速构建 API（Application Programming Interface，应用程序接口）。  
它建立在 Starlette（ASGI 框架）和 Pydantic（数据验证库）之上，凭借原生异步支持与自动生成的交互式文档，成为当前 Python Web 开发中最热门的框架之一。  

> 注意：FastAPI 底层基于 Starlette（ASGI 规范），因此天然支持异步编程；基于 Pydantic，因此拥有强大的类型提示与数据校验能力。  

### 1.1.2 原生异步支持

传统同步接口在遇到耗时操作（如 time.sleep）时会阻塞线程，一个请求必须等前一个请求处理完才能开始；而异步接口可以在等待期间切换去处理其他请求，从而大幅提升并发处理能力。  
下面以"处理 10 次耗时 1 秒的任务"为例，对比同步与异步的耗时差异。  

![同步与异步对比](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch1_sync_async.png)  

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

![同步流程](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch1_sync_flow.png)  

![异步流程](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch1_async_flow.png)  

两种方式的耗时对比：  

```vtable
{"rows": [[{"t": "对比项", "rs": 1, "cs": 1}, {"t": "同步方式", "rs": 1, "cs": 1}, {"t": "异步方式", "rs": 1, "cs": 1}], [{"t": "执行方式", "rs": 1, "cs": 1}, {"t": "串行执行，一个任务完成才执行下一个", "rs": 1, "cs": 1}, {"t": "交错执行，await 等待时让出控制权", "rs": 1, "cs": 1}], [{"t": "总耗时", "rs": 1, "cs": 1}, {"t": "10 个各耗时 1s 的任务共需约 10s", "rs": 1, "cs": 1}, {"t": "10 个任务同时等待，总耗时约 1s", "rs": 1, "cs": 1}], [{"t": "代码形式", "rs": 1, "cs": 1}, {"t": "普通 def + time.sleep", "rs": 1, "cs": 1}, {"t": "async def + await + asyncio.gather 并发调度", "rs": 1, "cs": 1}], [{"t": "适用场景", "rs": 1, "cs": 1}, {"t": "简单脚本、纯 CPU 计算", "rs": 1, "cs": 1}, {"t": "I/O 密集任务（网络请求、文件读写、数据库查询）", "rs": 1, "cs": 1}]]}
```

> 注意：只有耗时操作属于 I/O 密集（网络请求、文件读写、数据库查询等）时，异步才有明显优势；纯 CPU 计算依然会占用事件循环。  

### 1.1.3 FastAPI 的三大优势

```vtable
{"rows": [[{"t": "优势", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}, {"t": "举例", "rs": 1, "cs": 1}], [{"t": "异步性能高", "rs": 1, "cs": 1}, {"t": "基于 ASGI 规范原生支持 async/await，高并发场景性能好", "rs": 1, "cs": 1}, {"t": "10 个 I/O 任务约 1s 完成，性能接近 Node.js 和 Go", "rs": 1, "cs": 1}], [{"t": "开发效率高", "rs": 1, "cs": 1}, {"t": "借助 Pydantic 类型提示与自动校验，减少手动编写校验代码", "rs": 1, "cs": 1}, {"t": "一个函数同时完成参数解析、数据校验与接口文档生成", "rs": 1, "cs": 1}], [{"t": "自动生成交互式文档", "rs": 1, "cs": 1}, {"t": "框架自动生成 /docs 在线接口文档，方便调试与前后端联调", "rs": 1, "cs": 1}, {"t": "浏览器访问 http://127.0.0.1:8000/docs 即可在线调试接口", "rs": 1, "cs": 1}]]}
```

## 1.2 第一个 FastAPI 程序

### 1.2.1 创建项目

使用 PyCharm 创建 FastAPI 项目：New Project → 选择 FastAPI → 虚拟环境选择 Virtualenv → 点击 Create 创建。  
创建完成后，PyCharm 会自动安装 fastapi 与 uvicorn 等依赖。  

![创建项目](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch1_create_project.png)  

### 1.2.2 运行项目

在终端中执行以下命令启动项目：  

```bash
uvicorn main:app --reload
```

其中 main 表示入口文件名（main.py），app 表示 FastAPI 实例名；--reload 表示代码变更后自动重启服务，开发阶段非常方便。  

### 1.2.3 访问项目

服务启动后，浏览器访问：  

```text
http://127.0.0.1:8000
```

即可看到默认路由返回的内容；访问 http://127.0.0.1:8000/docs 可以打开 FastAPI 自动生成的交互式 API 文档，在页面上直接测试各个接口。  

![访问项目](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch1_access_project.png)  

### 1.2.4 虚拟环境的作用

虚拟环境用于隔离不同项目之间的依赖，避免包版本冲突。  
例如项目 A 需要 fastapi 0.100，项目 B 需要 fastapi 0.115，如果安装在同一环境会互相覆盖；使用虚拟环境后各项目依赖相互独立，互不影响。  

## 1.3 路由

### 1.3.1 什么是路由

路由是 URL 地址和处理函数之间的映射关系：当客户端访问某个 URL 时，框架根据路由找到对应的处理函数并执行。  

### 1.3.2 路由的定义

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

### 1.3.3 路由练习

需求：访问路径 /user/hello，响应结果为 {"msg": "我正在学习 FastAPI ......"}。  
参考实现：  

```python
@app.get("/user/hello")
async def user_hello():
    return {"msg": "我正在学习 FastAPI ......"}
```

## 1.4 参数

### 1.4.1 参数的作用

参数就是客户端发送请求时附带的额外信息和指令。  
参数的作用是让同一个接口能根据不同的输入，返回不同的输出，实现动态交互。例如访问 /book 时传入 book_id=1 返回图书 1 的信息，传入 book_id=2 返回图书 2 的信息。  

### 1.4.2 参数分类

HTTP 请求中的参数按位置与用途分为三类：路径参数、查询参数、请求体。  

![参数分类](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch1_param_types.png)  

```vtable
{"rows": [[{"t": "类型", "rs": 1, "cs": 1}, {"t": "位置", "rs": 1, "cs": 1}, {"t": "作用", "rs": 1, "cs": 1}, {"t": "方法", "rs": 1, "cs": 1}, {"t": "语法示例", "rs": 1, "cs": 1}], [{"t": "路径参数", "rs": 1, "cs": 1}, {"t": "URL 路径的一部分，如 /book/{id}", "rs": 1, "cs": 1}, {"t": "指向唯一的、特定的资源", "rs": 1, "cs": 1}, {"t": "GET", "rs": 1, "cs": 1}, {"t": "@app.get(“/book/{id}”)，访问 /book/1", "rs": 1, "cs": 1}], [{"t": "查询参数", "rs": 1, "cs": 1}, {"t": "URL? 之后，如 k1=v1&k2=v2", "rs": 1, "cs": 1}, {"t": "对资源集合进行过滤、排序、分页等操作", "rs": 1, "cs": 1}, {"t": "GET", "rs": 1, "cs": 1}, {"t": "/book?page=1&pageSize=10", "rs": 1, "cs": 1}], [{"t": "请求体", "rs": 1, "cs": 1}, {"t": "HTTP 请求的消息体（body）中", "rs": 1, "cs": 1}, {"t": "创建、更新资源，携带大量数据如 JSON", "rs": 1, "cs": 1}, {"t": "POST、PUT 等", "rs": 1, "cs": 1}, {"t": "请求体 {“title”: “标题”, “content”: “正文”}", "rs": 1, "cs": 1}]]}
```

### 1.4.3 路径参数

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

### 1.4.4 查询参数

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

### 1.4.5 请求体参数

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

## 1.5 请求与响应

### 1.5.1 请求与响应模型

Web 开发中，客户端（浏览器、App 等）向服务器发送 Request（请求），服务器处理后返回 Response（响应），一次完整的交互即"请求-响应"模型。  
FastAPI 默认会自动将路径操作函数返回的 Python 对象（字典、列表、Pydantic 模型等），经由 jsonable_encoder 转换为 JSON 兼容格式，并包装为 JSONResponse 返回，省去了手动序列化的步骤。  

### 1.5.2 FastAPI 内置响应类型

如果需要返回非 JSON 数据（如 HTML、文件流），FastAPI 提供了丰富的响应类型：  

```vtable
{"rows": [[{"t": "响应类型", "rs": 1, "cs": 1}, {"t": "用途", "rs": 1, "cs": 1}, {"t": "示例", "rs": 1, "cs": 1}, {"t": "导入", "rs": 1, "cs": 1}], [{"t": "JSONResponse", "rs": 1, "cs": 1}, {"t": "默认响应，返回 JSON 数据", "rs": 1, "cs": 1}, {"t": "return {“key”: “value”}", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import JSONResponse", "rs": 1, "cs": 1}], [{"t": "HTMLResponse", "rs": 1, "cs": 1}, {"t": "返回 HTML 内容", "rs": 1, "cs": 1}, {"t": "return HTMLResponse(html_content)", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import HTMLResponse", "rs": 1, "cs": 1}], [{"t": "PlainTextResponse", "rs": 1, "cs": 1}, {"t": "返回纯文本", "rs": 1, "cs": 1}, {"t": "return PlainTextResponse(“text”)", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import PlainTextResponse", "rs": 1, "cs": 1}], [{"t": "FileResponse", "rs": 1, "cs": 1}, {"t": "返回文件下载", "rs": 1, "cs": 1}, {"t": "return FileResponse(path)", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import FileResponse", "rs": 1, "cs": 1}], [{"t": "StreamingResponse", "rs": 1, "cs": 1}, {"t": "流式响应，边生成边返回", "rs": 1, "cs": 1}, {"t": "生成器函数逐段返回数据", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import StreamingResponse", "rs": 1, "cs": 1}], [{"t": "RedirectResponse", "rs": 1, "cs": 1}, {"t": "重定向", "rs": 1, "cs": 1}, {"t": "return RedirectResponse(url)", "rs": 1, "cs": 1}, {"t": "from fastapi.responses import RedirectResponse", "rs": 1, "cs": 1}]]}
```

### 1.5.3 响应类型设置方式

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

### 1.5.4 自定义响应数据格式

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

### 1.5.5 异常处理

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
