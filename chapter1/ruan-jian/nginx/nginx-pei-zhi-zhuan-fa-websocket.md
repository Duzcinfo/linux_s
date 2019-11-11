---
description: nginx配置转发websocket
---

# nginx配置转发websocket

```text
   location /ws {
    proxy_pass http://192.168.31.58:8080/fmback/api/webSocket;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
}

```

主要是参数：

proxy\_set\_header Upgrade,Conection "upgrade"

