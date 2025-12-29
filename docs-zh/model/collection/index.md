---
title: "藏品集合与集合"
---



## 概述

有许多用例需要将实体分组在一起，通常是相同类别的，但有时是不同类型的。这些用例在下面的部分中举例说明，范围从拍卖批次中的对象集合，到经销商库存和博物馆藏品、展览、相关概念集合，或共享共同特征（如性别或国籍）的人群集合。

为了用一致的模式覆盖所有用例，我们引入了一个来自CIDOC-CRM外的新 `Set` 类。这避免了具有不同类型的实体集合的问题，以及对象和集合身份的语义。如果将来在核心CIDOC-CRM本体中添加等价的类，规范的新主要版本可能会改变使用它。


## 特征

集合是概念性分组，而不是物理分组。虚拟展览中的对象集合或简单的人员喜爱对象集合永远不会因为成为或不成为集合的一部分而改变其物理状态。一个人可能有一个被毁坏对象的集合，如果集合是不再存在的东西的物理聚合，那将是非常奇怪的。因此，集合是通过 `Creation` 创建的，而不是通过 `Production`，并且不能被销毁。集合在任何给定时间点可能有零个成员而不会停止存在。

像任何核心实体一样，`Set` 的实例必须有 `id` 和 `type`，可能有额外的分类，并且可以有标识符和名称。可以有关于它们的断言，最重要的是可以有成员实体。

集合的成员实体通过成员实体的 `member_of` 属性包含，该属性的值为 `Set` 的URI。理论上，成员可以是任何类，但是Linked Art API限制仅为核心实体类型。这意味着关于成员的信息发布者需要包含到 `Set` 实例的 `member_of` 属性。在两者都在同一环境中管理的情况下这不是问题，在模型中概念上也不是挑战（有反向的 `member` 属性），但是API不允许集合引用它们的成员，遵循与群体不引用它们的成员、对象不引用它们的部分相同的设计原则。这也意味着成员必须是规范中可以独立作为[记录](/api/1.0/endpoint/)的主要类之一，如 `HumanMadeObject` 或 `Activity`，而不是只在记录中使用的类，如 `Production` 或 `Name`，因为没有找到封装记录的方法。

**示例：**

展览中的对象集合。

```crom
top = model.Set(ident="exhset/1", label="Exhibition objects")
top.identified_by = vocab.PrimaryName(content="Objects in Manet and Modern Beauty")
top.referred_to_by = vocab.Description(content="Objects in the exhibition Manet and Modern Beauty at the Art Institute of Chicago and the Getty Museum")
cre = model.Creation()
ts = model.TimeSpan()
ts.begin_of_the_begin = "2019-05-01"
ts.end_of_the_end = "2019-05-01"
cre.timespan = ts
top.created_by = cre
```

该集合中的一个对象。

```crom
top = vocab.Painting(ident="spring/13", label="Jeanne (Spring) by Manet")
top.identified_by = model.Name(content="Jeanne (Spring)")
top.member_of = model.Set(ident="exhset")
```

### 成员顺序

为了确保成员正确排序，可以将排序值作为标识符添加到成员上。这个值应该相对于集合的其他成员正确排序，字母数字最低的标识符值首先呈现，然后从那里按升序排列。这个标识符可能有一个与之关联的 `AttributeAssignment`，该分配被应应用排序值的集合 `influenced_by`。这允许同一实体同时成为多个有序集合的成员。

**示例：**

