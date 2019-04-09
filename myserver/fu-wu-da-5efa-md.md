---
title: banwagong
sys: centos7 
---

# 系统初始化
# 需要的服务
# git 
# docker服务
[docker文档](https://docs.docker-cn.com/engine/installation/)

# hexo博客
# shadowsocks（docker安装）
docker：docker pull oddrationale/docker-shadowsocks

## docker运行命令
```shell
docker run -dt --name ss -p 6443:6443 mritd/shadowsocks -s "-s 0.0.0.0 -p 6443 -m chacha20-ietf-poly1305 -k test123"
-m : 指定 shadowsocks 命令，默认为 ss-server
-s : shadowsocks-libev 参数字符串
-x : 开启 kcptun 支持
-e : 指定 kcptun 命令，默认为 kcpserver
-k : kcptun 参数字符串
-r : 使用 /dev/urandom 来生成随机数
```

# nginx
# rap2 
# jenkins
# postgresql
# python虚拟环境 

