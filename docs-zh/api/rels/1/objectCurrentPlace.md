---
title: "HAL 链接: 对象CurrentPlace"
---

## 对象CurrentPlace

返回 对象 are, as far as the system knows, currently at the 地点.

参见相关的 [模型文档](/model/对象/ownership/#location)

### 示例

从...的记录中 Getty's gallery W204, 的记录 Jeanne (Spring) 将在响应中


### 详情

* 给定类: Place
* 返回类: HumanMadeObject
* 关系: current


### SPARQL
```
SELECT DISTINCT ?object WHERE {
     BIND(<%current%> as ?where)
     ?object a crm:E22_Human-Made_Object ;         crm:P55_has_current_location ?where }
```

