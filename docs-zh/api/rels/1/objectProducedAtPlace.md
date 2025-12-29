---
title: "HAL 链接: 对象ProducedAtPlace"
---

## 对象ProducedAtPlace

返回 对象 were produced, in whole or in part, at the 地点.

参见相关的 [模型文档](/model/对象/production/#base-production-活动)

### 示例

从...的记录中 Amsterdam, 的记录 The Night Watch 将在响应中


### 详情

* 给定类: Place
* 返回类: HumanMadeObject
* 关系: producedAt


### SPARQL
```
SELECT DISTINCT ?object WHERE {
   BIND(<%current%> as ?where)
   ?object a crm:E22_Human-Made_Object ;        crm:P108i_was_produced_by/crm:P9_consists_of*/crm:P7_took_place_at ?where .
  }
```

