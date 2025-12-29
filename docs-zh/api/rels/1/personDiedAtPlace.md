---
title: "HAL 链接: personDiedAtPlace"
---

## personDiedAtPlace

返回 people who died at the 地点.

参见相关的 [模型文档](/model/actor/#birth-and-death-formation-and-dissolution)

### 示例

从...的记录中 Amsterdam, 的记录 Rembrandt 将在响应中


### 详情

* 给定类: Place
* 返回类: Person
* 关系: diedAt


### SPARQL
```
SELECT DISTINCT ?person WHERE {
   BIND(<%current%>as ?where)
   ?person crm:P100i_died_in ?death .
    ?death crm:P7_took_place_at ?where .
 }
```

