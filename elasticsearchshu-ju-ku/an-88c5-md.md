---
title: es的安装
---

# 安装.md

> os.version: ubuntu16  
> elasticsearch: 6.8.1  
> kibana: 6.8.1

## 安装 elasticseach

[elasticsearch 下载地址](https://www.elastic.co/cn/downloads/)

* 修改配置

```text
vim /path/elasticsearch.yml
path.data
path.log

vim /path/jvm.options

-Xms1g
-Xmx1g   # 一般更改为内存的一半或者2/3
```

## 查询

```markup
GET _nodes/stats  #查看节点信息，path.data，内存等
GET _cluster/heath #健康检查

/_cat/allocation
/_cat/shards
/_cat/shards/{index}
/_cat/master
/_cat/nodes
/_cat/tasks
/_cat/indices
/_cat/indices/{index}
/_cat/segments
/_cat/segments/{index}
/_cat/count
/_cat/count/{index}
/_cat/recovery   #查看恢复的时间
/_cat/recovery/{index}
/_cat/health
/_cat/pending_tasks
/_cat/aliases
/_cat/aliases/{alias}
/_cat/thread_pool
/_cat/thread_pool/{thread_pools}
/_cat/plugins
/_cat/fielddata
/_cat/fielddata/{fields}
/_cat/nodeattrs
/_cat/repositories
/_cat/snapshots/{repository}
/_cat/templates
```

