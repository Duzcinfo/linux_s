
---

# 远程登陆 pg 数据库

```sql
psql -U username -h hostname -p port -d dbname
```

# 备份数据

```sql
pg_dump  -d ccip_prod --no-owner -f  /tmp/ccip_prod_20181121.sql    #--no-owner参数的意思是不备份数据库owner
```

# 数据库的恢复

* 创建数据库

```sql
create database ccip_
psql -d ccip_pre -U postgres -f /tmp/ccip_prod_20181121.sql

create user ccip_pre;
\passwd ccip_pre

grant all privileges on database ccip_pre to ccip_pre;
```

```sql
psql  -U  username   -d  dbname -h hostname  -f zch_20181128.sql
```

* 问题

连接数据库并不能直接访问数据，原因是备份恢复的数据库onwer为postgres用户。

```sql
psql
\c ccip_pre     #登入数据库
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO ccip_pre;
```

```sql
psql:zch_20181128.sql:45: ERROR:  role "yuan" does not exist
#因为导数据的时候，没有加 --no-owner 选项。但这个结果不影响使用。
```



[pg 参考](https://emacsist.github.io/2016/01/22/postgresql%E5%A4%87%E4%BB%BDpg_dump%E4%B8%8E%E6%81%A2%E5%A4%8Dpg_restore/)



