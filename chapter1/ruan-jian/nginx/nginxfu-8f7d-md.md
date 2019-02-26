* # 负载后，地址及其客户端程序问题 {#h1_10}

```shell
 nginx反向代理配置时，一般会添加下面的配置：  
      proxy_set_header Host $host;  
      proxy_set_header X-Real-IP $remote_addr;  
      proxy_set_header REMOTE-HOST $remote_addr;  
      proxy_set_header X-Forwarded-Fo
      $proxy_add_x_forwarded_for;
```



