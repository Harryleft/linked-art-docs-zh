---
title: "HAL 链接: groupFoundedByAgent"
---

## groupFoundedByAgent

返回 groups that were founded by the 个人或群体.

参见相关的 [模型文档](/model/actor/#birth-and-death-formation-and-dissolution)

### 示例

从...的记录中 Katherine Dreier, Man Ray or Marcel Duchamps, the group Societe Anonyme 将在响应中


### 详情

* 给定类: Agent
* 返回类: Group
* 关系: foundedBy


### SPARQL
```
SELECT DISTINCT ?group WHERE {
   BIND (<%current%>AS ?who)
.   ?group crm:P95i_was_formed_by ?formation .
   ?formation crm:P14_carried_out_by ?who .
 }
```

