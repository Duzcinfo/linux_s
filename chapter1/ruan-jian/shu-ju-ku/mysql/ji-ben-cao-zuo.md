* 创建数据库

```mysql
create database zabbix character set utf8 collate utf8_general_ci;
show create database zabbix;
#显示内容
mysql> show create database zabbix;
+----------+-----------------------------------------------------------------+
| Database | Create Database                                                 |
+----------+-----------------------------------------------------------------+
| zabbix   | CREATE DATABASE `zabbix` /*!40100 DEFAULT CHARACTER SET utf8 */ |
+----------+-----------------------------------------------------------------+
1 row in set (0.00 sec)
```
* 创建用户
```mysql
create user 'duzc' identified by 'duzhichuan';

```
* 授权

```mysql
grant select,insert,update,delete,create,drop on dbname.* to "username"@"%" indentified by "passwd";
# dbname.* 是dbname所有表 
grant all on  *.* to "username"@"localhost" identified by "passwd";
flush privileges;

select * from user; # 查看mysql user表里的用户
show grants for username; # 查看用户"username"授的权限
```

* 数据类型



