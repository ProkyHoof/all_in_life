---
tags:
  - 知识
类型: 计算机
领域: Python_FastAPI
来源: 黑马程序员FastAPI基础到实战课程（本地PDF课件）
日期: 2026-10-12
关联:
---

# 6 项目实战 - AI 掘金头条（缓存与模型调用）

## 6.1 缓存

### 6.1.1 什么是缓存

缓存是一种高速临时数据存储机制：临时存储数据或计算结果，避免重复耗时获取。  
在项目中的作用：提升性能、降低延迟；减轻服务器和数据库负载；降低网络延迟；节省资源成本。  

### 6.1.2 缓存架构

![缓存架构](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_cache_arch.png)  

用户/前端 → FastAPI 服务器（业务逻辑控制中心）→ 高速临时数据（取的快）+ 数据库（权威真实数据，存得住）。  
缓存负责快速读取，数据库负责数据持久化，两者配合各取所长。  

### 6.1.3 项目中的缓存流程

![项目中的缓存流程](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_cache_flow.png)  

前端请求数据 → 服务器先查缓存 → 有缓存则直接返回数据；无缓存则查询数据库 → 将数据写入缓存 → 再返回给前端。  

## 6.2 Redis

### 6.2.1 Redis 是什么

Redis 是一种高性能的 Key-Value 存储系统，它将数据存储在内存中，因此读写速度极快，非常适合作为应用层的缓存服务。  
在 FastAPI 这样的后端框架中，通常在应用层使用像 Redis 这样的内存数据存储作为缓存，默认端口号为 6379。  

![Redis 四步总览](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_redis_steps.png)  

使用 Redis 做缓存分四步：安装 Redis 服务端 → 配置 Redis 客户端 → 封装缓存操作 → 设计缓存策略。  

### 6.2.2 安装 Redis 服务端

![安装 Redis 服务端](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_redis_install.png)  

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

### 6.2.3 配置 Redis 客户端

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

![配置 Redis 客户端](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_redis_client.png)  

配置参数说明：  

```vtable
{"rows": [[{"t": "参数", "rs": 1, "cs": 1}, {"t": "默认值", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "host", "rs": 1, "cs": 1}, {"t": "127.0.0.1", "rs": 1, "cs": 1}, {"t": "Redis 服务器地址，本机开发用 localhost", "rs": 1, "cs": 1}], [{"t": "port", "rs": 1, "cs": 1}, {"t": "6379", "rs": 1, "cs": 1}, {"t": "Redis 默认端口号", "rs": 1, "cs": 1}], [{"t": "db", "rs": 1, "cs": 1}, {"t": "0", "rs": 1, "cs": 1}, {"t": "数据库编号（0~15），不同业务可隔离", "rs": 1, "cs": 1}], [{"t": "decode_responses", "rs": 1, "cs": 1}, {"t": "False", "rs": 1, "cs": 1}, {"t": "True 时 get 直接返回字符串，否则返回 bytes 需手动 decode", "rs": 1, "cs": 1}]]}
```

> 注意：decode_responses=True 时 get 直接返回字符串，否则返回 bytes 字节流，需要手动 decode。  

### 6.2.4 封装缓存操作

缓存操作就是围绕 Redis 做"存、取、删、判断、过期"等操作，让数据访问更快、数据库压力更小。  
Redis 存储数据的形式：key - value。  

![封装缓存操作](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_cache_ops.png)  

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

### 6.2.5 设计缓存策略（旁路缓存 Cache-Aside）

最常见的缓存策略是旁路缓存（Cache-Aside）：  

```vtable
{"rows": [[{"t": "方向", "rs": 1, "cs": 1}, {"t": "流程", "rs": 1, "cs": 1}, {"t": "关键点", "rs": 1, "cs": 1}], [{"t": "读", "rs": 1, "cs": 1}, {"t": "先查缓存 → 命中直接返回；未命中 → 查数据库 → 写缓存 → 返回", "rs": 1, "cs": 1}, {"t": "未命中时先写缓存再返回，并设置过期时间 TTL", "rs": 1, "cs": 1}], [{"t": "写", "rs": 1, "cs": 1}, {"t": "更新数据库后，更新缓存或删除缓存", "rs": 1, "cs": 1}, {"t": "优先删除缓存，下次读取时重建，避免写脏数据", "rs": 1, "cs": 1}]]}
```

