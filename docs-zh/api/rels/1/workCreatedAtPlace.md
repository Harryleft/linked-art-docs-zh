---
title: "HAL 链接: 作品CreatedAtPlace"
---

## 作品CreatedAtPlace

返回 作品 were created, in whole or in part, at the 地点.

参见相关的 [模型文档](/model/document/#creation-and-publication)

### 示例

从...的记录中 Oxford UK, the Lord of the Rings and the Hobbit 将在响应中


### 详情

* 给定类: Place
* 返回类: Work
* 关系: createdAt


### SPARQL
```
SELECT DISTINCT ?work WHERE {
   BIND(<%current%> as ?where)
   ?work crm:P94i_was_created_by/crm:P9_consists_of*/crm:P7_took_place_at ?where .
  }
```

