# [knowledge_index](1_all_in_life_index.md)  

``` dataview
TABLE 领域, 来源, 日期
FROM #知识
SORT 领域 DESC, number(split(file.name, "\.")[0]) ASC
```