![缓存策略](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_cache_strategy.png)  

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

![缓存时长设计](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_cache_ttl.png)  

```vtable
{"rows": [[{"t": "类型", "rs": 1, "cs": 1}, {"t": "时间", "rs": 1, "cs": 1}, {"t": "Key 示例", "rs": 1, "cs": 1}], [{"t": "分类、配置", "rs": 1, "cs": 1}, {"t": "7200（2小时）", "rs": 1, "cs": 1}, {"t": "news:category:list", "rs": 1, "cs": 1}], [{"t": "列表数据", "rs": 1, "cs": 1}, {"t": "600（10分钟）", "rs": 1, "cs": 1}, {"t": "news:list:1:1:10", "rs": 1, "cs": 1}], [{"t": "详情数据", "rs": 1, "cs": 1}, {"t": "1800（30分钟）", "rs": 1, "cs": 1}, {"t": "news:detail:101", "rs": 1, "cs": 1}], [{"t": "验证码", "rs": 1, "cs": 1}, {"t": "120（2分钟）", "rs": 1, "cs": 1}, {"t": "sms:code:13800001111", "rs": 1, "cs": 1}]]}
```

新闻列表的缓存 Key 设计：news:list:分类ID:页码:每页数量，Value 为新闻列表数据。  

> 注意：缓存 Key 必须包含查询的关键维度（分类、页码、每页数量），否则不同条件会命中同一份错误数据。  

## 6.3 调用 QWen 大模型

### 6.3.1 获取调用凭证

调用阿里云通义千问大模型的路径：登录阿里云百炼模型广场 → 选择模型（通义千问 3-Max）→ 查看 API 参考 → 获取 HTTP 请求地址和 API Key。  

### 6.3.2 前端配置 api.js

前端在 src/config/api.js 中配置模型调用的地址、密钥与模型名：  

```javascript
// src/config/api.js
export const apiEndpoint = 'https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions'
export const apiKey = 'sk-9c4d89982a6a4bd3b7494d94751fe81c'
export const model = 'qwen3-max-preview'
```

> 注意：apiKey 是课程演示值，生产环境必须由后端保管，绝不能明文写在浏览器前端代码中，否则会被任意用户窃取盗用。  

### 6.3.3 AI 问答界面

前端提供"首页 / AI 问答 / 我的"三个页面，AI 问答页支持与通义千问对话。  
对话示例：用户提问"我想学习 FastAPI 相关内容"，AI 输出 FastAPI 的定义——基于 Starlette（ASGI 规范）和 Pydantic，性能接近 Node.js 和 Go。  

![AI 问答界面](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch6_ai_chat_ui.png)  

## 6.4 本章总结

```vtable
{"rows": [[{"t": "要点", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "Redis 四步", "rs": 1, "cs": 1}, {"t": "安装服务端 → 配置客户端 → 封装缓存操作 → 设计缓存策略", "rs": 1, "cs": 1}], [{"t": "旁路缓存策略", "rs": 1, "cs": 1}, {"t": "读：先查缓存再查库写缓存；写：更新数据库后更新或删除缓存", "rs": 1, "cs": 1}], [{"t": "缓存雪崩预防", "rs": 1, "cs": 1}, {"t": "不同类型数据差异化缓存时长，数据越稳定缓存越久", "rs": 1, "cs": 1}], [{"t": "缓存 Key 设计", "rs": 1, "cs": 1}, {"t": "news:list:分类ID:页码:每页数量，维度完整避免错乱", "rs": 1, "cs": 1}], [{"t": "QWen 调用路径", "rs": 1, "cs": 1}, {"t": "模型广场选模型 → API 参考 → 请求地址 + API Key → 前端配置调用", "rs": 1, "cs": 1}], [{"t": "API Key 安全", "rs": 1, "cs": 1}, {"t": "演示密钥仅用于学习，生产环境必须由后端保管", "rs": 1, "cs": 1}]]}
```
