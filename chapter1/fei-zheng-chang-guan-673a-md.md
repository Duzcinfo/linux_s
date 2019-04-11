---
title: 非正常关机
---

linux 自动关机排查方法
1. 系统日志在 `/var/log`,查看message 信息有无温度过高
2.查看 var/log/cron 
     该日志文件记录crontab守护进程crond所派生的子进程的动作，前面加上用 户、登录时间和PID，以及派生出的进程的动作。CMD的一个动作是cron派生出一个调度进程的常见情况。REPLACE（替换）动作记录用户对它的 cron文件的更新，该文件列出了要周期性执行的任务调度。 RELOAD动作在REPLACE动作后不久发生，这意味着cron注意到一个用户的cron文件被更新而cron需要把它重新装入内存。该文件可能会查 到一些反常的情况。
3. 查看last 
4. 查看 /var/log/boot.log    该文件记录了系统在引导过程中发生的事件，就是Linux系统开机自检过程显示的信息。
 
 
 ## last
 last参数详解
 
 ```shell
用户名  终端（pts|tty0-tty6） 登录ip或者内核  开始时间    结束时间  持续时间

zhichuan pts/7        172.16.8.83      Mon Apr  1 09:32 - 11:52  (02:20)
jiangong pts/1        172.16.8.159     Mon Apr  1 09:29 - 20:02  (10:33)

```

可以用

`sudo dump-utmp  btmp` 查看 last信息

安装该命令 : `sudo apt install acct`