
# 🧭 我的人生仪表盘

> 最后更新：`= dateformat(date(today), "yyyy-MM-dd")`

## 🗺️ [route](route_index.md)  

```dataview
TABLE 年度, 愿景描述
FROM #路线图
SORT 创建日期 DESC
LIMIT 3
```

## 📚 [最近知识输入](knowledge_index.md)  

``` dataview
TABLE introduction, start_date
FROM #knowledge 
SORT 日期 DESC
LIMIT 5
```

## 🧰 [新增资源](tool_index.md)  

``` dataview
TABLE 分类, 日期
FROM #资源
SORT 日期 DESC
LIMIT 5
```

## 🌱 [生活片段](生活索引.md)  

``` dataview
TABLE 领域, 日期
FROM #生活
SORT 日期 DESC
LIMIT 5
```

## 🚀 [项目进展](project_index.md)  

``` dataview
TABLE 状态, 开始日期, 截止日期, 关联知识
FROM #项目
SORT 状态 ASC, 开始日期 DESC
```




