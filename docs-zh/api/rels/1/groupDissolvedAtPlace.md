---
title: "HAL 链接: groupDissolvedAtPlace"
---

## groupDissolvedAtPlace

返回 groups that were dissolved at the 地点.

参见相关的 [模型文档](/model/actor/#birth-and-death-formation-and-dissolution)

### 示例

从...的记录中 New Haven Connecticut, 的记录 Société Anonyme 将在响应中


### 详情

* 给定类: Place
* 返回类: Group
* 关系: dissolvedAt


### SPARQL
```
SELECT DISTINCT ?group WHERE {
   BIND(<%current%>as ?where)
   ?group crm:P99i_was_dissolved_by ?dissolution .
    ?dissolution crm:P7_took_place_at ?where .
 }
```

