---
title: "HAL 链接: 作品AboutAgent"
---

## 作品AboutAgent

返回 作品 are 关于 or have a subject of the 个人或群体.

参见相关的 [模型文档](/model/对象/关于ness/#subject)

### 示例

从...的记录中 Abraham Lincoln, 的记录 We are Lincoln Men : Abraham Lincoln and his Friends 将在响应中.


### 详情

* 给定类: Agent
* 返回类: Work
* 关系: 关于


### SPARQL
```
SELECT DISTINCT ?work WHERE {
    BIND(<%current%> AS ?who)
    ?work crm:P129_is_about ?who .
 } 
```

