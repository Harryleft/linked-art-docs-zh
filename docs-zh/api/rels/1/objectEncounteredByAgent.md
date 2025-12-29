---
title: "HAL 链接: 对象EncounteredByAgent"
---

## 对象EncounteredByAgent

返回 对象 were discovered or encountered by the 个人或群体.

参见相关的 [模型文档](/model/对象/production/#discovery-versus-production)

### 示例

从...的记录中 O.C. Marsh, 的记录 the Torosaurus holotype 将在响应中


### 详情

* 给定类: Agent
* 返回类: HumanMadeObject
* 关系: encounteredBy


### SPARQL
```
SELECT DISTINCT ?object WHERE {
   BIND(<%current%> as ?who)
   ?object a crm:E22_Human-Made_Object ; sci:O19i_was_object_encountered_at ?enc .
   ?enc crm:P9_consists_of*/crm:P14_carried_out_by ?who .
  }
```

