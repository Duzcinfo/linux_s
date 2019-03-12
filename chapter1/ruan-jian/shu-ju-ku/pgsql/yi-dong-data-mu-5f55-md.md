
---

title: pg数据库迁移数据目录问题  
date: 20190311

> 场景需求：本地的pg数据库，存储空间已满，需要迁移到挂载的磁盘。其中所遇到的问题，记录如下。  
> 环境为：ubuntu16 postgresql9.5 ,apt安装

## 迁移

[迁移文档参考1](https://tutorials.technology/tutorials/83-Moving-PostgreSQL-data-directory-to-a-new-path.html)  
[迁移文档参考2](https://www.digitalocean.com/community/tutorials/how-to-move-a-postgresql-data-directory-to-a-new-location-on-ubuntu-16-04)

pg 目录如下：

```shell
/var/lib/postgresql/9.5/main  # 数据目录
##如何查看数据目录的配置
方法1：
1. su - postgres 
2. psql
3. SHOW data_directory;
方法2：
cat /etc/postgresql/9.6/main/postgresql.conf | grep data_directory

/etc/postgresql/9.6/main/postgresql.conf  # postgresql 配置文件
```

1. 停掉postgresql的服务

```shell
sudo systemctl stop postgres
```
 
 2. 移动数据
 
 ```shell
 sudo rsync -av /var/lib/postgresql /mnt/new_volume
 ```
 3. 
 


