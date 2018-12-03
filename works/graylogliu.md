日志切割

原日志格式：  
更新

```shell
GET /?wtype=crawler.py&message=%7B%22status%22%3A+%22ACCESS%22%2C+%22info%22%3A+%22update+end%2C+update+num+%3A0%22%2C+%22area%22%3A+%22%5Cu9ed1%5Cu9f99%5Cu6c5f%22%7D&event=judgement&wname=dev-hlj HTTP/1.1
```

error

```shell
GET /?wtype=crawler.py&message=%7B%22status%22%3A+%22ERROR%22%2C+%22data%22%3A+%7B%22url%22%3A+%222f51e06de72ed92a8410f570dd9aded6%22%2C+%22publish_date%22%3A+%222018-12-02%22%2C+%22area%22%3A+%22%5Cu65b0%5Cu7586%22%7D%7D&event=judgement&wname=dev-xj HTTP/1.1
```

需要的字段：

切割方式：

```shell
#获取每天更新的总量
(?<status>ACCESS).*(?<update>update\Send).*event=(?<event>\w+)
```

结果：

```shell

```

{  
  "status": \[  
    \[  
      "ACCESS"  
    \]  
  \],  
  "update": \[  
    \[  
      "update+end"  
    \]  
  \],  
  "event": \[  
    \[  
      "judgement"  
    \]  
  \]  
}

```
#获取报错信息
(?<status>ERROR).*event=(?<event>\w+)
```

结果：

```shell
{
  "status": [
    [
      "ERROR"
    ]
  ],
  "event": [
    [
      "judgement"
    ]
  ]
}
```

报错：

```shell
(?<status>ERROR).*event=(?<event>\w+).*wname=(?<wname>\w+.*)

# 结果
{
  "status": [
    [
      "ERROR"
    ]
  ],
  "event": [
    [
      "judgement"
    ]
  ],
  "wname": [
    [
      "dev-xj HTTP/1.1"
    ]
  ]
}

```



