---
title: banwagong
sys: centos7
---

# 服务搭建.md

## 系统初始化

## 需要的服务

## git

## docker服务

[docker文档](https://docs.docker-cn.com/engine/installation/)

* 安装

```text
yum install -y yum-utils device-mapper-persistent-data lvm2 #安装所需的软件包。
yum-config-manager \
     --add-repo \
     https://download.docker.com/linux/centos/docker-ce.repo
     #使用下列命令设置 stable 镜像仓库。

yum makecache fast # 更新yum软件包
yum install docker-ce  # 安装

systemctl start docker #启动docker
```

**注意**：此 yum list 命令仅显示二进制软件包。如果还需要显示 源软件包，请从软件包名称中省略 .x86\_64

```text
[root@localhost ~]# yum list docker-ce.x86_64  --showduplicates | sort -r
 * updates: mirror.jaleco.com
Loading mirror speeds from cached hostfile
Loaded plugins: fastestmirror
Installed Packages
 * extras: centos-distro.1gservers.com
 * elrepo-kernel: repos.lax-noc.com
docker-ce.x86_64            3:18.09.4-3.el7                    docker-ce-stable 
docker-ce.x86_64            3:18.09.4-3.el7                    @docker-ce-stable
docker-ce.x86_64            3:18.09.3-3.el7                    docker-ce-stable 
docker-ce.x86_64            3:18.09.2-3.el7                    docker-ce-stable 
docker-ce.x86_64            3:18.09.1-3.el7                    docker-ce-stable 
docker-ce.x86_64            3:18.09.0-3.el7                    docker-ce-stable 
docker-ce.x86_64            18.06.3.ce-3.el7                   docker-ce-stable 
docker-ce.x86_64            18.06.2.ce-3.el7                   docker-ce-stable 
docker-ce.x86_64            18.06.1.ce-3.el7                   docker-ce-stable 
docker-ce.x86_64            18.06.0.ce-3.el7                   docker-ce-stable 
docker-ce.x86_64            18.03.1.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            18.03.0.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.12.1.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.12.0.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.09.1.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.09.0.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.06.2.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.06.1.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.06.0.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.03.3.ce-1.el7                   docker-ce-stable 
docker-ce.x86_64            17.03.2.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.03.1.ce-1.el7.centos            docker-ce-stable 
docker-ce.x86_64            17.03.0.ce-1.el7.centos            docker-ce-stable 
#安装指定版本
yum install docker-ce-<VERSION>
```

## hexo博客

## shadowsocks（docker安装）

docker：docker pull oddrationale/docker-shadowsocks

### docker运行命令

```text
docker run -dt --name ss -p 6443:6443 mritd/shadowsocks -s "-s 0.0.0.0 -p 6443 -m chacha20-ietf-poly1305 -k test123"
-m : 指定 shadowsocks 命令，默认为 ss-server
-s : shadowsocks-libev 参数字符串
-x : 开启 kcptun 支持
-e : 指定 kcptun 命令，默认为 kcpserver
-k : kcptun 参数字符串
-r : 使用 /dev/urandom 来生成随机数
```

## nginx

[nginx-docker仓库](https://hub.docker.com/_/nginx) docker pull nginx

* nginx.sh

  ```text
  #!/bin/bash
  docker run --name nginx \
  -v $PWD/conf.d/:/etc/nginx/conf.d/ \
  -v /var/log/nginx:/var/log/nginx\
  -v $PWD/www:/usr/share/nginx/html \
  -p 8080:80 \
  -d nginx
  ```

## rap2

## jenkins

## postgresql

## python虚拟环境

### pyenv

```text
git clone git://github.com/yyuu/pyenv.git ~/.pyenv

vim ~/.bash_profile
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

* 用法

```text
   commands    List all available pyenv commands
   local       Set or show the local application-specific Python version
   global      Set or show the global Python version
   shell       Set or show the shell-specific Python version
   install     Install a Python version using python-build
   uninstall   Uninstall a specific Python version
   rehash      Rehash pyenv shims (run this after installing executables)
   version     Show the current Python version and its origin
   versions    List all Python versions available to pyenv
   which       Display the full path to an executable
   whence      List all Python versions that contain the given executable
```

### 插件

```text
git clone git://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv
exec $SHELL # 重新加入配置
```

