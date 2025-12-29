---
title: "时间上下文：时期、事件和活动"
---



## 概述

我们关心的大多数事件、活动和其他时间方面都直接与对象、个人和其他实体相关。这些包括将实体带入存在的活动（制作、创作、出生和成立），将它们带出存在（毁坏、消除、解散）或以其他方式显著影响它们在文化记录中出现的情况（何时被发现、它们的出版、个人的专业活动）。有两类广泛的活动有其自己的特定模型——对象的[流传历史](../provenance/)或所有权历史，以及[展览](../exhibition/)。

还有时间段、事件和个人进行的活动，它们为对象提供额外的上下文，但不直接与它们绑定。这些类型的时间实体将包括时间段（白垩纪、青铜时代、17世纪）、发生但不是由人有意图执行的事件（维苏威火山爆发、伦敦大火、COVID-19大流行），以及由个人进行的活动（第一次Linked Art面对面会议、登月、斯科特的南极之旅）。模型的这部分关注后几种类型，因为它们与对象分离，就像个人、地点和概念一样。

## 类型

如上所述，有三种时间实体类型：

* **Period（时期）**：一段时间，可能是某种程度上任意定义的，如"时代"或世纪。
* **Event（事件）**：发生然后结束的事件，通常以某种方式改变世界的状态。
* **Activity（活动）**：由个人或群体有意或故意执行的事件。

这些类型或类在模型中记录在 `type` 中。

**示例：**

19世纪是从1800年到1899年底的时期。

```crom
top = model.Period(ident="19c/1", label="19th Century")
top.identified_by = vocab.PrimaryName(content="19th Century")
ts = model.TimeSpan()
ts.begin_of_the_begin = "1800-01-01T00:00:00Z"
ts.end_of_the_end = "1899-12-31T23:59:59Z"
top.timespan = ts
```

## 共同特征

实体的所有共同特征都可用于事件，包括为事件或活动专门定义的特征，如由另一个事件引起，如下面更详细描述的，由个人或群体执行等等。

## 原因

事件和活动可以由前面的事件或活动引起，例如庞贝的毁坏是由维苏威火山爆发引起的。维苏威火山爆发将是一个事件，使用 `caused_by` 属性从庞贝（物理）城市的毁坏事件中引用。维苏威火山爆发也在许多绘画中描绘，是许多书籍的主题。因此，它必须有自己的记录，以便对象、作品和事件可以引用同一个实体。

**示例：**

维苏威火山于公元79年8月24日爆发。

```crom
top = model.Event(ident="vesuvius/1", label="Eruption of Vesuvius")
top.identified_by = vocab.PrimaryName(content="Eruption of Vesuvius")
top.took_place_at = model.Place(ident="vesuvius", label="Mount Vesuvius")
ts = model.TimeSpan()
ts.begin_of_the_begin = "0079-08-24T12:00:00Z"
ts.end_of_the_end = "0079-08-26T23:59:59Z"
top.timespan = ts
```

并且是庞贝城毁坏的原因。

```crom
top = model.HumanMadeObject(ident="pompeii-buildings/1", label="Buildings making up the city of Pompeii")
top.identified_by = vocab.PrimaryName(content="City of Pompeii")
dest = model.Destruction()
dest.caused_by = model.Event(ident="vesuvius")
top.destroyed_by = dest
```

## During与Part Of

有两种关系描述事件如何在分区或包含方面相互关联：`part_of` 和 `during`。每个都有特定的用法，应该仔细遵守，否则搜索和用户界面将变得非常混乱和复杂。

首先，如果一个事件是另一个事件的严格部分，如果你列出所有部分，那么整个整体将被完整描述，那么使用的正确属性是 `part_of`。例如，青铜时代由早期青铜时代、中期青铜时代和晚期青铜时代组成。这些中的每一个都可能进一步细分为时期的层次结构。

相反，如果我们知道一个文物是在青铜时代创造的，我们不会将其与其部分一起列出。关系是包含关系，而不是严格的分区，并且通常是对未知和更明确时间范围的替代，或者是在更广泛上下文期间对发生活动或事件进行分类或分组的方法。例如，文物的制作活动发生在青铜时代时期`期间`，但不是像上面列出的那些组成部分之一。

**示例：**

早期罗马帝国时期，从公元前31年到公元193年，是罗马帝国时期的一部分。

```crom
top = model.Period(ident="early_roman/1", label="Early Roman Empire (31 BCE - 193 CE)")
top.identified_by = vocab.PrimaryName(content="Early Roman Empire")
top.part_of = model.Period(ident="roman", label="Roman Empire")

```

维苏威火山在这个时期爆发。

```crom
top = model.Event(ident="vesuvius/2", label="Eruption of Vesuvius")
top.identified_by = vocab.PrimaryName(content="Eruption of Vesuvius")
top.during = model.Period(ident="early_roman", label="Early Roman Empire")
```

## 相对时间

有时我们有活动或事件相对于彼此的顺序，但没有它们发生的具体时间。例如，我们可能从文档证据中知道一个对象是在某个事件之前创造的，但只有这两个活动发生的最模糊的时间段。我们可以使用属性 `before`（具有属性的事件在属性值的事件之前发生）和 `after`（相反）来描述事件之间的顺序。这对于流传历史活动特别有用，以便形成事件的有序序列，而不知道销售的日期。

**示例：**

庞贝的一座雕像必须在维苏威火山爆发之前创造。

```crom
top = model.HumanMadeObject(ident="pompeii_statue/1", label="Statue in Pompeii")
top.identified_by = vocab.PrimaryName(content="Pompeii Statue")
prod = model.Production()
prod.before = model.Event(ident="vesuvius", label="Eruption of Vesuvius")
top.produced_by = prod
```