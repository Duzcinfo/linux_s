---
title: install-pg-client
---

# install-client-pg.md

> 安装pg连接工具的客户端，系统是ubuntu

## 安装客户端

```text
sudo apt search  postgresql-client
Sorting... Done
Full Text Search... Done
postgresql-client/xenial-updates 9.5+173ubuntu0.2 all
  front-end programs for PostgreSQL (supported version)

postgresql-client-9.5/xenial-updates,xenial-security 9.5.14-0ubuntu0.16.04 amd64
  front-end programs for PostgreSQL 9.5

postgresql-client-common/xenial-updates,now 173ubuntu0.2 all [installed]
  manager for multiple PostgreSQL client versions
```

* 安装

[https://www.postgresql.org/download/linux/ubuntu/](https://www.postgresql.org/download/linux/ubuntu/)

```text
sudo apt  install postgresql-client-9.5
```

[客户端](https://www.postgresql.org/download/linux/ubuntu/)

### 安装deb包

[deb包下载](https://packages.ubuntu.com/xenial/all/postgresql-client-common/download)

sudo dpkg -i name.deb

