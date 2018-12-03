ubuntu 18 和 Ubuntu 16 的网络配置文件不同。ubuntu 18 现在读取的是 yml 文件。

读取的文件： `/etc/netplan/50-cloud-init.yaml`

内容：

```yml
# This file is generated from information provided by
# the datasource.  Changes to it will not persist across an instance.
# To disable cloud-init's network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    ethernets:
        enp103s0f0:
            addresses: [192.168.21.5/24]
            dhcp4: no
            gateway4: 192.168.21.1
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
    version: 2
```

# dns

ubuntu 18 服务器版 只修改 ``/etc/resolv.conf,dns 还是会改回他的默认值 `127.0.0.53 ` ,导致上不了网。``

原因：

在 `/etc/resolv.conf`   有一句注释 ： ```# This file is managed by man:systemd-resolved\(8\). Do not edit.``

说明这个文件被 `systemd-resolve` 托管.

通过`netstat -tnpl| grep systemd-resolved` 查看到这个服务是监听在53号端口上。

```shell
userroot@ubuntu:~$ sudo lsof -i:53
COMMAND    PID            USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
systemd-r 3294 systemd-resolve   12u  IPv4 928128      0t0  UDP localhost:domain 
systemd-r 3294 systemd-resolve   13u  IPv4 928129      0t0  TCP localhost:domain (LISTEN)
```

直接改 /etc/systemd/resolved.conf 这个配置文件

```shell
dns= 8.8.8.8 
```
然后重启 `systemctl restart systemd-resolved`




