---
date: 2017.10.15
---

# 配置.md

fastcgi.conf

```text
fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;
fastcgi_param  QUERY_STRING       $query_string;
fastcgi_param  REQUEST_METHOD     $request_method;
fastcgi_param  CONTENT_TYPE       $content_type;
fastcgi_param  CONTENT_LENGTH     $content_length;

fastcgi_param  SCRIPT_NAME        $fastcgi_script_name;
fastcgi_param  REQUEST_URI        $request_uri;
fastcgi_param  DOCUMENT_URI       $document_uri;
fastcgi_param  DOCUMENT_ROOT      $document_root;
fastcgi_param  SERVER_PROTOCOL    $server_protocol;
fastcgi_param  HTTPS              $https if_not_empty;

fastcgi_param  GATEWAY_INTERFACE  CGI/1.1;
fastcgi_param  SERVER_SOFTWARE    nginx/$nginx_version;

fastcgi_param  REMOTE_ADDR        $remote_addr;
fastcgi_param  REMOTE_PORT        $remote_port;
fastcgi_param  SERVER_ADDR        $server_addr;
fastcgi_param  SERVER_PORT        $server_port;
fastcgi_param  SERVER_NAME        $server_name;

# PHP only, required if PHP was built with --enable-force-cgi-redirect
fastcgi_param  REDIRECT_STATUS    200;
```

> 在vhost文件，`location ~ .*\.(php|php5)?$`末尾加上`include fcgi.conf`

## 优化内核参数

* vim /etc/sysctl.conf

```text
# Kernel sysctl configuration file for Red Hat Linux
#
# For binary values, 0 is disabled, 1 is enabled.  See sysctl(8) and
# sysctl.conf(5) for more details.

# Controls IP packet forwarding   控制IP包转发
net.ipv4.ip_forward = 0

# Controls source route verification 控制源路由校验

# Do not accept source routing  
net.ipv4.conf.default.accept_source_route = 0  

# Controls the System Request debugging functionality of the kernel 内核系统请求调试功能控制,0表示禁用,1表示启用
kernel.sysrq = 0

# Controls whether core dumps will append the PID to the core filename. 内核转存是否根据进程ID保存成文件
# Useful for debugging multi-threaded applications.   这有利于多线程调试,0表示禁用,1表示启用
kernel.core_uses_pid = 1

# Controls the use of TCP syncookies  是否使用TCP同步cookies,0表示禁用,1表示启用

# Disable netfilter on bridges.   禁用桥接网络过滤,0表示禁用,1表示启用
net.bridge.bridge-nf-call-ip6tables = 0
net.bridge.bridge-nf-call-iptables = 0
net.bridge.bridge-nf-call-arptables = 0

# Controls the default maxmimum size of a mesage queue  消息队列最大值
kernel.msgmnb = 65536

# Controls the maximum size of a message, in bytes 设置消息的大小,以字节为单位
kernel.msgmax = 65536

# Controls the maximum shared segment size, in bytes 控制最大的共享段最大使用尺寸,以字节为单位,对于oracle来说，通常将其设置为2G。
kernel.shmmax = 68719476736  

# Controls the maximum number of shared memory segments, in pages   控制最大页面内最大的共享内存段,该参数表示系统一次可以使用的共享内存总量（以页为单位）,通常不需要修改。
kernel.shmall = 4294967296

vm.swappiness = 0
net.ipv4.neigh.default.gc_stale_time=120
net.ipv4.conf.all.rp_filter=0
net.ipv4.conf.default.rp_filter=0
net.ipv4.conf.default.arp_announce = 2
net.ipv4.conf.all.arp_announce=2
net.ipv4.tcp_max_tw_buckets = 5000
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_max_syn_backlog = 1024
net.ipv4.tcp_synack_retries = 2
net.ipv4.conf.lo.arp_announce=2
```

* 防ddos

