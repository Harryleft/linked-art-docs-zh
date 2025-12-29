---
title: "HAL 链接: 作品PublishedByAgent"
---

## 作品PublishedByAgent

返回 作品 are published by the 个人或群体.

参见相关的 [模型文档](/model/document/#creation-and-publication)

### 示例

从...的记录中 Bloomsbury Publishing, 的记录 Alias Grace 将在响应中.


### 详情

* 给定类: Agent
* 返回类: Work
* 关系: publishedBy


### SPARQL
```
SELECT DISTINCT ?work WHERE {
    BIND(<%current%> AS ?who)
     ?work crm:P16i_was_used_for ?pub .
    ?pub crm:P14_carried_out_by ?who .
 } 
```

