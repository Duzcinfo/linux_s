---
title: es的安装
---
> os.version: ubuntu16
elasticsearch: 6.8.1
kibana: 6.8.1

# 安装 elasticseach

[elasticsearch 下载地址](https://www.elastic.co/cn/downloads/)


* 修改配置

```wiki
vim /path/elasticsearch.yml
path.data
path.log

vim /path/jvm.options

-Xms1g
-Xmx1g   # 一般更改为内存的一半或者2/3

```

# 查询

```html
GET _nodes/stats  #查看节点信息，path.data，内存等
GET _cluster/heath #健康检查


```