```text
##自定义

  #0表示禁用,1表示启用,表示开启SYN Cookies,当SYN等待队列溢出时,启用cookies来处理,可以防范少量的SYN攻击,默认为0,表示关闭

    net.ipv4.tcp_syncookies = 1

    #0表示禁用,1表示启用,允许将TIME_WAIT sockets重新用于新的TCP连接,默认为0,表示关闭

    net.ipv4.tcp_tw_reuse = 1

    #0表示禁用,1表示启用,允许将TIME_WAIT sockets快速回收以便利用,默认为0,表示关闭
     net.ipv4.tcp_tw_recycle = 1

   #设置TCP三次请求的fin状态超时
     net.ipv4.tcp_fin_timeout = 30

   #以上4个绿色的设置,以防DDoS,CC和SYN攻击
```

* 提升并发

```text
  #设置TCP 发送keepalive的频度,默认的缺省为2小时,1200秒表示20分钟,表示服务器以20分钟发送keepalive消息

   net.ipv4.tcp_keepalive_time = 1200

   #探测包发送的时间间隔设置为2秒

   net.ipv4.tcp_keepalive_intvl = 2

   #如果对方不给予应答,探测包发送的次数
   net.ipv4.tcp_keepalive_probes = 2

   #设置本地端口范围,缺省情况下:32768 到 61000,现在改为10000 到 65000,最小值不能设置太低,否则占用了正常端口
   net.ipv4.ip_local_port_range = 10000 65000

   #表示SYN队列的长度,默认为1024,加大队列长度为8192,可以容纳更多的网络连接数
   net.ipv4.tcp_max_syn_backlog = 8192

   #设置保持TIME_WAIT的最大数量,如果超过这个数量,TIME_WAIT将立刻清楚并打印警告信息,默认为180000,改为5000.对于Apache,Nginx等服务器,上几行的参数可以很好滴减少TIME_WAIT套接字数量,对于Squid(代理软件,实现正向代理或者反向代理,主要以实现缓存为主),效果却不打.此项参数可以控制TIME_WAIT的最大数量,避免Squid服务器被大量的TIME_WAIT拖死.
   net.ipv4.tcp_max_tw_buckets = 5000

   #配置服务器拒绝接受广播风暴或者smurf 攻击attacks,0表示禁用,1表示启用,这是忽略广播包的作用

   net.ipv4.icmp_echo_ignore_broadcasts = 1

  #有些路由器针对广播祯发送无效的回应，每个都产生警告并在内核产生日志。这些回应可以被忽略,0表示禁用,1表示启用,

  net.ipv4.icmp_ignore_bogus_error_responses = 1

  #开启并记录欺骗，源路由和重定向包

 net.ipv4.conf.all.log_martians = 1

  #表示SYN队列的长度，选项为服务器端用于记录那些尚未收到客户端确认信息的连接请求的最大值。

   该参数对应系统路径为：/proc/sys/net/ipv4/tcp_max_syn_backlog
  net.ipv4.tcp_max_syn_backlog = 4096

  #增加tcp buff  size,tcp_rmem表示接受数据缓冲区范围从4096 到 87380 到16777216

   tcp_wmem表示发送数据缓冲区范围从4096 到 87380 到16777216
   net.ipv4.tcp_rmem = 4096 87380 16777216
   net.ipv4.tcp_wmem = 4096 65536 16777216

   #TCP失败重传次数,默认值15,意味着重传15次才彻底放弃.可减少到5,以尽早释放内核资源
   net.ipv4.tcp_retries2 = 5

  #选项默认值是128，这个参数用于调节系统同时发起的tcp连接数，在高并发请求中，默认的值可能会导致连接超时或重传，因此，需要结合并发请求数来调节此值。该参数对应系统路径为：/proc/sys/net/core/somaxconn 128
    net.core.somaxconn = 4096

   #设置tcp确认超时时间 300秒,这在TCP三次握手有体现,结合本文的图理解

   net.netfilter.nf_conntrack_tcp_timeout_established = 300

    #设置tcp等待时间 12秒,超过12秒自动放弃
   net.netfilter.nf_conntrack_tcp_timeout_time_wait = 12

   #设置tcp关闭等待时间60秒,超过60秒自动关闭
    net.netfilter.nf_conntrack_tcp_timeout_close_wait = 60

  #设置tcp fin状态的超时时间为120秒,超过该时间自动关闭
    net.netfilter.nf_conntrack_tcp_timeout_fin_wait = 120
```

