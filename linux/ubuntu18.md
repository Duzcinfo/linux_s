---
title: ubuntu18
---

# 网络

ubuntu18采用了`yaml`的格式，和之前的ubuntu16有区别。

## 修改主机名

ubuntu 18.04不能直接修改/etc/hostname中主机名称,重启后又恢复到安装时设置的主机名称.正确的修改步骤如下:  
`sudo vim /etc/cloud/cloud.cfg`,找到preserve\_hostname: false修改为preserve\_hostname: ture  
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
## 网络
已经安装了kvm的网络配置
```yaml
  bridges:
	br0:
	  interfaces: [enp103s0f0]
	  dhcp4: no
	  addresses: [172.30.10.102/24]
	  gateway4: 172.30.10.1
	  nameservers:
		addresses: [61.128.128.68]
        
        
        
        
        
        network:
    ethernets:
        enp103s0f0:
            addresses: [172.30.10.101/24]
            dhcp4: no
            gateway4: 172.30.10.1
        enp103s0f1:
            addresses: []
            dhcp4: true
            optional: true
        enp103s0f2:
            addresses: []
            dhcp4: true
            optional: true
        enp103s0f3:
            addresses: []
            dhcp4: true
            optional: true
        bridges:
                br0:
                interfaces: [enp103s0f0]
                dhcp4: no
                addresses: [172.30.10.102/24]
                gateway4: 172.30.10.1
                nameservers:
                addresses: [61.128.128.68]


    version: 2

```


# kvm虚拟化

```shell
userroot@ubuntu:~$ Unable to init server: Could not connect: Connection refused
Unable to init server: Could not connect: Connection refused
Unable to init server: Could not connect: Connection refused

(virt-manager:11101): Gtk-WARNING **: 05:42:18.976: cannot open display: 
```
`egrep -c '(vmx|svm)' /proc/cpuinfo`   大于0，硬件支持虚拟化 

```shell
 sudo apt install --no-install-recommends ubuntu-desktop
 sudo apt install qemu qemu-kvm libvirt-bin bridge-utils virt-manager virtinst cpu-checker 
```
[root@localhost ~]# systemctl enable libvirtd
[root@localhost ~]# systemctl start libvirtd




出现error错误：
解决办法，添加源
源：
deb http://archive.ubuntu.com/ubuntu bionic main universe restricted multiverse
deb http://archive.ubuntu.com/ubuntu bionic-security main universe restricted multiverse
deb http://archive.ubuntu.com/ubuntu bionic-updates main universe restricted multiverse





```yml
network:
    ethernets:
        enp103s0f0:
            dhcp4: no
    bridges:
            br0:
                    interfaces: [enp103s0f0]
                    dhcp4: no
                    addresses: [192.168.21.3/24]
                    gateway4: 192.168.21.1
                    nameservers:
                            addresses: [61.128.128.68]

    version: 2
```




