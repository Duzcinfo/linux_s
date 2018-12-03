日志切割

原日志格式：

```shell
GET /?wtype=crawler.py&message=%7B%22url%22%3A+%22http%3A%2F%2Fwww.hshfy.sh.cn%2Fshfy%2Fgweb2017%2Fflws_view.jsp%3Fpa%3DadGFoPaOoMjAxOKOpu6YwMTEww%2FGz9TE5NTAyusUmd3N4aD0xz%22%2C+%22status%22%3A+%22ACCESS%22%2C+%22s3_path%22%3A+%22data%2F2018%2F10%2F30%2F5734a383ce39dc7ea56ce755486dc1fe.json%22%7D&event=judgement&wname=dev-judgement_detail_sh_4 HTTP/1.1
```

需要的字段：

切割方式：

```shell
#获取每天更新的总量
(?<status>ACCESS).*(?<update>update\Send).*event=(?<event>\w+)

#获取报错信息
(?<status>ERROR).*event=(?<event>\w+)
```



