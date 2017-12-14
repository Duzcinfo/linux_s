

* 授权

```mysql
grant select,insert,update,delete,create,drop on dbname.* to "username"@"%" indentified by "passwd";
# dbname.* 是dbname所有表 
grant all on  *.* to "username"@"localhost" indentified by "passwd";
flush privileges;

select * from user; # 查看mysql user表里的用户
show grants for username; # 查看用户"username"授的权限
 
```



