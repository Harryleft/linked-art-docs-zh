---
title: 未知类型的转移
up_href: "/model/provenance/"
up_label: "流传历史"
---



## 简介

特别是在处理不完整的文档证据时，往往很难准确确定过去发生了什么类型的交换。对象可能已被出售或以其他方式改变了所有权，也可能只是被借出。虽然理论上可以通过不确定的[财产权利](../rights)转移来处理这种情况，但这会非常复杂，并且给人留下比实际情况信息更多的印象。因此，我们添加了一个名为 `Transfer` 的新类，它允许在双方之间不确定地转移对象，而不声称是所有权、保管权还是其他什么。

## Transfer

不确定转移的类是 `Transfer`，除了核心活动属性外，它还有三个属性：

* **transferred**：引用被转移的一个或多个对象
* **transferred_from**：引用对象转移所来自的一个或多个人或群体
* **transferred_to**：引用对象转移所到达的一个或多个人或群体

这与其他类如 `Acquisition`、`TransferOfCustody` 和 `Move` 相似。

**示例**：

一幅绘画在两个人之间转移，但是不清楚是永久性的还是仅仅是借出。

```crom
top = vocab.ProvenanceEntry(ident="transfer/1", label="Transfer of Painting")
xfer = model.Transfer()
xfer.transferred = model.HumanMadeObject(ident="example", label="Example Painting")
xfer.transferred_from = model.Person(ident="person1", label="Person 1")
xfer.transferred_to = model.Person(ident="person2", label="Person 2")
top.part = xfer
```
