---
title: 对象流传历史
up_href: "/model/"
up_label: "模型概述"
---



## 概述

描述对象流传历史的一般模型是追踪关注对象被创建或发现、在所有者或保管人之间转移的事件，直到它丢失、毁坏或到达其当前位置。例如，一幅画的流传历史从艺术家绘制它时开始，然后有事件将画的所有权从艺术家转移到其第一个所有者，然后再转移到后续所有者。这些转移的细节是要在模型流传历史部分收集的主要数据。

在事件之间，所有权不发生变化的时间段，但可能仍然发生其他有趣的事件，包括保管权的变更，如画被借出用于[展览](../exhibition/)、[保护](../conservation/)、重新评估或其他会建立对象在某个时间点位置和所有权的活动。

对象的流传历史被描述为一系列活动，建立在基础模式之上。对于流传历史链中的单个条目，经常有多个活动捆绑在一起形成一个感兴趣的"流传历史事件"。这些捆绑的活动可能是所有权的转移、保管权的转移、对象的物理移动、金钱支付或某些未来行动的承诺。本节记录了描述流传历史事件的基本框架，后续章节将记录具体的用例。

事件链从对象的创作者制作对象开始，仅在其毁坏时结束。由于每种只能有一个，它们专注于对象而不是活动，并有不同的模式。此信息在模型的[对象](/model/object/production/)部分涵盖，因为虽然这些事件是对象生命周期的一部分，但它们的建模方式与其他流传历史事件不同。

## 流传历史事件

流传历史事件是包装活动，代表几个更细粒度事件发生的上下文，并代表在链中跟踪的总体事件，而不是影响一个或多个对象的具体法律和物理变化。例如，用一个对象交换另一个对象是单个流传历史条目，涉及两个对象的所有权转移，因此该事件将出现在两个对象的时间线中。它还可能伴随着额外的金钱支付、活动承诺或其他贡献。

流传历史事件具有所有常规属性和关系，如[基线模式](/model/base/)中所述。特别是，与行动者、地点和时间的关系反映了总体事件，如果它们不同且已知，可以在单独的部分中进一步指定。

**示例：**

爱德华·马奈于1883年以3,000法郎将他的画《Jeanne》卖给Antonin Proust。

```crom
top = vocab.ProvenanceEntry(ident="manet_proust/1", label="Purchase of Spring by Proust")
top.identified_by = vocab.PrimaryName(content="Purchase of Spring by Proust from Manet")

ts = model.TimeSpan()
ts.begin_of_the_begin = "1881-01-01T00:00:00Z"
ts.end_of_the_end = "1883-12-31T23:59:59Z"
top.timespan = ts

acq = model.Acquisition(label="Ownership of Spring to Proust")
top.part = acq
acq.transferred_title_of = model.HumanMadeObject(ident="spring", label="Spring")
acq.transferred_title_from = model.Person(ident="manet", label="Manet")
acq.transferred_title_to = model.Person(ident="proust", label="Proust")

pay = model.Payment(label="3000 Francs to Manet")
pay.paid_from = model.Person(ident="proust", label="Proust")
pay.paid_to = model.Person(ident="manet", label="Manet")
amnt = model.MonetaryAmount()
amnt.currency = vocab.instances['fr francs']
amnt.value = 3000
pay.paid_amount = amnt
top.part = pay
```


### 分类

有许多不同类型的流传历史活动可以用此模型涵盖，从简单的购买到用金钱交换对象，或更复杂的捐赠、承诺赠与、遗赠等等。这些分类应该添加到活动中以阐明特定事件。

**示例：**

徐子蔚于1999年将她的画"风景"赠送给耶鲁大学艺术画廊

```crom
top = vocab.ProvenanceEntry(ident="ziwei_yuag/1", label="Gift of Landscape to YUAG")
top.classified_as = model.Type(ident="http://vocab.getty.edu/aat/300417637", label="Gift")
ts = model.TimeSpan()
ts.begin_of_the_begin = "1999-01-01T00:00:00Z"
ts.end_of_the_end = "1999-12-31T23:59:59Z"
top.timespan = ts
acq = model.Acquisition(label="Acquisition of Painting 1")
acq.transferred_title_of = model.HumanMadeObject(ident="ziwei_landscape", label="Landscape")
acq.transferred_title_to = model.Group(ident="yuag", label="Yale University Art Gallery")
acq.transferred_title_from = model.Person(ident="ziwei", label="Xu Ziwei")
top.part = acq
```

