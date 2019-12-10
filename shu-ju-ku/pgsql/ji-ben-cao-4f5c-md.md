# 基本操作.md

## [https://blog.csdn.net/qq\_31156277/article/details/88821654](https://blog.csdn.net/qq_31156277/article/details/88821654)

## 远程登陆 pg 数据库

```sql
psql -U username -h hostname -p port -d dbname
```

## 备份数据

```sql
pg_dump  -U name -d ccip_prod --no-owner -f  /tmp/ccip_prod_20181121.sql    #--no-owner参数的意思是不备份数据库owner
#备份单表
pg_dump -U hotel_loan_dev  -d hotel_loan_dev  -t  hotel_ruzhulv_bak  --no-owner -h 192.168.31.157  -f  /home/dell/hotel_pg_data/157_hotel_loan_dev/hotel_ruzhulv_bak_bak
```

## 数据库的恢复

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

[pg 参考](https://emacsist.github.io/2016/01/22/postgresql备份pg_dump与恢复pg_restore/)

* 更改数据库时区

```sql
ALTER DATABASE gd_data_test SET timezone TO 'Asia/Chongqing';
```

