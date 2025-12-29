---
title: "HAL 链接: personBornAtPlace"
---

## personBornAtPlace

返回 people who were born at the 地点.

参见相关的 [模型文档](/model/actor/#birth-and-death-formation-and-dissolution)

### 示例

从...的记录中 Leiden, 的记录 Rembrandt 将在响应中


### 详情

* 给定类: Place
* 返回类: Person
* 关系: bornAt


### SPARQL
```
SELECT DISTINCT ?agent WHERE {
   BIND(<%current%>as ?where)
   ?agent crm:P98i_was_born ?birth .
    ?birth crm:P7_took_place_at ?where .
 }
```

