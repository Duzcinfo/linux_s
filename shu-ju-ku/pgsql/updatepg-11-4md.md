# update\_pg\_11.4.md

```sql
 psql test_db -c'CREATE EXTENSION pg_pathman' ;
```

```text
安装扩展（源码安装）

systermctl stop postgresql
$cd /path/to/src/postgresql-11/contrib/pg_trgm
$make
$sudo make install # or su -c 'make install' if you don't use sudo


systermctl start postgresql

# 然后先管理员创建这人扩展，否则普通用户报权限错误，
然后再在普通用户执行
>psql
CREATE EXTENSION pg_trgm;

psql test_db -c'CREATE EXTENSION pg_trgm' ;
```



