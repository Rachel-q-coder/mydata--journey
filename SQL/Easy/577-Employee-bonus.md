# 577-Employee-bonus

## 题目描述：

编写解决方案，报告每个奖金 少于 1000 的员工的姓名和奖金数额。

### Employee table:

```
+-------+--------+------------+--------+
| empId | name   | supervisor | salary |
+-------+--------+------------+--------+
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |
+-------+--------+------------+--------+
```

### Bonus table:
```
+-------+-------+
| empId | bonus |
+-------+-------+
| 2     | 500   |
| 4     | 2000  |
+-------+-------+
```

## SQL代码：

# Write your MySQL query statement below
select name,bonus
from employee
left join bonus on employee.empId=bonus.empId
where coalesce(bonus,0)<1000;

## 总结

- where语句只返回true值，不会返回null值

- 想让null显示出来：
  
1. 用 is null：SELECT * FROM table 
WHERE value < 1000 OR value IS NULL;

1. SELECT * FROM table 
WHERE COALESCE(value, 0) < 1000;

-- 把NULL当作0来处理

- coalesce(expression,value1,value2)