---
title: "HAL 链接: 作品RepresentsPlace"
---

## 作品RepresentsPlace

返回 visual 作品 represent or depict the 地点.

参见相关的 [模型文档](/model/对象/关于ness/#depiction)

### 示例

从...的记录中 Paris France, 的记录 Pissarro's "Boulevard Montmartre at Night" 将在响应中


### 详情

* 给定类: Place
* 返回类: Work
* 关系: represents


### SPARQL
```
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/> SELECT DISTINCT ?work WHERE {
   BIND(<%current%>as ?where)
   ?work crm:P138_represents ?where .
  }
```

