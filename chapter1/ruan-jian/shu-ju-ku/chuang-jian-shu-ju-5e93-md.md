```shell
create database  test_db;  #创建数据库
create user test_db;  # 创建用户
\passwd  test_db    # 设置密码
grant all privileges on database test_db to test_db; # 授权
```

* 给某些权限

```shell
grant select on table tablename to xxx;

grant select,update on table tablename1,tablename2 to xxx;  #可不可以这样？ ##grant的语法只可以对某个表授予权限
```



```shell

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



