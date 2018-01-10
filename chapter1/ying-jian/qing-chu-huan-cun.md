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



