```
密码策略合规检测会检测如下Linux账户密码策略：
```

```
1.账号密码最大使用天数
2.密码修改最小间隔天数
3.账号不活动最长天数
加固建议：
1.在/etc/login.defs 里面修改 PASS_MAX_DAYS 1095
2.在/etc/login.defs 里面修改 PASS_MIN_DAYS 7
3.执行useradd -D -f 1095
```

* ssl登录

```shell
SSH登录安全策略检测如下配置：
1.登录端口是否为默认22端口
2.root账号是否允许直接登录
3.是否使用不安全的SSH V1协议
4.是否使用不安全的rsh协议
5.是否运行基于主机身份验证的登录
修复方案：
编辑 /etc/ssh/sshd_config
1.Port（非22）
2.PermitRootLogin（no）
3.Protocol（2）
4.IgnoreRhosts（yes）
5.HostbasedAuthentication（no）
```

