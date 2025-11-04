# 176.第二高的薪水

**难度：** 中级

## 题目描述：

查询并返回 Employee 表中第二高的 不同 薪水 。如果不存在第二高的薪水，查询应该返回 null(Pandas 则返回 None) 。

Employee 表：
```
+----+--------+
| id | salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

Employee 表：
```
+----+--------+
| id | salary |
+----+--------+
| 1  | 100    |
+----+--------+
```

## 我的思路

1.**需求分析：** 是要返回第二高的，查询不到会有 ***null*** 出现

2.**解体思路：** 看到第二，我第一反应是rank函数，再通过子循环得到

## rank方法

```sql
select
(select salary 
from (
    select salary,dense_rank()over(order by salary desc) as rk
    from Employee
) as fr
where rk=2
limit 1
) as SecondHighestSalary
```

## 其他解法

1.在看到最大，最小以及它们周围的数据时，可以采用max，min函数。

### max

```
select max(salary) as SecondHighestSalary
from employee
where salary<(select max(salary) from employee)
```

2.官方：offset与limit合用：limit 1 offset 1//跳过第一行，只取一行

### offset

```
select
(select distinct salary 
from employee
order by salary desc
limit 1 offset 1)
as SecondHighestSalary;
```

### 总结

-当未查询到任何东西，返回空集合；

-若在一个空集合，未查询到任何东西，则返回null

-所以方一和方三外部都需再嵌套一个select