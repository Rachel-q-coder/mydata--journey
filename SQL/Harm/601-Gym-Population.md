# 601-Gym-Population

## 题目描述：

编写解决方案找出每行的人数大于或等于 100 且 id 连续的三行或更多行记录。

返回按 visit_date 升序排列 的结果表。

### Stadium 表:

```
+------+------------+-----------+
| id   | visit_date | people    |
+------+------------+-----------+
| 1    | 2017-01-01 | 10        |
| 2    | 2017-01-02 | 109       |
| 3    | 2017-01-03 | 150       |
| 4    | 2017-01-04 | 99        |
| 5    | 2017-01-05 | 145       |
| 6    | 2017-01-06 | 1455      |
| 7    | 2017-01-07 | 199       |
| 8    | 2017-01-09 | 188       |
+------+------------+-----------+
```

## 我的思路：

1.**需求分析：** 这是一个连续问题，人数>=100
2.**解题思路：** 一个查询处理人数>=100，一个查询处理id连续：连续n个——等差数列————差值恒定——分组依据。使用cte模块。。

## SQL代码：

```
with t1 as(
    select id,visit_date,people,
    id-row_number()over(order by id ) is_group
    from stadium
    where people>=100
)
,t2 as(
    select is_group
    from t1
    group by is_group
    having count(*)>2
)
select id,visit_date,people
from t1
join t2
on t1.is_group=t2.is_group
order by visit_date 

```

## 总结：

- 连续序列检测：值 - ROW_NUMBER() 技巧

- 窗口函数：ROW_NUMBER() OVER(ORDER BY ...)

- CTE（WITH语句）：模块化复杂查询

- 分组统计：GROUP BY + HAVING