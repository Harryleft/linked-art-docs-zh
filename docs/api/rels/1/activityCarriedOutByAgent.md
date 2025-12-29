---
title: "HAL 链接: activityCarriedOutByAgent"
---

## activityCarriedOutByAgent

返回由个人或群体进行的活动。

参见相关的 [模型文档](/model/base/#events-and-activities /model/exhibition/#exhibition-activity)

### 示例

从国家艺术画廊的记录中，马奈展览活动的记录将在响应中


### 详情

* 给定类: Agent
* 返回类: Activity
* 关系: carriedOutBy


### SPARQL
```
SELECT DISTINCT ?activity WHERE {
  BIND (<%current%>AS ?group)
.  ?activity crm:P14_carried_out_by ?group .
   }
```

