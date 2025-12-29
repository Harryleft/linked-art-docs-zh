---
title: "HAL 链接: 对象ProductionInfluencedByAgent"
---

## 对象ProductionInfluencedByAgent

返回 对象s whose production was 受...影响 the 个人或群体.

参见相关的 [模型文档](/model/对象/production/#inspirations-studies-or-copies)

### 示例

从...的记录中 Albert Bierstadt, the prints of his 作品s (which were not necessarily created by him) 将在响应中


### 详情

* 给定类: Agent
* 返回类: HumanMadeObject
* 关系: productionInfluencedBy


### SPARQL
```
SELECT DISTINCT ?objects WHERE {
  ?objects crm:P108i_was_produced_by ?production .
  ?production crm:P15_was_influenced_by <%current%>.  }
```

