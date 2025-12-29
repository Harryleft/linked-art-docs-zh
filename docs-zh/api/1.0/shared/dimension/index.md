---
title: "Linked Art API: 尺寸结构"
up_href: "/api/1.0/shared/"
up_label: "Linked Art API 1.0 共享数据结构"
---




## 简介

尺寸是数值、数值单位和关于它是什么类型数值的分类的组合。它们可以通过某些方式在实体上测量，如计数或使用仪器。数据结构通常用于物理事物（如高度和宽度），但也适用于文本作品（如单词数）甚至人（如身高、体重）。如果有可计算的特征，那么可以使用此数据结构表示为尺寸。

## 属性定义

尺寸数据结构具有以下属性。

### 尺寸的属性

| 属性名称          | 数据类型      | 要求        | 描述 |
|-------------------|---------------|-------------|-------------|
| `id`              | string        | 可选        | 如果存在，值必须是标识尺寸的 URI，可以从该 URI 检索尺寸的表示 |
| `type`            | string        | 必需        | 尺寸的类，必须具有值 `"Dimension"` |
| `_label`          | string        | 推荐        | 易读标签，面向开发人员 |
| `_complete`       | boolean       | 可选        | 非语义。如果存在带有 URI 的 `id` 属性，并且从该 URI 的表示中可以获得关于标识符的更多信息，那么 `_complete` 必须存在，值为 `false`，以通知消费应用程序它可能想要检索它 |
| `value`           | number        | 必需        | 尺寸的数值 |
| `unit`            | json object   | 必需        | 尺寸的单位，必须遵循 [MeasurementUnit](../type/) 的要求 |
| `classified_as`   | array         | 推荐        | json 对象数组，每个都是尺寸的进一步分类，必须遵循 [类型](../type/) 的要求 |
| `identified_by`   | array         | 推荐        | json 对象数组，每个都是尺寸中结构化数据的文本表示，必须遵循 [名称](../name/) 的要求 |
| `upper_value_limit` | number      | 可选        | 数字，表示尺寸可能的最高值 |
| `lower_value_limit` | number      | 可选        | 数字，表示尺寸可能的最低值 |
| `referred_to_by`  | array         | 可选        | json 对象数组，每个都是引用尺寸的 [文本作品](../../endpoint/textual_work/) 的 [引用](../reference/)，或者是关于尺寸的嵌入 [陈述](../statement/)。 |
| `assigned_by`     | array         | 可选        | json 对象数组，每个都是尺寸的测量活动，遵循 [AttributeAssignment](../assignment/) 模式 |

### 属性图

> ![图](dimension_properties.png){:.diagram_img width="600px"}

### 传入属性

尺寸实例通常作为以下属性的对象被找到。此列表并不详尽，但旨在涵盖可能的情况。

| 属性名称   | 源端点   | 描述 |
|-----------------|-------------------|-------------|
| `dimension`     | [物理对象](../../endpoint/physical_object/)、[数字对象](../../endpoint/digital_object) 等 | 尺寸实例是源实体的尺寸，特别是物理和数字对象 |
| `duration`      | 所有端点中的 TimeSpan | 尺寸是实际时间范围的长度（持续时间），在 TimeSpan 实例描述的边界内，可以存在于所有端点中 |

## 示例

人造物 [实例](../../endpoint/physical_thing/) 的高度为 24（+/- 2）英寸，由策展人测量：

```crom
top = model.HumanMadeObject(ident="auto int-per-segment", label="Painting")
dim = model.Dimension()
dim.value = 24
dim.unit = vocab.Unit(ident="http://vocab.getty.edu/aat/300379093", label="inches")
dim.upper_value_limit = 26
dim.lower_value_limit = 22
dim.classified_as = model.Type(ident="http://vocab.getty.edu/aat/300055644", label="height")
aa = model.AttributeAssignment()
aa.carried_out_by = model.Person(ident="auto int-per-segment", label="Curator")
dim.assigned_by = aa
top.dimension = dim
```