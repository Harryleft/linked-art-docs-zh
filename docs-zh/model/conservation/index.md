---
title: "保护活动"
up_href: "/model/"
up_label: "模型概述"
---


## 概述

本节描述如何建模关于作为对象护理和保护工作一部分而进行的活动信息。特别是，有状态评估、保护活动和保护项目，后者包含前两者。状态评估是策展人或保护员评估对象状态以及需要保护干预程度的时候。保护活动是对对象的物理修改以改善其状态。

Linked.Art 模型的其他部分也与保护相关：

* [断言](/model/base/#statements-about-an-entity)可以关于对象的状态或保护相关活动
* 采样活动在[通过移除的制作](/model/object/production/#production-by-removal)下描述


## 状态评估

状态评估描述了一个活动，在此期间检查对象并确定其保存状况或损坏类型。状况类型被分配为对象的分类。

**示例：**

阿姆斯特丹国家博物馆在"夜巡行动"项目开始时检查了《夜巡》的状况。

```crom
top = vocab.Painting(ident="nightwatch/25", label="夜巡")
aa = model.AttributeAssignment(label="夜巡状态评估")
top.attributed_by = aa
ts = model.TimeSpan()
ts.begin_of_the_begin = "2019-05-01T00:00:00Z"
ts.end_of_the_end = "2019-09-30T23:59:59Z"
aa.timespan = ts
actor = model.Group(ident="rijksmuseum", label="阿姆斯特丹国家博物馆")
aa.carried_out_by = actor
aa.identified_by = model.Name(content="全面状态评估")
aa.assigned_property = "classified_as"
aa.referred_to_by = vocab.Description(content = "整个绘画表面非常细小的裂纹")
aa.assigned = model.Type(ident="http://vocab.getty.edu/aat/300387447", label="微裂纹")
aa.part_of = model.Activity(ident="operation_nightwatch", label="夜巡行动")
```

## 保护活动

保护活动指的是在展览前对对象进行的或以防止对象恶化为目标的活动。

**示例：**

对《夜巡》进行了轻微的保护改进。

```crom
top = vocab.Painting(ident="nightwatch/26", label="夜巡")
mod = model.Modification(label="夜巡保护")
top.modified_by = mod
ts = model.TimeSpan()
ts.begin_of_the_begin = "2020-01-01T00:00:00Z"
ts.end_of_the_end = "2021-12-31T23:59:59Z"
mod.timespan = ts
mod.carried_out_by = model.Group(ident="rijksmuseum", label="阿姆斯特丹国家博物馆")
mod.referred_to_by = vocab.Description(content="针对早期调查的轻微保护工作")
mod.technique = model.Type(ident="http://vocab.getty.edu/aat/300053027", label="清洁")
mod.part_of = model.Activity(ident="operation_nightwatch", label="夜巡行动")
```


## 保护项目

保护项目是包装活动，表示更细化事件的上下文，并代表在链中跟踪的整体事件，而不是影响一个或多个对象的具体法律和物理变更。例如，涉及检查多个对象的收藏状态检查，或以状态检查开始并继续进行干预性保护工作的保护活动。

保护项目具有所有常规属性和关系，如[基线模式](/model/base/)中所记录。特别是，与行动者、地点和时间的关系反映了整体事件。

**示例：**

夜巡行动是关于《夜巡》的保护和研究项目

```crom
top = vocab.Conserving(ident="operation_nightwatch/1", label="保护项目")
top.identified_by = vocab.PrimaryName(content="夜巡行动")
top.carried_out_by = model.Group(ident="rijksmuseum", label="阿姆斯特丹国家博物馆")
top.carried_out_by = model.Group(ident="akzonobel", label="阿克苏诺贝尔")
ts = model.TimeSpan()
ts.begin_of_the_begin = "2019-01-01T00:00:00Z"
ts.end_of_the_end = "2023-12-31T23:59:59Z"
top.timespan = ts
top.referred_to_by = vocab.Description(content="夜巡行动是有史以来对伦勃朗最著名绘画进行的最大规模和最广泛的研究。")
```