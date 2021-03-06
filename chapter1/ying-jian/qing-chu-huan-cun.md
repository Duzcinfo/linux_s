# 清除缓存

```text
密码策略合规检测会检测如下Linux账户密码策略：
```

```text
1.账号密码最大使用天数
2.密码修改最小间隔天数
3.账号不活动最长天数
加固建议：
1.在/etc/login.defs 里面修改 PASS_MAX_DAYS 1095
2.在/etc/login.defs 里面修改 PASS_MIN_DAYS 7
3.执行useradd -D -f 1095
```

* ssl登录

```text
SSH登录安全策略检测如下配置：
1.登录端口是否为默认22端口
2.root账号是否允许直接登录
3.是否使用不安全的SSH V1协议
4.是否使用不安全的rsh协议
5.是否运行基于主机身份验证的登录
修复方案：
编辑 /etc/ssh/sshd_config
1.Port（非22）
2.PermitRootLogin（no）
3.Protocol（2）
4.IgnoreRhosts（yes）
5.HostbasedAuthentication（no）
```

```text
> 在Linux系统下，我们一般不需要去释放内存，因为系统已经将内存管理的很好。但是凡事也有例外，有的时候内存会被缓存占用掉，导致系统使用SWAP空间影响性能，此时就需要执行释放内存（清理缓存）的操作了。
```

```text
>
> Linux系统的缓存机制是相当先进的，他会针对dentry（用于VFS，加速文件路径名到inode的转换）、Buffer Cache（针对磁盘块的读写）和Page Cache（针对文件inode的读写）进行缓存操作。但是在进行了大量文件操作之后，缓存会把内存资源基本用光。但实际上我们文件操作已经完成，这部分缓存已经用不到了。这个时候，我们难道只能眼睁睁的看着缓存把内存空间占据掉么？
>
> 所以，我们还是有必要来手动进行Linux下释放内存的操作，其实也就是释放缓存的操作了。

要达到释放缓存的目的，我们首先需要了解下关键的配置文件/proc/sys/vm/drop\_caches。这个文件中记录了缓存释放的参数，默认值为0，也就是不释放缓存。他的值可以为0~3之间的任意数字，代表着不同的含义：

* 0 不释放

* 1 释放页缓存

* 2 释放dentries和inodes

* 3 释放所有缓存






#首先要用sync,将所有未写的系统缓冲区写到磁盘中，包含已修改的 i-node、已延迟的块 I/O 和读写映射文件。否则在释放缓存的过程中，可能会丢失未保存的文件。


echo 3 > /proc/sys/vm/drop_caches

#要查询当前缓存释放的参数，可以输入下面的指令:
cat /proc/sys/vm/drop_caches
```

