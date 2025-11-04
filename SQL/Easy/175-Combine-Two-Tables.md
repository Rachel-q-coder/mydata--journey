# 175.组合两个表


**难度：** 简单
**标签：** 数据库

## 题目描述:

报告 Person 表中每个人的姓、名、城市和州。如果 personId 的地址不在 Address 表中，则报告为 null 。

Person表:
+-----------+----------+----------+
| personID | lastName | firstName |
| -------- | -------- | --------- |
| 1        | Wang     | Allen     |
| 2        | Alice    | Bob       |
+-----------+----------+----------+
Address表:
+-----------+----------+---------------+------------+
| addressId | personId | city          | state      |
+-----------+----------+---------------+------------+
| 1         | 2        | New York City | New York   |
| 2         | 3        | Leetcode      | California |
+-----------+----------+---------------+------------+

## 我的思路：

1.题目要求表明了personid必须都呈现，所以应该选择person为主表
2.使用left join，通过相同的条件——personid，将两表连接

## SQL代码：

```sql
select firstName,lastName,city,state
from Person as P
left join Address as A on P.personID = A.personID




