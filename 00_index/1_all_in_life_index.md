
# 🧭 我的人生仪表盘

> 最后更新：`= dateformat(date(today), "yyyy-MM-dd")`

## 🗺️ [route](route_index.md)  

```dataview
TABLE 年度, 愿景描述
FROM #路线图
SORT 创建日期 DESC
LIMIT 3
```

## 📚 [knowledge](knowledge_index.md)  

``` dataview
TABLE introduction, start_date
FROM #knowledge 
SORT 日期 DESC
LIMIT 5
```

## 🧰 [tool](tool_index.md)  

``` dataview
TABLE 分类, 日期
FROM #资源
SORT 日期 DESC
LIMIT 5
```

## 🚀 [project](project_index.md)  

``` dataview
TABLE 状态, 开始日期, 截止日期, 关联知识
FROM #项目
SORT 状态 ASC, 开始日期 DESC
```




