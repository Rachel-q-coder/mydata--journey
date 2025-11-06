# 181-Overpass-salary

## 题目描述：

### 表：Employee 
```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| name        | varchar |
| salary      | int     |
| managerId   | int     |
+-------------+---------+
```
- id 是该表的主键（具有唯一值的列）。
- 该表的每一行都表示雇员的ID、姓名、工资和经理的ID。
- 编写解决方案，找出收入比经理高的员工。

## 我的思路：

1. **需求分析：** 只需将员工和其隶属的经理，两人薪资用where进行比较
2. **解题思路：** 目前只有一张表，但是同时需要用到表的薪资。联想到了自连接。这样就可以得到员工的数据和经理的数据。

## SQL代码：

```
select e1.name as Employee
from Employee as e1
left join Employee as e2
on e1.managerId=e2.id 
where e1.salary>e2.salary

```
