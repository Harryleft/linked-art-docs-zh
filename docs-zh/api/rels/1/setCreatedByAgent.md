---
title: "HAL 链接: 集合CreatedByAgent"
---

## 集合CreatedByAgent

返回 集合s or collections that were created, in whole or in part, by the 个人或群体.

参见相关的 [模型文档](/model/collection/#features)

### 示例

从...的记录中 O.C. Marsh, 的记录 his archive 将在响应中


### 详情

* 给定类: Agent
* 返回类: Set
* 关系: createdBy


### SPARQL
```
SELECT DISTINCT ?set WHERE {
   ?set crm:P94i_was_created_by ?creation .
    ?creation crm:P15_was_influenced_by <%current%>. }
```

