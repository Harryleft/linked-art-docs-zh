---
title: "HAL 链接: 对象OwnedByAgent"
---

## 对象OwnedByAgent

返回 对象 are 由...拥有 the 个人或群体.

参见相关的 [模型文档](/model/对象/ownership/#ownership)

### 示例

从...的记录中 the Rijksmuseum, 的记录 The Night Watch 将在响应中.


### 详情

* 给定类: Agent
* 返回类: HumanMadeObject
* 关系: ownedBy


### SPARQL
```
SELECT DISTINCT ?object WHERE {
   BIND(<%current%> as ?who)
   ?object a crm:E22_Human-Made_Object ; crm:P52_has_current_owner ?who .
 }
```

