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

# gitlab 使用ssh登陆

使用gitlab ssh 登陆，添加ssh ，在使用时，可以 pul ，但是 push 会报错误：

![](/assets/ssh-git.png)

```shell
解决方法：

在.ssh目录下，创建的 config 文件，更改一下内容：
# gitlab
Host sc-git   # 更改的内容
    HostName sc-git  # 更改的内容
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/yc
# github
Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/github_id-rsa
```

问题解决

