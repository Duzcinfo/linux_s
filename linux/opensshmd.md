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

## linux ssh 登陆失败

```shell
ssh_exchange_identification: read: Connection reset by peer
```

* 调试模式

```shell
ubuntu@ubuntu-31-59:~$ ssh root@192.168.31.55 -vvv
OpenSSH_7.2p2 Ubuntu-4ubuntu2.6, OpenSSL 1.0.2g  1 Mar 2016
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: Applying options for *
debug2: resolving "192.168.31.55" port 22
debug2: ssh_connect_direct: needpriv 0
debug1: Connecting to 192.168.31.55 [192.168.31.55] port 22.
debug1: Connection established.
debug1: key_load_public: No such file or directory
debug1: identity file /home/ubuntu/.ssh/id_rsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/ubuntu/.ssh/id_rsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/ubuntu/.ssh/id_dsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/ubuntu/.ssh/id_dsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/ubuntu/.ssh/id_ecdsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/ubuntu/.ssh/id_ecdsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/ubuntu/.ssh/id_ed25519 type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/ubuntu/.ssh/id_ed25519-cert type -1
debug1: Enabling compatibility mode for protocol 2.0
debug1: Local version string SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.6
ssh_exchange_identification: read: Connection reset by peer
```

# ssh 登录不上

* 目录权限问题

sshd 的 目录权限一定为 755.不能是777，一一旦权限不对，系统会自检。

```shell
ubuntu@node0:~$ ll -d /var/run/sshd
drwxr-xr-x 2 root root 40 Jan 15 11:03 /var/run/sshd/
```

* 会被忽略掉的防火墙

在开启防火墙的时候，请注意查看是否开放22端口。

# github添加ssh

```shell
git config --global user.name "xxx"
git config --global user.email "xxx@gmail.com"
# 添加git账号
ssh-keygen -t rsa -C "your_email@example.com"
ssh-agent -s
ssh-add
# 如果执行ssh-add出现错误Could not open a connection to your authentication agent.
# 执行eval `ssh-agent -s`
再将公钥传入github上

[root@host www]# ssh -T git@github.com
Hi Duzcinfo! You've successfully authenticated, but GitHub does not provide shell access.  ##成功
```



