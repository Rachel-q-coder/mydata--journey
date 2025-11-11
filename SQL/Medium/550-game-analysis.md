# 550-game-analysis

## 题目分析：

编写解决方案，报告在首次登录的第二天再次登录的玩家的 比率，四舍五入到小数点后两位。换句话说，你需要计算从首次登录后的第二天登录的玩家数量，并将其除以总玩家数。

### Activity table:
```
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |
+-----------+-----------+------------+--------------+
```

## 我的思路：

1.**需求分析：** 题目要求的是比率，且规定了比率值的格式，使用round标准化结果。且是第二天玩的，那得先查到第一天玩的时间。

2.**解题思路：** 先找出玩家第一天登录的时间，自连接一个新表用于排查出对应第二天登录时间是否存在。使用avg（event_date is not null）。来对标比率

### SQL代码

```
select round(avg(a2.event_date is not null),2) as fraction
from(
    select player_id,min(event_date) as event_date
    from activity
    group by player_id
)as a1
left join activity a2 on
a1.player_id=a2.player_id
and datediff(a2.event_date,a1.event_date)=1
```

## 我的总结：

-可以在连接时用on也能筛选不需要的东西。这里就不用where来判断第二天的时间有没有存在。直接on出能对应得上时间