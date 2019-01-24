> 当服务挂掉，通过多口找问题

* 查看端口

```shell
netstat -lntup
```

* 查看服务端口的启动时间

```shell
# 首先找到该进程是由什么服务起的
netstat -lntup
# 查看端口的运行时间
ps `pid`

ubuntu@localhost$ ps 1936
  PID TTY      STAT   TIME COMMAND
 1936 ?        Sl     3:11 java -jar 
 
 #TIME就是启动的时间
```



