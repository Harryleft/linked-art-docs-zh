---
title: "Linked Art API: Rights Structure"
up_href: "/api/1.0/shared/"
up_label: "Linked Art API 1.0 共享数据结构"
---




## 简介

The Rights construct is used to express machine comparable, but not necessarily actionable, rights assertions about intellectual works. The URI for the class of Right is conveyed in `classified_as`.

See the model documentation for [rights](/model/object/rights/#rights-assertions).

## 属性定义

The rights data structure has the following properties.

### 的属性 Rights

| Property 名称     | 数据类型      | 要求 | 描述 | 
|-------------------|---------------|-------------|-------------|
| `id`              | string        | 可选    | If present, the 值 MUST be a URI identifying the right description, from which a representation of it can be retrieved | 
| `type`            | string        | 必需    | The class for the right, which MUST be the 值 `"Right"` |
| `_label`          | string        | 推荐 | A human readable label, intended for developers |
| `_complete`       | boolean       | 可选    | Non-Semantic. If there is an `id` property with a URI, and there is more information about the identifier available from the representation at that URI, then `_complete` MUST be present with a 值 of `false` to inform the consuming application that it might want to retrieve it |
| `identified_by`   | array         | 推荐 | An array of json objects, each of which is a name for the right, and MUST follow the requirements for [名称](../name/) |
| `classified_as`   | array         | 推荐 | An array of json objects, each of which is a further classification of the right and MUST follow the requirements for [类型](../type/) |
| `referred_to_by`  | array         | 可选    | An array of json objects, each of which is an embedded [statement](../statement/) about the right |
| `possessed_by`    | array         | 可选    | An array of json objects, each of which is a reference to a [Person](../../endpoint/person) or [Group](../../endpoint/group) that holds the right |

### Property Diagram

> ![diagram](right_properties.png){:.diagram_img width="600px"}

### 传入属性

Right instances are typically found as the object of the following properties.

| Property 名称   | Source Endpoint   | 描述 |
|-----------------|-------------------|-------------|
| `subject_to`     | [Textual Work](../../endpoint/textual_work/), [Visual Work](../../endpoint/visual_work), [Abstract Work](../../endpoint/abstract_work), [声明](../statement/) | Intellectual things, primarily works, can have rights associated with them using the `subject_to` property |

## 示例

A textual work is in the public domain.

* The Textual Work is `subject_to` the Right
* The Right itself does not have a URI, but has a `type` of `Right`
* It is `classified_as` the sort of Right, in this case the Creative Commons URI for CC Zero
* It is `identified_by` a `名称`, which is `classified_as` being a Display Title, and the `content` of "Public Domain"

```crom
top = model.LinguisticObject(ident="auto int-per-segment", label="示例 Text")
r = model.Right(label="Public Domain status of 示例 Text")
r.identified_by = vocab.Display名称(content="Public Domain")
r.classified_as = model.类型(ident="https://creativecommons.org/publicdomain/zero/1.0/", label="cc0")
top.subject_to = r
```
