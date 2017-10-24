## 服务器端

* 基于秘钥

1.生成一对秘钥

```shell
ssh-keygen 

ssh-copy-id "root@host"
```

2.将公钥传至服务器端某用户的家目录下.ssh/authorized\_keys

3.登录

* 基于口令

#### 红帽系列ssh配置

* 目录

```shell
/etc/sh

ssh (ssh_config)#客户端
sshd(sshd_config)#服务端
```



