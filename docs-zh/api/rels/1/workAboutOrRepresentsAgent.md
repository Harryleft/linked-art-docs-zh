---
title: "HAL 链接: 作品AboutOrRepresentsAgent"
---

## 作品AboutOrRepresentsAgent

返回 作品 are either 关于 or depict the 个人或群体.

参见相关的 [模型文档](/model/对象/关于ness/#subject)

### 示例

从...的记录中 John Trumbull, the visual items and texts that depict him (such as a bibliographic record and a self-portrait) 将在响应中


### 详情

* 给定类: Agent
* 返回类: Work
* 关系: 关于 / represents


### SPARQL
```
SELECT DISTINCT ?work WHERE {
   {
     ?work crm:P138_represents <%current%>.   }   UNION   {
     ?work crm:P129_is_about <%current%>.   }
}
```

