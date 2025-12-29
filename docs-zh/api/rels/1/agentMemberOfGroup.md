---
title: "HAL 链接: 行动者MemberOfGroup"
---

## 行动者MemberOfGroup

返回 people or groups that are members of the group.

参见相关的 [模型文档](/model/actor/#organization-membership)

### 示例

从...的记录中 Societe Anonyme, Katherine Dreier and Fortunato Depero would all be in the response


### 详情

* 给定类: Group
* 返回类: Agent
* 关系: memberOf


### SPARQL
```
SELECT DISTINCT ?member WHERE {
   BIND (<%current%> AS ?group)
.   ?member crm:P107i_is_current_or_former_member_of ?group .
 }
```

