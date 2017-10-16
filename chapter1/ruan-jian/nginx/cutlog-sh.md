---
details: nginx日志切割脚本
---



> nginx 日志切割脚本

```shell
#!/bin/bash
# this script run at 00:00.
# The nginx logs path
# script_files_name:nginx_logrotate.sh
Logs_path='/tmp/test'
Years=`date -d "yesterday" +"%Y"`
Mounth=`date -d "yesterday" +"%m"`
mkdir -p ${Logs_path}/${Years}/${Mounth}/
mv ${Logs_path}access.log  ${Logs_path}/${Years}/${Mounth}/access_$(date -d "yesterday" +"%Y%m%d").log
kill -USR1 `path/nginx.pid`

```

```shell
#!/bin/bash
pid=`cat /usr/local/nginx/logs/nginx.pid`
d=`date -d "-1 day" +%Y%m%d`
mv /tmp/1.log /tmp/$d.log
kill -HUP $pid
gzip -f /tmp/$d.log
```

将脚本放入`crontab `

```shell
00 00 * * * /bin/bash   /usr/local/sbin/nginx_logrotate.sh
```



