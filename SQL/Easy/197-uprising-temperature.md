# 197-uprising-temperature

## 题目描述：

编写解决方案，找出与之前（昨天的）日期相比温度更高的所有日期的 id 。

返回结果 无顺序要求 。

### Weather 表：

```
+----+------------+-------------+
| id | recordDate | Temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+
```

## 我的思路：

1.**需求分析：** 今天比昨天温度高，要对每一行进行判断
2.**解题思路：** 因为要对一张表两天的温度进行比较，使用自连接，共同对象便是日期，涉及日期，使用date_add,即可将表关联上，再一个简单where判断。

## SQL代码：

```
select today.id
from Weather yesterday
left join Weather today on today.recordDate=date_add(yesterday.recordDate,interval 1 day)
where today.Temperature>yesterday.Temperature;
```

## 总结：

-涉及日期。date_add(a,interval x day/month/year)
