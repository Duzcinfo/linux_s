```shell
create database  test_db;  #创建数据库
create user test_db;  # 创建用户
\passwd  test_db    # 设置密码
grant all privileges on database test_db to test_db; # 授权
```



* 给某些权限

```shell
grant select on table tablename to xxx;
```



