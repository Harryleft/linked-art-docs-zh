---
title: "Linked Art API: 分配关系结构"
---




## 简介

拥有实体之间的直接关系通常很有用，例如彼此有某种（未声明的）关系的对象、过于复杂无法语义表达的人际关系，或者只是对消费应用程序及其用户可能感兴趣的其他实体的任意推荐集。为了管理这种任意的、非语义的关系，使用 AttributeAssignment 活动来传达这种关系，可选的 `assigned_property` 用于在知道的情况下给出关系类型。

## 属性定义

关系分配数据结构具有以下属性。

### 分配的属性

| 属性名称          | 数据类型      | 要求        | 描述 |
|-------------------|---------------|-------------|-------------|
| `id`              | string        | 可选        | 如果存在，值必须是标识分配的 URI，可以从该 URI 检索分配的表示 |
| `type`            | string        | 必需        | 分配的类，必须是值 `"AttributeAssignment"` |
| `_label`          | string        | 推荐        | 分配的易读标签，面向开发人员 |
| `_complete`       | boolean       | 可选        | 非语义。如果存在带有 URI 的 `id` 属性，并且从该 URI 的表示中可以获得关于属性分配的更多信息，那么 `_complete` 必须存在，值为 `false`，以通知消费应用程序它可能想要检索它 |
| `identified_by`   | array         | 推荐        | json 对象数组，每个都是分配的名称，必须遵循 [名称](../../shared/name/) 的要求，或者是分配的标识符，必须遵循 [标识符](../../shared/identifier/) 的要求|
| `classified_as`   | array         | 推荐        | json 对象数组，每个都是分配的进一步分类，必须遵循 [类型](../type/) 的要求 |
| `referred_to_by`  | array         | 可选        | json 对象数组，每个都是关于分配的嵌入 [陈述](../statement/) |
| `carried_out_by`  | array         | 可选        | json 对象数组，每个都是对进行分配的 [个人](../../endpoint/person) 或 [群体](../../endpoint/group) 的 [引用](../reference/) |
| `timespan`        | json object   | 可选        | 描述关系分配时间的 json 对象，必须遵循 [时间范围](../timespan/) 的要求|
| `during`          | array         | 可选        | json 对象数组，每个都是对分配发生的 [时期](../event/) 的 [引用](../../shared/reference) |
| `before`          | array         | 可选        | json 对象数组，每个都是对此分配发生之前的时期、事件或活动的 [引用](../../shared/reference) |
| `after`          | array         | 可选        | json 对象数组，每个都是对此分配发生之后的时期、事件或活动的 [引用](../../shared/reference) |
| `influenced_by`    | array         | 可选        | json 对象数组，每个都是对影响或激励分配的其他实体的 [引用](../reference/) |
| `caused_by`       | array         | 可选        | json 对象数组，每个都是对导致分配发生的 [事件](../event/) 的 [引用](../../shared/reference/) |
| `used_specific_object` | array    | 可选        | json 对象数组，每个都是对在分配中具有重要作用的其他端点的 [引用](../reference/) |
| `technique` | array | 可选 | json 对象数组，每个都是分配中使用的技术，必须遵循 [类型](../../shared/type) 的要求 |
| `assigned`        | array         | 必需        | json 对象数组，每个都是与当前实体相关的其他实体的 [引用](../reference/)（不应与尺寸或标识符分配一起使用） |
| `assigned_property` | string      | 可选        | 字符串，可以是 URI，或通过上下文文档解析为 URI，用于主实体和 `assigned` 中引用的实体之间的特定关系 |


### 属性图

> ![图](assignment_properties.png){:.diagram_img width="600px"}

### 传入属性

关系分配实例通常作为以下属性的对象被找到。此列表并不详尽，但旨在涵盖可能的情况。

| 属性名称   | 源端点   | 描述 |
|-----------------|-------------------|-------------|
| `attributed_by` | 所有端点     | 实体的关系分配列表 |
| `assigned_by`   | 尺寸、标识符 | 将尺寸或标识符分配给实体的活动 |


## 示例

人造物 [实例](../../endpoint/physical_thing/)：

```crom
top = model.HumanMadeObject(ident="auto int-per-segment", label="Painting of a Fish")
aa = model.AttributeAssignment()
aa.carried_out_by = model.Person(ident="auto int-per-segment", label="Curator")
aa.identified_by = vocab.DisplayName(content="Related Object: Another Painting of a Fish")
aa.classified_as = model.Type(ident="http://example.org/types/recommending", label="Recommendation")
aa.assigned = model.HumanMadeObject(ident="auto int-per-segment", label="Another Painting of a Fish")
top.attributed_by = aa
```