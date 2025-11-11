# 196-Delete-repeat

## 题目描述：

编写解决方案 删除 所有重复的电子邮件，只保留一个具有最小 id 的唯一电子邮件。

（对于 SQL 用户，请注意你应该编写一个 DELETE 语句而不是 SELECT 语句。）

（对于 Pandas 用户，请注意你应该直接修改 Person 表。）

运行脚本后，显示的答案是 Person 表。驱动程序将首先编译并运行您的代码片段，然后再显示 Person 表。Person 表的最终顺序 无关紧要 。

### Person 表:
```
+----+------------------+
| id | email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
```

## 我的思路：

1.**需求分析：** 删除，则应该选择delete，而不是查询。

1.**解题思路：** 因为是删除，那就把最小id的选出来，再把id不在最小里的选出来，就是要删掉得。涉及到 not in

##sql代码

```
Delete from Person 
where id not in(
    select id
    from(
    select min(id) as id
    from Person
    group by email
) as temp
)
```