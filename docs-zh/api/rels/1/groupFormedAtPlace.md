---
title: "HAL 链接: groupFormedAtPlace"
---

## groupFormedAtPlace

返回 groups that were formed at the 地点.

参见相关的 [模型文档](/model/actor/#birth-and-death-formation-and-dissolution)

### 示例

从...的记录中 Los Altos California, 的记录 Apple Computers 将在响应中


### 详情

* 给定类: Place
* 返回类: Group
* 关系: formedAt


### SPARQL
```
SELECT DISTINCT ?group WHERE {
   BIND(<%current%>as ?where)
   ?group crm:P95i_was_formed_by ?formation .
    ?formation crm:P7_took_place_at ?where .
 }
```

