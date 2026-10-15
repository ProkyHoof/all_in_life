# [project_index](1_all_in_life_index.md)  

``` dataview
TABLE introduction, start_date
FROM #project
WHERE introduction != "项目"
SORT start_date DESC
```
