# nginx编译安装&动态模块



## 编译参数

```text
   ./configure --prefix=/usr/local/nginx \
--with-http_addition_module \
--with-http_flv_module \
--with-http_gzip_static_module \
--with-http_realip_module \
--with-http_ssl_module \
--with-http_stub_status_module \
--with-http_sub_module \
--with-http_dav_module --with-http_v2_module 
```



```text
 ✘ ⚡ root@devop-All-Series  /usr/local/src/nginx-1.16.1  systemctl restart  nginx
Failed to restart nginx.service: Unit nginx.service is masked.
```

ubuntu18加入开机的脚本，启动报错，解决办法：

```text
 ✘ ⚡ root@devop-All-Series  /usr/local/src/nginx-1.16.1  systemctl unmask nginx.service
Removed /etc/systemd/system/nginx.service.
```

成功启动

**编译动态模块**

```text
   ./configure --prefix=/usr/local/nginx \
--with-http_addition_module \
--with-http_flv_module \
--with-http_gzip_static_module \
--with-http_realip_module \
--with-http_ssl_module \
--with-http_stub_status_module \
--with-http_sub_module \
--with-http_dav_module --with-http_v2_module \
--add-module=/opt/nginx_module/echo-nginx-module-0.61/
```

--add-module=/path/



编译安装升级

执行过程： .configure ---&gt; make    ,然后备份`mv /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.bak` 

最后`cp objs/nginx /usr/local/nginx/sbin/`, 升级完成。

