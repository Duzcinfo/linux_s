# 基本操作.md

## [https://blog.csdn.net/qq\_31156277/article/details/88821654](https://blog.csdn.net/qq_31156277/article/details/88821654)

## 膨胀表处理方法：[https://www.cnblogs.com/easonbook/p/10945265.html](https://www.cnblogs.com/easonbook/p/10945265.html)

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

## 查看数据库的大小，表的大小，索引的大小

```sql
以KB，MB，GB的方式来查看数据库大小
select pg_size_pretty(pg_database_size('xx_prod'));
```

### 查看所有数据库的大小

```sql
select pg_database.datname, pg_database_size(pg_database.datname) AS size from pg_database;   

```

#### 统计各数据库占用磁盘大小

```sql
 SELECT d.datname AS Name,  pg_catalog.pg_get_userbyid(d.datdba) AS Owner,  
   CASE WHEN pg_catalog.has_database_privilege(d.datname, 'CONNECT')  
       THEN pg_catalog.pg_size_pretty(pg_catalog.pg_database_size(d.datname))  
       ELSE 'No Access'  
   END AS SIZE  
ROM pg_catalog.pg_database d  
   ORDER BY  
   CASE WHEN pg_catalog.has_database_privilege(d.datname, 'CONNECT')  
       THEN pg_catalog.pg_database_size(d.datname)  
       ELSE NULL  
   END DESC -- nulls first  
   LIMIT 20
```

### 查看单表

```sql
\d  tables_name;   # 相当于mysql desc table_name;

查看表大小
   select pg_relation_size('tables_name');
   select pg_size_pretty(pg_relation_size('tables_name'));

```

#### 统计数据库中各表占用磁盘大小

```sql
SELECT  
    table_schema || '.' || table_name AS table_full_name,  
    pg_size_pretty(pg_total_relation_size('"' || table_schema || '"."' || table_name || '"')) AS size  
FROM information_schema.tables  
ORDER BY  
    pg_total_relation_size('"' || table_schema || '"."' || table_name || '"') DESC  

```

### 查看索引

```sql
   \di    # 相当于mysql show index from test; 

   查看表的总大小，包括索引大小
   
   select pg_size_pretty(pg_total_relation_size('test')); 
```

