# 602-Who-has-mostfriend

## 题目介绍：

编写解决方案，找出拥有最多的好友的人和他拥有的好友数目。

生成的测试用例保证拥有最多好友数目的只有 1 个人。

### RequestAccepted 表：

```
+--------------+-------------+-------------+
| requester_id | accepter_id | accept_date |
+--------------+-------------+-------------+
| 1            | 2           | 2016/06/03  |
| 1            | 3           | 2016/06/08  |
| 2            | 3           | 2016/06/08  |
| 3            | 4           | 2016/06/09  |
+--------------+-------------+-------------+
```

## 我的思路：

1.**需求分析：** 一个人发信息给别人的人数和他收到信息的次数
2.**解题思路：** 将收到和发送信息的id合并，再根据id分组，统计次数。

## SQL代码：

```
select id,count(*) as num
from(
    select requester_id as id from requestaccepted
    union all
    select accepter_id as id from requestaccepted
)as f1
group by id
order by num desc
limit 1;
```

## 总结：

1. 使用UNION ALL当：

- 需要保留所有记录（包括重复）

- 进行数量统计

- 性能要求高

2. 使用UNION当：

- 需要去重，获取唯一值

- 业务逻辑要求不重复