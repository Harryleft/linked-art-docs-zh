---
title: "Linked Art API：概念"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

概念 API 是获取概念描述的方法，包括类型、材料、语言、计量单位和货币。概念模型相对简单，具有通用属性和模式，很少有附加内容。此 API 端点用于描述概念的完整记录，而不是其他记录中对概念的引用。对于嵌入式概念结构，请参阅[类型结构](../../shared/type)页面。


## 属性定义

通过概念端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 概念的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是概念的表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 概念的类，必须是 `"Type"`、`"Material"`、`"Language"`、`"Currency"` 或 `"MeasurementUnit"` 之一 |
| `_label`          | string        | 推荐    | 概念的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是概念的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是概念的名称，必须遵循[名称](../../shared/name/)的要求，或概念的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于概念的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对概念的外部身份和描述的[引用](../../shared/reference) |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前概念的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前概念成员的集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前概念，必须遵循[引用](../../shared/reference)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前概念与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `broader`         | array         | 可选    | JSON 对象数组，每个对象都是对比当前概念更宽泛的另一个概念的[引用](../../shared/reference) |
| `created_by` | json object | 可选 | 表示概念创建的 JSON 对象，遵循[创建](../../shared/activity)的要求 |


### 属性图

> ![diagram](concept_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/concept)和[模式本身](../../schema/concept.json)


### 传入属性

集合实例通常作为以下属性的对象被发现，除了上述自引用属性外。此列表并非详尽无遗，但旨在涵盖其他端点引用概念的可能情况。


| 属性名称   | 源类   | 描述 |
|-----------------|----------------|-------------|
| `classified_as` | 所有            | 几乎每个实体都可以分类为类型 |
| `technique`     | `Activity`     | 活动（各种类型）可以具有技术，这被建模为类型 |
| `influenced_by`  | `Activity`     | 活动也可以受到类型的影响 |
| `about`         | `LinguisticObject`, `VisualItem` | 文本和视觉作品可以具有主题，这些主题被建模为类型 |
| `assigned`      | `AttributeAssignment` | 对象的分类可能在文档化的属性分配中被分配 |
| `language`      | `LinguisticObject`    | 语言内容的语言被建模为语言 |
| `currency`      | `MonetaryAmount`      | 货币金额的货币被建模为货币 |
| `unit`          | `Dimension`           | 维度的单位被建模为计量单位 |
| `made_of`       | `Material`            | 人造物的材料被建模为材料 |


## 示例

概念条目的 JSON 可能如下所示。

* 它在 `@context` 中包含 Linked Art 上下文文档引用
* 它在 `id` 中自文档化其 URI
* 它的 `type` 是 "Type"
* 它有一个 `_label`，值为 "History of France"，供阅读 JSON 的人员使用
* 它有一个 `identified_by` 属性，带有为其提供主要名称 "History of France" 的 `Name`
* 它有一个 `member_of` 属性，表示它是一个集合的成员，标签为 "Useful History Concepts"
* 它有一个 `broader` 属性，表示更宽泛的术语是标签为 "History of Europe" 的 `Type`
* 它有一个 `equivalent` 属性，表示它通常等同于 LCSH 标题 sh85051256
* 它在 `Creation` 中被创建，该创建...
  * ...受到两个其他实体的 `influenced_by`...
    * ...标签为 "History" 的 `Type`
    * ...和标签为 "France" 的 `Place`


```crom
top = model.Type(ident="auto int-per-segment", label="History of France")
top.identified_by = vocab.PrimaryName(content="History of France")
top.broader = model.Type(label="History of Europe")
top.member_of = model.Set(label="Useful History Concepts")
top.equivalent = model.Type(ident="http://id.loc.gov/authorities/subjects/sh85051256")
cre = model.Creation(label="Concept Creation")
top.created_by = cre
cre.influenced_by = model.Type(label="History")
cre.influenced_by = model.Place(label="France")
```