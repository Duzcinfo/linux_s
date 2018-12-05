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
  create user 'duzc'@'%' identified by 'duzhichuan'; #这个账户可以在任何主机登陆，这里可以限制登陆的ip。授权那里也可以做此限制
```

* 授权

```mysql
    grant select,insert,update,delete,create,drop on dbname.* to "username"@"%" identified by "passwd";
    # dbname.* 是dbname所有表 
    grant all on  *.* to "username"@"localhost" identified by "passwd";
    flush privileges;

    select * from user; # 查看mysql user表里的用户
    show grants for username; # 查看用户"username"授的权限
```

* 取消授权

  ```mysql
  revoke all on *.* from  'root'@'%' ;
  revoke all on *.* from dba@localhost;
  ```

* 数据类型

* 创建表

```mysql
mysql> create table student(
    -> id int auto_increment,
    -> name char(32) not null,
    -> age int not null,
    -> register_date date not null,
    -> primary key (id));
Query OK, 0 rows affected (1.08 sec)
```

* 插入数据

```mysql
insert into student (name,age,register_date) values ("duzc","23","2017-12-2");

/* 查看
select * from student
select name from student where age="23"
```

* 排序

```mysql
mysql> select * from student order by id desc;
+----+---------+-----+---------------+
| id | name    | age | register_date |
+----+---------+-----+---------------+
|  3 | 子川    |  26 | 2017-12-15    |
|  2 | wild_du |  25 | 2017-12-14    |
|  1 | duzc    |  23 | 2017-12-02    |
+----+---------+-----+---------------+
3 rows in set (0.00 sec)

mysql> select * from student order by id asc;
+----+---------+-----+---------------+
| id | name    | age | register_date |
+----+---------+-----+---------------+
|  1 | duzc    |  23 | 2017-12-02    |
|  2 | wild_du |  25 | 2017-12-14    |
|  3 | 子川    |  26 | 2017-12-15    |
+----+---------+-----+---------------+
```

* 事务  
  innodb

  * begin
  * rollback
  * commit

* 索引  
    主键只有一个,索引可以有多个.索引\(hash\)

  ```mysql
    create index indexname on tablename(zidaun(length));
    alter tablename add index [indexname] on (ziduan(length));
    #删除索引
    drop index indexname on tablename;
  ```

# mysql8.0

* 创建数据库

```shell
create database zabbix;
create user 'zabix'@'%' identified by 'zabbix';
grant all privileges on zabbix.* to 'zabbix'@'%';
```

* 授权

MySQL8.0取消了直接grant创建用户的语法，只能先create user再grant，因此创建root如下：

```shell
mysql> SELECT User, Host FROM mysql.user;
+------------------+-----------+
| User             | Host      |
+------------------+-----------+
| dzc              | %         |
| zabbix           | %         |
| duzc             | localhost |
| mysql.infoschema | localhost |
| mysql.session    | localhost |
| mysql.sys        | localhost |
| root             | localhost |
| zabbix           | localhost |
+------------------+-----------+
8 rows in set (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON duzc_qcd.* TO'duzc'@'192.168.0.106';
ERROR 1410 (42000): You are not allowed to create a user with GRANT
##为什么加入这句话是错误的？

mysql> GRANT ALL PRIVILEGES ON duzc_qcd.* TO'duzc'@'localhost';
Query OK, 0 rows affected (0.15 sec)
```

官网的列子：

```shell

mysql> CREATE USER 'custom'@'localhost' IDENTIFIED BY 'password';
mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP
    ->     ON bankaccount.*
    ->     TO 'custom'@'localhost';
mysql> CREATE USER 'custom'@'host47.example.com' IDENTIFIED BY 'password';
mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP
    ->     ON expenses.*
    ->     TO 'custom'@'host47.example.com';
mysql> CREATE USER 'custom'@'%.example.com' IDENTIFIED BY 'password';
mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP
    ->     ON customer.*
    ->     TO 'custom'@'%.example.com';
```





用 navicat 连接出错：

```shell
    2059 -Authentication plugin 'cacing_sh2_password' cannot be loaded
```





