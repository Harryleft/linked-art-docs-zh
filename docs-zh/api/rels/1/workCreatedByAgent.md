---
title: "HAL 链接: 作品CreatedByAgent"
---

## 作品CreatedByAgent

返回 作品 were created, in whole or in part, by the 个人或群体.

参见相关的 [模型文档](/model/document/#creation-and-publication)

### 示例

从...的记录中 André Chastel, 的记录 The Vatican Frescoes of Michelangelo 将在响应中.


### 详情

* 给定类: Agent
* 返回类: Work
* 关系: createdBy


### SPARQL
```
SELECT DISTINCT ?work WHERE {
   BIND(<%current%> as ?who)
     ?work crm:P94i_was_created_by ?cre .
         ?cre crm:P9_consists_of*/crm:P14_carried_out_by ?who .
 }
```

