如何用 curl 测试相应网页的速度？

```shell
curl -o /dev/null -s -w %{time_namelookup}:%{time_connect}:%{time_starttransfer}:%{time_total} http://www.baidu.com

time_namelookup:解析时间
time_connect:连接时间
time_starttransfer:传送时间
time_total:总的时间

0.004:0.033:0.064:0.064
```



