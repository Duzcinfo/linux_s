# docker ngixn

* pull

```shell
docker pull nignx
```

* run

```shell
 docker run \
    --name nginx\
    -p 80:80 \
    -p 8001:8001\
    -v /usr/nginx/conf.d:/etc/nginx/conf.d\       #将docker容器的配置文件挂载出来
    -d nginx
    
    
    #或
    docker run  --log-driver=gelf --log-opt gelf-address=udp://**.**.**.**:12201 \
--restart=always \
--name ahhx-nginx  \
-p 18090:18090   \
-p 18091:18091 \
-v /opt/test/conf.d:/etc/nginx/conf.d \
-d nginx

```

配置文件  `default.conf`

```shell
upstream duzc{
server 104.224.162.46;

}

server {
    listen 80;
    server_name localhost;
    access_log /var/logs/access.log main
    error_log  /var/logs/error.log info

    location / {
    proxy_redirect off;  
        proxy_set_header Host $host;  
        proxy_set_header X-Real-IP $remote_addr;  
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
        proxy_pass http://duzc; 
      }

      location /pre{
        proxy_redirect off;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
        proxy_pass http://www.baidu.com;
}


}

##这样做行不通，因为 把 url也带过去了，而代理过去的是没有这个url的，除非代理后的url有这个地址。
```



