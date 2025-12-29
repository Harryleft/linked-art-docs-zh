---
title: "HAL 链接: activityParticipantAgent"
---

## activityParticipantAgent

返回个人或群体参与但未直接执行的活动。

参见相关的 [模型文档]()

### 示例

从特里斯坦·查拉的记录中，伏尔泰酒馆的记录将在响应中。

### 详情

* 给定类: Agent
* 返回类: Event, Activity
* 关系: participant

### SPARQL
```
SELECT DISTINCT ?activity WHERE {
  ?activity crm:P11_had_participant <%current%>.  }
```