在[档案用例](/model/archives/#archival-hierarchy)中描述的Obermeyer信件应该在Stieglitz家庭信件集合中排序为"000001"。

```crom
top = model.HumanMadeObject(ident="letter/2", label="Obermeyer 1920")
top.identified_by = vocab.PrimaryName(content="Obermeyer, Bertha (1920)")
sv = vocab.SortValue(content="000001")
aa = model.AttributeAssignment()
aa.influenced_by = model.Set(ident="archive_sfl", label="Stieglitz Family Letters")
sv.assigned_by = aa
top.identified_by = sv
top.member_of = model.Set(ident="archive_sfl", label="Stieglitz Family Letters")
```

### 原型成员

关于集合中任何特定成员的信息可能不可用，但是可能知道关于集合中实体的通用信息。例如，特定集合中的对象可能由同一个人创作，被分类为相同类型，或者有相同的所有者。作品可能用相同语言编写，关于相同主题等等。由于任何实体都可以成为集合的成员，这为描述被分组在一起的事物类型提供了很大的自由度。这对于档案经常是真实的，但对于使集合的基本原理更明显也很有价值，例如绘画部门策展的对象（通常）是绘画。

原型成员的描述嵌入在集合中作为 `members_exemplified_by` 属性的值。

这不是集合的"重点"成员，如对象集合中的著名作品。为此，使用[相关对象](/model/assertion/)模式。使用这种方法并不意味着集合的*每个*成员都具有原型成员的所有特征，但是应该注意不要包含通常不真实的信息。

**示例：**

展览的对象通常是（但不排除）马奈的绘画。

```crom
top = model.Set(ident="exhset/2", label="Exhibition objects")
hmo = vocab.Painting()
prod = model.Production()
prod.carried_out_by = model.Person(ident="http://vocab.getty.edu/ulan/500010363", label="Manet")
hmo.produced_by = prod
top.members_exemplified_by = hmo
```

## 对象集合

集合可以用来描述构成策展藏品的对象集合。这不一定与机构拥有的对象集合相同，因为可能有由其他组织或个人拥有但由机构照看的对象，也不是机构目前拥有保管权的对象集合，因为借给其他组织展览的对象仍然是概念性对象集合的一部分。对象与机构之间的关系细节记录在对象上，而集合为藏品本身提供身份，独立于成员对象。对象可以同时成为多个集合的一部分——私人所有者的个人收藏和博物馆的公共收藏。因此虽然大多数对象都是由机构拥有并由其保管，但这不是确定的，不应该被推断。

机构经常被分成部门，每个部门将管理整体藏品的一部分。这些藏品部分作为单独的集合管理，而不是以某种方式在单个集合内。部门藏品可能是机构藏品的成员，就像部门是组织的 `member_of` 一样。能够描述对象在每个上下文中的属性是很有用的，并允许从组织图表中分离的库存管理结构。部门也可能构思他们对象的进一步集合，没有任何直接对应关系，很可能同一个对象同时成为多个集合的一部分。

**示例：**

国家博物馆的完整藏品。

```crom
top = vocab.CollectionSet(ident="rijks_objects/1", label="Collection of the Rijksmuseum")
top.identified_by = vocab.PrimaryName(content="Collection of the Rijksmuseum")
```

国家博物馆的绘画，由绘画部门策展。

```crom
top = vocab.CollectionSet(ident="rijks_paintings/1", label="Paintings of the Rijksmuseum")
top.identified_by = vocab.PrimaryName(content="Paintings of the Rijksmuseum")
top.member_of = model.Set(ident="rijks_objects", label="Collection of the Rijksmuseum")
cur = vocab.Curating()
cur.carried_out_by = model.Group("rijks_paintings_dept", label="Paintings Department")
top.used_for = cur
```

夜巡是绘画集合的成员。

```crom
top = vocab.Painting(ident="nightwatch/16", label="Night Watch by Rembrandt")
top.identified_by = vocab.PrimaryName(content="The Night Watch")
top.member_of = model.Set(ident="rijks_paintings", label="Paintings of the Rijksmuseum")
```


## 其他用例

### 人群集合

群体是其他 `Group` 和 `Person` 的集合，可以采取行动。这意味着集合的特征也可用于群体，如 `members_exemplified_by`。这允许我们具体说明大型群体的原型成员，如国籍或"未识别"人员。

/// warning
Set是Group的新超类仅在使用Linked Art本体时成立，在CIDOC-CRM基础本体中不成立，因为Linked Art引入了Set的概念。
///


**示例：**

"14世纪意大利人"群体的原型成员是在1300年至1400年间在意大利出生的人。

```crom
top = model.Group(ident="14thc_italian/1", label="14th c italians")
top.identified_by = vocab.PrimaryName(content="Unidentified 14th Century Italian")
p = model.Person()
b = model.Birth()
ts = model.TimeSpan()
ts.begin_of_the_begin = "1300-01-01T00:00:00Z"
ts.end_of_the_end = "1399-12-31T00:00:00Z"
b.timespan = ts
b.took_place_at = model.Place(ident="https://vocab.getty.edu/tgn/1000080", label="Italy")
p.born = b
top.members_exemplified_by = p
```

### 档案

Set类广泛用于建模[档案](/model/archives/)。

### 拍卖批次

[拍卖批次](/model/provenance/auctions.html#set-of-objects)中的对象集合也被建模为集合。这些不像博物馆藏品那样策展，不一定曾经物理聚集在一起，甚至可能不是物理的而是数字对象，但作为单一实体被拍卖。同样，[展览](/model/exhibition/#objects)中使用的对象集合也被建模为集合。

### 藏品特定信息

关于实体特定于它们所属集合上下文的信息，如对象对于该特定藏品的入藏号，可以使用关于[断言](/model/assertion/#context-specific-assertions)页面中描述的 `AttributeAssignment` 模式来描述，方式与上面描述的集合内排序值相同。