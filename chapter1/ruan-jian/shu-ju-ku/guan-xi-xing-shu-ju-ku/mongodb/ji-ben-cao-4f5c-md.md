---
title: mongodb 基本操作
---

# 连接

```shell
mongo
```

# 查询

```shell
#查看数据库
> show dbs
admin  0.078GB
dzc    0.078GB
local  0.078GB
```

```shell
# 进入数据库
use local

# 查看数据库的表
db.getCollectionNames()
[ "startup_log", "system.indexes" ]

# 按条件查找内容
db.startup_log.count()

```