### 相对时间

在描述历史事件时，可能无法给出活动发生的任何有用时间范围，只能将其与在另一个事件之前或之后发生相关联。这允许活动在事件链中排序，而不明确任何日期范围。

流传历史活动有两个属性来覆盖这种情况：`after`（此事件在引用事件结束后开始，因此引用事件是在具有 `after` 属性的事件之前）和 `before`（此事件在引用事件开始前结束，因此引用事件是在当前事件之后）。具有属性的事件是在属性引用的事件之后或之前。


**示例：**

Jean-Baptise Faure在Proust之后拥有《春天》（但不一定直接从Proust获得），在1907年将其转移给Durand-Ruel画廊（巴黎）之前。

```crom
top = vocab.ProvenanceEntry(ident="unknown_faure/1", label="Unknown Acquisition of Spring by Faure")
top.after = vocab.ProvenanceEntry(ident="manet_proust")
top.before = vocab.ProvenanceEntry(label="foure_durand")
```


## 部分

流传历史事件可能包括一些数量的进一步、更具体的方面。这些方面在以下链接的部分中有更详细的描述。


### 获得与支付

大多数流传历史事件包括对象的所有权变更，或其获得。许多这些获得涉及金钱支付，或另一个对象的交换，以转移所有权——购买而不是赠与。

这些类型的流传历史事件在[获得](acquisition)部分记录。

### 保管权转移

也有不涉及法律所有权转移的流传历史事件，只涉及保管权或监护权的转移。此用例包括永久借展，可能看起来像所有权，以及临时借展，如展览用。盗窃或掠夺都是非法的保管权转移，因为对象应该归还给其合法所有者，对象的简单丢失是向没有任何特定实体的保管权转移。

这些类型的流传历史事件在[保管权](custody)部分记录。

### 对象的发现或重新发现

对象可能丢失，有时是很长的时间，然后被与丢失它的不同文化或人群遇到。由于这可能发生在对象的历史中几次，并且重新发现具有所有权和保管权含义，这种相遇是对象流传历史记录的一部分。关于先前相遇或对象制作的知识可能不知道，这意味着这可能是流传历史链中第一个已知条目。

这些类型的流传历史事件在[遇到对象](encounters)部分记录。

### 权利的获得

一些所有权转移比简单地获得对象更复杂，涉及所有权份额的转移，可能在一组所有者网络中随时间交易。在这种情况下，有必要建模所有权权利，以及它如何被分割和管理。此模式重要的其他场景是当获得的"东西"不是物理对象，而是知识产权权利，如表演戏剧作品或其他基于时间的媒体的权利。

请注意，本节很复杂，可能只对专门的流传历史数据库有价值。欢迎提供反馈以改进其在表示非物理所有权转移方面的可用性和准确性。

这些类型的流传历史事件在[权利](rights)部分记录。

### 活动的承诺

活动的承诺作为流传历史事件的一部分捕获也很有趣。这包括对象借给组织，但有根据某些条件未来将给予所有权的承诺的情况。同样，委托对象涉及艺术家创作艺术品的承诺，可能涉及借出物品以复制或获得灵感，以及财务补偿的预付款。最后，拍卖中的出价是如果是最高出价则获得对象（或对象）的承诺。

承诺在[承诺](promises)部分记录，出价是此的拍卖特定用途，在[拍卖](auctions)部分记录。

### 对象移动

虽然通常没有明确记录，但大多数流传历史活动也涉及获得对象的物理重新定位。这对于描述展览特别有趣，其中位置在一段时间内明确已知，或者在这种移动以某种方式非凡的情况下，如建筑物或其他"不可移动"艺术品的重新定位。

这些类型的流传历史事件在[移动](movement)部分记录。

### 未知类型的转移

当处理不完整的文档证据时，经常很难准确确定过去发生了什么类型的交换。例如，档案或信件可能说对象"去了博物馆"，这不足以区分所有权转移、保管权转移，或仅仅是对象的物理移动。虽然每当可能时都应该努力在流传历史文档中精确，但捕获不确定的活动也很重要。

这些类型的流传历史事件在[转移](transfer)部分记录。


## 特定用途

有一些常见的场景可以用Linked Art的流传历史建模描述，有一些额外的词汇以确保精确：

* [拍卖](auctions)