---
description: 亚马逊云的es备份
---

# 备份恢复（AWS）

* 首先您需要确定备份源

```javascript
#假设您需要从自动备份恢复，执行如下命令：
    [root@ec2 logstash]# curl -XGET https://search-xxxxxxxx-xxxxxxxxxx.cn-northwest-1.es.amazonaws.com.cn/_snapshot?pretty
{
  "cs-automated" : {        <-----这个地方是您自动备份的reposity  cs-automated 
    "type" : "s3"
  },
  "es-test" : {
    "type" : "s3",
    "settings" : {
      "bucket" : "jingamz-create",
      "region" : "cn-northwest-1",
      "role_arn" : "arn:aws:iam::536382408000:role/TheSnapshotRole"
    }
  }
  }
```

* 确定 对应reposity的备份中的snapshot

```javascript
 curl -XGET https://search--xxxxxxxx-xxxxxxxxxx.cn-northwest-1.es.amazonaws.com.cn/_snapshot/cs-automated/_all?pretty
   输出类似于如下： 
********
{
  "snapshots" : [ {
    "snapshot" : "2019-10-14t09-47-44.49bb5e15-3c00-40b4-a5d4-c2926594aa92",
    "uuid" : "cZ_SjKrrRoKk8SVqvBUpSQ",
    "version_id" : 7010199,
    "version" : "7.1.1",
    "indices" : [ "mono", "chapter3", "movies", ".kibana_2", ".kibana_3", ".tasks", ".kibana_1", "test_chinese", "chapter1", ".kibana_4" ],
    "include_global_state" : true,
    "state" : "SUCCESS",
    "start_time" : "2019-10-14T09:47:44.145Z",
    "start_time_in_millis" : 1571046464145,
    "end_time" : "2019-10-14T09:47:47.623Z",
    "end_time_in_millis" : 1571046467623,
    "duration_in_millis" : 3478,
    "failures" : [ ],
    "shards" : {
      "total" : 30,
      "failed" : 0,
      "successful" : 30
    }
  }, {
    "snapshot" : "2019-10-14t10-47-45.34d1f1f3-76d1-40c3-b8f4-ecfcb71775d2",   <-----注意这里。
    "uuid" : "F0NjMIeeTMWY54N38IREkw",
    "version_id" : 7010199,
    "version" : "7.1.1",
    "indices" : [ "mono", "chapter3", "movies", ".kibana_2", ".kibana_3", ".tasks", ".kibana_1", "test_chinese", "chapter1", ".kibana_4" ],
    "include_global_state" : true,
    "state" : "SUCCESS",
    "start_time" : "2019-10-14T10:47:45.550Z",
    "start_time_in_millis" : 1571050065550,
    "end_time" : "2019-10-14T10:47:49.301Z",
    "end_time_in_millis" : 1571050069301,
    "duration_in_millis" : 3751,
    "failures" : [ ],
    "shards" : {
      "total" : 30,
      "failed" : 0,
      "successful" : 30
    }
  }
```

* 恢复

```typescript
curl -XPOST https://search-jingamz-f2ibhslaaywlaercaf3tl4vdsm.cn-northwest-1.es.amazonaws.com.cn/_snapshot/cs-automated/2019-10-14t10-47-45.34d1f1f3-76d1-40c3-b8f4-ecfcb71775d2/_restore
```

**注意**：

提醒您一下，如果您使用的AWS自动备份的话， 当ES处在不正常状态的话，自动备份将停止。同时，自动备份只保留15天。 换句话说，如果您的实例处在非正常状态同时超过15天的话，您的自动备份将会消失。 同时，备份只能用于本实例的回复，不能跨ES实例进行回复。 总之，注意时间节点，免得没有有效的备份啊

