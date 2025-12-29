---
title: "对象：来源"
up_href: "/model/object/"
up_label: "对象"
---



## 简介

追踪对象的来源在模型的[来源](/model/provenance)部分有详细描述。这种详细程度的记录通常不是所有对象都可用的，并且在对象记录中直接拥有对象的所有权、保管和位置的当前信息是有益的。

即使对于对象有详细的所有权历史记录，这些记录仍然可能限于谁拥有它、何时以及如何获得它的基本信息。获得也可能是对象本身的，支付或交换的内容很少能够发布。对于这99%的情况，所有权转移可以在对象记录中列出，而不是在单独的来源记录中，但如果存在可以链接到它们。此模式**不**扩展到保管或位置的变化。


## 当前和正常所有者、保管者和位置

### 所有权

对象的当前所有者应该在最最近`Acquisition`中用`transferred_title_to`引用，该`Acquisition``transferred_title_of`对象。这些转移在来源模型的[获得](/model/provenance/acquisition)部分有详细描述，以及在下面对象记录中描述的简化版本中。

为了使当前所有者在数据中更容易找到，所有者也应该从对象本身用`current_owner`引用。关于可能拥有对象的[人和组织](/model/actor)有更多建模细节可用。

**示例**：

《春天》的当前所有者是盖蒂。

```crom
top = model.HumanMadeObject(ident="spring/6", label="马奈的珍妮（春天）")
top.current_owner = model.Group(ident="http://vocab.getty.edu/ulan/500115988", label="盖蒂博物馆")
```

### 保管

类似地，对象的当前保管者应该在最最近的`TransferOfCustody`中用`transferred_custody_to`引用，方式与当前所有者从最最近`Acquisition`引用相同。与`current_owner`等效的保管属性是`current_custodian`。保管转移在[保管](/model/provenance/custody)部分有更详细的描述。

如果有部门或个人不是所有者但负责对象，那么该行动者是`current_custodian`。类似地，组织之间的出借（无论是临时还是永久）转移的是保管而不是所有权。

**示例**：

《夜巡》由阿姆斯特丹市拥有，永久出借给国家博物馆。

```crom
top = vocab.Painting(ident="nightwatch/14",label="绘画", art=1)
top.current_owner = model.Group(ident="amsterdam_govt", label="阿姆斯特丹市政府")
top.current_custodian = model.Group(ident="http://vocab.getty.edu/ulan/500246547", label="国家博物馆")
```

#### 正常保管者

当对象临时出借给另一个组织时，例如为了展览，那么当前所有者不会改变，但当前保管者会改变。在这种情况下，当对象的通常或正常保管者与当前保管者不同时，知道对象通常或正常保管者是谁是有用的。例如，如果（考虑到绘画的现实世界尺寸，这是一个非常大的"如果"）《夜巡》曾经出借给另一个组织，那么所有者将保持为城市，当前保管者将是展览组织，而国家博物馆将保持为正常保管者。这使用一个名为`current_permanent_custodian`的属性。

**示例**：

《夜巡》也（完全假设地）出借给盖蒂博物馆。

```crom
top = vocab.Painting(ident="nightwatch/17",label="绘画", art=1)
top.current_owner = model.Group(ident="amsterdam_govt", label="阿姆斯特丹市政府")
top.current_permanent_custodian = model.Group(ident="http://vocab.getty.edu/ulan/500246547", label="国家博物馆")
top.current_custodian = model.Group(ident="http://vocab.getty.edu/ulan/500115988", label="盖蒂博物馆")
```


### 位置

对象的当前位置使用`current_location`属性给出。这可以引用画廊或设施的特定部分，或用于对象当前持有的组织的一般位置。关于[地点](/model/place/)有更多建模细节可用。

**示例**：

《春天》的当前位置是W204画廊（这是西馆的一部分，西馆是盖蒂中心的一部分）

```crom
top = model.HumanMadeObject(ident="spring/7", label="马奈的珍妮（春天）")
top.current_location = model.Place(ident="W204", label="W204画廊")
```

#### 正常位置

类似于当前与正常保管者，对象也可能有相对于当前位置的正常位置。对象可能不在其通常位置，因为被移除进行保护工作，因为它为展览而移动，或由于画廊轮换。模型使用与正常保管者相同的模式，使用`current_permanent_location`属性。

**示例**：

《春天》（也假设地）当前在另一个画廊进行展览。

```crom
top = model.HumanMadeObject(ident="spring/14", label="马奈的珍妮（春天）")
top.current_permanent_location = model.Place(ident="W204", label="W204画廊")
top.current_location = model.Place(ident="E100", label="展览画廊100")
```


## 简单历史所有权

所有者列表可以使用`changed_ownership_through`属性直接在对象记录中提供。这传达了所有权变更的获得列表（**不是**完整的来源事件）。获得应该按照它们应该显示的模型结果序列化顺序，例如如果遵循Linked Art API，在JSON-LD数组中的正确顺序。如果有完整的来源活动记录，那么这些可以通过获得中的`part_of`属性引用。

否则，所有常规事件属性和关系都可用于使用。

**示例**：

《春天》从马奈转移到普鲁斯特，然后后来从杜兰-鲁埃尔画廊转移到佩恩。
（完整的转移集合将在真实记录中给出）

```crom
top = model.HumanMadeObject(ident="spring/15", label="马奈的珍妮（春天）")

acq1 = model.Acquisition(label="春天所有权转移给普鲁斯特")
acq1.transferred_title_from = model.Person(ident="manet", label="马奈")
acq1.transferred_title_to = model.Person(ident="proust", label="普鲁斯特")
ts1 = model.TimeSpan()
ts1.begin_of_the_begin = "1881-01-01T00:00:00Z"
ts1.end_of_the_end = "1883-12-31T23:59:59Z"
acq1.timespan = ts1
acq1.part_of = model.Activity(ident="manet_proust", label="完整来源活动")
top.changed_ownership_through = acq1

acq2 = model.Acquisition(label="春天所有权转移给佩恩")
acq2.transferred_title_from = model.Person(ident="durand", label="杜兰-鲁埃尔画廊")
acq2.transferred_title_to = model.Person(ident="payne", label="奥利弗·佩恩")
ts2 = model.TimeSpan()
ts2.begin_of_the_begin = "1909-01-01T00:00:00Z"
ts2.end_of_the_end = "1909-12-31T23:59:59Z"
acq2.timespan = ts2
acq2.part_of = model.Activity(ident="durand_payne", label="完整来源活动")
top.changed_ownership_through = acq2
```



