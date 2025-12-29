---
title: "HAL 链接: 作品RepresentsAgent"
---

## 作品RepresentsAgent

返回 visual 作品 represent or depict the 个人或群体.

参见相关的 [模型文档](/model/对象/关于ness/#depiction)

### 示例

从...的记录中 Sarah Hope Harvey Trumbull, 的记录 Sarah Trumbull with a Spaniel 将在响应中.


### 详情

* 给定类: Agent
* 返回类: Work
* 关系: represents


### SPARQL
```
SELECT DISTINCT ?work WHERE {
    BIND (<%current%> AS ?who)
    ?work crm:P138_represents ?who .
 } 
```

