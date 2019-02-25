```sql
create database  test_db;  #创建数据库
create user test_db;  # 创建用户
\passwd  test_db    # 设置密码
grant all privileges on database test_db to test_db; # 授权
```

* 给某些权限

```sql
grant select on table tablename to xxx;

##赋予某个表增删改查的权限
grant select,update,delete,insert on table bidding to wu_songgen;
grant select,update,delete,insert on table bidding to liu_tianqi;



grant select,update on table tablename1,tablename2 to xxx;  #可不可以这样？ ##grant的语法只可以对某个表授予权限
```

```sql
/* 创建用户 */
CREATE ROLE rolename;
CREATE USER username WITH PASSWORD '*****';

/* 显示所有用户 */
\du

/* 修改用户权限 */
ALTER ROLE username WITH privileges;
/* 赋给用户表的所有权限 */
GRANT ALL ON tablename TO user; 
/* 赋给用户数据库的所有权限 */
GRANT ALL PRIVILEGES ON DATABASE dbname TO dbuser;

/* 撤销用户权限 */
REVOKE privileges ON tablename FROM user;
```

# 回收数据库

```sql
DROP OWNED BY  deep_learning_goods_name_classification; 
drop  user deep_learning_goods_name_classification;
#删除用户名

REVOKE CONNECT ON DATABASE dbname FROM PUBLIC, username;  # 回收用户数据库的权限
REVOKE delete ON TABLE sc_courtannouncement FROM username;

drop database [数据库名]; #删除数据库
```

## pg建表

```sql
psql -U username -h hostname -p port -d dbname

CREATE TABLE table_name(
   column1 datatype,
   column2 datatype,
   column3 datatype,
   .....
   columnN datatype,
   PRIMARY KEY( one or more columns )
); 
```



