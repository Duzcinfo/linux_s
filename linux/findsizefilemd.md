当用`df -h` 或 `du -sh` 看不出来时，请使用：

第一个方法只用到了一个命令find,它能够帮我们做一些文件查找的操作。它常用的参数有: 
- type:类型。POSIX支持——b:块设备文档、d:目录、c:字符设备文档、P:管道文档、l:符号链接文档、f:普通文档 
- name:按文件名查找。支持*模糊匹配 
- size:文件大小。+表示大于，-表示小于。支持k,M,G单位。


`find  . -type f -size +500M`

方法二：

第二个方法又进了一步，不仅把大于800M的文件列出来，还进一步对他们分别做了ls -lh操作。这里新出现了一个xargs命令。它的作用就是把管道进来的参数切分成多个部分，分别作为新的参数调用后续的命令。比如这里，xargs管道进来的是找到的所有文件绝对路径，把他们作为ls -lh参数，也就是打印出每个文件的具体信息。
`find . -type f -size +800M | xargs ls -lh`

方法三：
第三个方法则分别对找出来的数据进行排序

`find . -type f -size +800M | xargs du -hm | sort -nr`



du命令即disk usage,是用来统计文件占用磁盘大小的。sort顾名思义是排序的。具体就不说了，这两个是比较简单的命令
查找最大目录：

```shell
du -h --max-depth=1
du -hm --max-depth=2 | sort -n
du -hm --max-depth=2 | sort -nr | head -12
```

