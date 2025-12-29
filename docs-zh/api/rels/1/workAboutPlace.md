---
title: "HAL 链接: 作品AboutPlace"
---

## 作品AboutPlace

返回 作品 are 关于 or have a subject of the 地点.

参见相关的 [模型文档](/model/对象/关于ness/#subject)

### 示例

从...的记录中 Paris France, 的记录 Victor Hugo's 作品 "Paris" 将在响应中 


### 详情

* 给定类: Place
* 返回类: Work
* 关系: 关于


### SPARQL
```
SELECT DISTINCT ?work WHERE {
   BIND(<%current%>as ?where)
   ?work crm:P129_is_about ?where .
  }
```

