---
title: "HAL 链接: 对象CuratedByAgent"
---

## 对象CuratedByAgent

返回 对象 are curated, looked after, or otherwise are in the custody of the 个人或群体.

参见相关的 [模型文档](/model/对象/ownership/#custody)

### 示例

从...的记录中 the Paintings Department of the Rijksmuseum, 的记录 The Night Watch 将在响应中.


### 详情

* 给定类: Agent
* 返回类: HumanMadeObject
* 关系: curatedBy


### SPARQL
```
SELECT DISTINCT ?object WHERE {
   BIND(<%current%> as ?who)
   {
     ?object a crm:E22_Human-Made_Object ; la:member_of ?coll .
     ?coll crm:P16i_was_used_for ?curating .
     ?curating crm:P14_carried_out_by ?who .
    } UNION {
     ?object crm:P50_has_current_keeper ?who .
   }
}
```

