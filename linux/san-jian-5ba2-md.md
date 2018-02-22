# sed

# cut

-d 分割符

# join

# awk

> 默认以空白字段为分割符

```awk
awk '{print $1 ,$NF}' #    NF:内建变量.打印第一个字段与最后一个字段。其中当自段为0时，表示整条记录。
awk -F: '{print $1,$5}' /etc/passwd   
awk -F: -v 'OFS=**' '{print $1,$5}' /etc/passwd    #自定义第一个字段和第五个字段的连接符。
nobody**Unprivileged User
root**System Administrator
daemon**System Services
_uucp**Unix to Unix Copy Protocol
_taskgated**Task Gate Daemon



awk -F:  '{print "User",$1 ,"is realy",$5}' /etc/passwd
User nobody is realy Unprivileged User
User root is realy System Administrator
```



