---
title: "HAL 链接: 对象EncounteredAtPlace"
---

## 对象EncounteredAtPlace

返回 对象 were encountered at the 地点.

参见相关的 [模型文档](/model/对象/production/#discovery-versus-production)

### 示例

从...的记录中 the Burgess Shale, 的记录 Anomalocaris Canadiensis 将在响应中


### 详情

* 给定类: Place
* 返回类: HumanMadeObject
* 关系: encounteredAt


### SPARQL
```
SELECT DISTINCT ?object WHERE {
     BIND(<%current%> as ?where)
     ?object a crm:E22_Human-Made_Object ;         sci:O19i_was_object_found_by/crm:P9_consists_of*/crm:P7_took_place_at ?where .
  }
```

