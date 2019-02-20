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



## 限制服务器登录

只允许某个组的用户登录服务器

* sshd\_config文件

```shell
# Package generated configuration file
# See the sshd_config(5) manpage for details

# What ports, IPs and protocols we listen for
Port 22
# Use these options to restrict which interfaces/protocols sshd will bind to
#ListenAddress ::
#ListenAddress 0.0.0.0
Protocol 2
# HostKeys for protocol version 2
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_dsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key
#Privilege Separation is turned on for security
UsePrivilegeSeparation yes

# Lifetime and size of ephemeral version 1 server key
KeyRegenerationInterval 3600
ServerKeyBits 1024

# Logging
SyslogFacility AUTH
LogLevel VERBOSE

# Authentication:
LoginGraceTime 120
PermitRootLogin without-password
StrictModes no

RSAAuthentication yes
PubkeyAuthentication yes
#AuthorizedKeysFile	.ssh/authorized_keys
AuthorizedKeysFile	%h/.ssh/authorized_keys

# Don't read the user's ~/.rhosts and ~/.shosts files
IgnoreRhosts yes
# For this to work you will also need host keys in /etc/ssh_known_hosts
RhostsRSAAuthentication no
# similar for protocol version 2
HostbasedAuthentication no
# Uncomment if you don't trust ~/.ssh/known_hosts for RhostsRSAAuthentication
#IgnoreUserKnownHosts yes

# To enable empty passwords, change to yes (NOT RECOMMENDED)
PermitEmptyPasswords no

# Change to yes to enable challenge-response passwords (beware issues with
# some PAM modules and threads)
ChallengeResponseAuthentication no

# Change to no to disable tunnelled clear text passwords
#PasswordAuthentication yes

# Kerberos options
#KerberosAuthentication no
#KerberosGetAFSToken no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes

X11Forwarding yes
X11DisplayOffset 10
PrintMotd no
PrintLastLog yes
TCPKeepAlive yes
UseLogin yes

#MaxStartups 10:30:60
#Banner /etc/issue.net

# Allow client to pass locale environment variables
AcceptEnv LANG LC_*

Subsystem sftp /usr/lib/openssh/sftp-server

# Set this to 'yes' to enable PAM authentication, account processing,
# and session processing. If this is enabled, PAM authentication will
# be allowed through the ChallengeResponseAuthentication and
# PasswordAuthentication.  Depending on your PAM configuration,
# PAM authentication via ChallengeResponseAuthentication may bypass
# the setting of "PermitRootLogin without-password".
# If you just want the PAM account and session checks to run without
# PAM authentication, then enable this but set PasswordAuthentication
# and ChallengeResponseAuthentication to 'no'.
UsePAM yes
AllowGroups sc

```



