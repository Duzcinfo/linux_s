---
title: ubuntu18
---
# 网络
ubuntu18采用了
## 修改主机名
ubuntu 18.04不能直接修改/etc/hostname中主机名称,重启后又恢复到安装时设置的主机名称.正确的修改步骤如下:
`sudo vim /etc/cloud/cloud.cfg`,找到preserve_hostname: false修改为preserve_hostname: ture
1. 永久修改主机名
`sudo vim /etc/hostname`
2. 临时修改主机名
`#hostname master`
查看主机名：主机名实际存储在`/proc/sys/kernel/hostname`,但是该文件不能修改。
## 网络的自检
有时候是离线安装，所以系统自检网络还是比较费时间。
关掉网络自检：
```shell
A start job is running for wait for network to be configured  
 
$ sudo systemctl stop systemd-networkd-wait-online.service
$ sudo systemctl disable systemd-networkd-wait-online.service

 或
/lib/systemd/system/NetworkManager-wait-online.service
```




# kvm虚拟化


