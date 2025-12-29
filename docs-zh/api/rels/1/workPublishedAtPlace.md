---
title: "HAL 链接: 作品PublishedAtPlace"
---

## 作品PublishedAtPlace

返回 作品 were published at the 地点.

参见相关的 [模型文档](/model/document/#creation-and-publication)

### 示例

从...的记录中 Los Angeles, the Getty Exhibition catalog for Pacific Standard Time 将在响应中


### 详情

* 给定类: Place
* 返回类: Work
* 关系: publishedAt


### SPARQL
```
SELECT DISTINCT ?work WHERE {
     BIND(<%current%> as ?where)
     ?activity ^crm:P16i_was_used_for ?work ;         crm:P2_has_type <http://vocab.getty.edu/aat/300054686> ;         crm:P9_consists_of*/crm:P7_took_place_at ?where .
 } 
```

