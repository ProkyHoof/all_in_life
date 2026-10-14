---
tags:
  - 知识
类型: 计算机
领域: Python_FastAPI
来源: 黑马程序员FastAPI基础到实战课程（本地PDF课件）
日期: 2026-10-12
关联:
---

# 5 项目实战 - AI 掘金头条（收藏和浏览历史）

## 5.1 收藏模块

收藏模块共五个接口，所有接口都需要用户认证：路由参数声明 user: User = Depends(get_current_user)，未登录时 get_current_user 会抛出 401 异常。  

### 5.1.1 检查收藏状态

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

### 5.1.2 添加收藏

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

### 5.1.3 取消收藏

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

### 5.1.4 获取收藏列表

GET /api/favorite/list?page&pageSize，返回当前用户的收藏新闻列表，包含总量与 hasMore，列表项带收藏时间 favoriteTime。  
实现要点是 ORM 联表查询：select(News).join(Favorite)。  

![我的收藏界面](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch5_favorite_ui.png)  

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

### 5.1.5 清空收藏

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

## 5.2 浏览历史

浏览历史模块共四个接口，同样全部需要用户认证。  

### 5.2.1 添加浏览记录

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

### 5.2.2 获取浏览历史列表

GET /api/history/list?page&pageSize，联表 select(News).join(History) 查询当前用户的浏览记录，列表项带浏览时间 viewTime，同样包含 total 与 hasMore。  

![浏览历史界面](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch5_history_ui.png)  

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

### 5.2.3 删除单条浏览记录

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

### 5.2.4 清空浏览历史

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

## 5.3 收藏 VS 浏览历史

![收藏与浏览历史对比](../../../../03%20附件/attachments/知识附件/Python/2.%20FastAPI/ch5_compare.png)  

```vtable
{"rows": [[{"t": "维度", "rs": 1, "cs": 1}, {"t": "收藏", "rs": 1, "cs": 1}, {"t": "浏览历史", "rs": 1, "cs": 1}], [{"t": "触发方式", "rs": 1, "cs": 1}, {"t": "用户主动点击收藏按钮", "rs": 1, "cs": 1}, {"t": "用户看过新闻即自动记录", "rs": 1, "cs": 1}], [{"t": "去重方式", "rs": 1, "cs": 1}, {"t": "user_id + news_id 唯一约束，重复收藏报错", "rs": 1, "cs": 1}, {"t": "重复浏览只更新浏览时间", "rs": 1, "cs": 1}], [{"t": "时间字段", "rs": 1, "cs": 1}, {"t": "favoriteTime（收藏时间）", "rs": 1, "cs": 1}, {"t": "viewTime（浏览时间）", "rs": 1, "cs": 1}], [{"t": "接口数量", "rs": 1, "cs": 1}, {"t": "5 个（check/add/remove/list/clear）", "rs": 1, "cs": 1}, {"t": "4 个（add/list/delete/clear）", "rs": 1, "cs": 1}], [{"t": "列表实现", "rs": 1, "cs": 1}, {"t": "select(News).join(Favorite) 联表查询", "rs": 1, "cs": 1}, {"t": "select(News).join(History) 联表查询", "rs": 1, "cs": 1}], [{"t": "删除粒度", "rs": 1, "cs": 1}, {"t": "单条 remove + 清空 clear", "rs": 1, "cs": 1}, {"t": "单条 delete/{history_id} + 清空 clear", "rs": 1, "cs": 1}], [{"t": "认证要求", "rs": 1, "cs": 1}, {"t": "全部接口 Depends(get_current_user)", "rs": 1, "cs": 1}, {"t": "全部接口 Depends(get_current_user)", "rs": 1, "cs": 1}]]}
```

## 5.4 本章总结

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
