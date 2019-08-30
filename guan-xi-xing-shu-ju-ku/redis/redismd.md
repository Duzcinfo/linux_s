# redis.md

## title: redis

连接 `redis-cli -h host -p 6379`

查询日志

```text
select 0 # 选择库 0-15
keys * # 查看说有的key
DBSIZE #返回当前库的数量

flushall #清空是数据
```

