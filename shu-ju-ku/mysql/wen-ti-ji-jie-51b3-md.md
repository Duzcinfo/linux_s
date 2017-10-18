# mysqldump

* 问题描述
  在linux命令行数据库备份时，报`Out of resources when opening file`错误。

```shell
 mysqldump -uroot -ppasswd --databases dbname  > /tmp/20171018_xy.sql                    
mysqldump: Got error: 23: Out of resources when opening file './xiangyu/xy_user_meet_sum_20170410_9.MYD' (Errcode: 24) when using LOCK TABLES
```

原因：因为打开的文件数超过了my.cnf的--open-files-limit。

* 解决办法1：更改mysql的配置文件。`/etc/my.cnf`

查看系统打开文件的数目：

```
# ulimit -n  
    65535
```

```shell
 open_files_limit = 65535 # 如果没有请加上这句配置
```

`service mysqld restart` 重启mysql服务。问题就解决了。

查看mysql打开文件的状态：

```mysql
mysql> show global variables like 'open%';
+------------------+-------+
| Variable_name    | Value |
+------------------+-------+
| open_files_limit | 65536 |
+------------------+-------+
1 row in set (0.00 sec)
```

* 解决办法2：

```shell
# 非锁表方式导出数据，不影响原表写入
 mysqldump -uroot -ppasswd --databases dbname --lock-tables=false  > /tmp/20171013_xy.sql
 
## mysqldump几种方式 
 1、非锁表方式导出数据，不影响原表写入
mysqldump  -h    -u  -p  databasename tablename  --lock-table=false  > xx.sql
2、只导出数据,不带建表语句
mysqldump -t -h    -u  -p  databasename tablename  --lock-table=false  > xx.sql
3、只导出建表语句
mysqldump -d -h    -u  -p  databasename tablename  --lock-table=false  > xx.sql
 
4、只导出数据,不带drop-table、lock-tables、set-charset、disable-keys等选项
mysqldump --skip-opt   -h    -u  -p  databasename tablename  --lock-table=false  > xx.sql
 
 5、带条件导出数据
mysqldump --skip-opt   -h    -u  -p  databasename tablename  --lock-table=false  -w"status=3 and createtime < '2013-12-01'" > xx.sql
 
```
 



