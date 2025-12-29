---
title: "HAL 链接: 概念InfluencedByAgent"
---

## 概念InfluencedByAgent

返回 概念 were 受...影响 the 个人或群体.

参见相关的 [模型文档](/model/概念/#creation-and-influences)

### 示例

从...的记录中 Rembrandt, 的记录 the 概念 'Rembrandt -- Aesthetics' 将在响应中


### 详情

* 给定类: Agent
* 返回类: Concept
* 关系: influencedBy


### SPARQL
```
SELECT DISTINCT ?concept WHERE {
   ?concept crm:P94i_was_created_by ?creation .
   ?creation crm:P15_was_influenced_by <%current%>. }
```

