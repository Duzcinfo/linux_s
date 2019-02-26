* # 负载后，地址及其客户端程序问题 {#h1_10}

```shell
 nginx反向代理配置时，一般会添加下面的配置：  
      proxy_set_header Host $host;  
      proxy_set_header X-Real-IP $remote_addr;  
      proxy_set_header REMOTE-HOST $remote_addr;  
      proxy_set_header X-Forwarded-Fo
      $proxy_add_x_forwarded_for;
    proxy_connect_timeout       1;
    proxy_read_timeout          1;
    proxy_send_timeout          1;
  #  proxy_connect_timeout 个参数， 这个参数是连接的超时时间。 我设置成1，表示是1秒后超时会连接到另外一台服务器。
```



