# 585-2016-investation

## 题目描述：

编写解决方案报告 2016 年 (tiv_2016) 所有满足下述条件的投保人的投保金额之和：

他在 2015 年的投保额 (tiv_2015) 至少跟一个其他投保人在 2015 年的投保额相同。
他所在的城市必须与其他投保人都不同（也就是说 (lat, lon) 不能跟其他任何一个投保人完全相同）。
tiv_2016 四舍五入的 两位小数 。

### Insurance 表：

```
+-----+----------+----------+-----+-----+
| pid | tiv_2015 | tiv_2016 | lat | lon |
+-----+----------+----------+-----+-----+
| 1   | 10       | 5        | 10  | 10  |
| 2   | 20       | 20       | 20  | 20  |
| 3   | 10       | 30       | 20  | 20  |
| 4   | 10       | 40       | 40  | 40  |
+-----+----------+----------+-----+-----+
```

## 我的思路：

1.**需求分析：** 2015投保至少有相同的数值存在；地方得不一样
1.**解题思路：** 使用count，对需求的条件，计数。

## SQL代码:

# Write your MySQL query statement below
select round(sum(tiv_2016),2) as tiv_2016
from (
    select tiv_2016,
    count(*)over(partition by tiv_2015) as same_2015,
    count(*)over(partition by lat,lon) as same_lat
    from insurance
)as i1 
where same_2015>1
and same_lat=1;

## 总结：

-对于问题有关于存在数量情况，可以使用count，把计数情况单独做出一列，后续用where，筛选所需条件。