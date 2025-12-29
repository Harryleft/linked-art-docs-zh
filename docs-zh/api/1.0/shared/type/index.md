---
title: "Linked Art API: 类型 Structure"
up_href: "/api/1.0/shared/"
up_label: "Linked Art API 1.0 共享数据结构"
---




## 简介

Concepts, called 类型s, are a core part of the model and present in practically every resource description. They give access to external vocabularies, such as the Getty's Art and Architecture Thesaurus, in order to add classifications to entities described. As they are external entities, rather than the focus of the Linked Art documentation, they are only slightly more detailed than any other [entity reference](../reference/), allowing an additional meta-classification to be asserted about the 类型. 

The 类型 pattern is also used for more specific concept types:

* `Language` is used for human-spoken languages, such as Spanish
* `Material` is used for the materials that make up a physical thing, such as gold
* `Currency` is used for the 货币 of monetary amounts, such as the Euro
* `MeasurementUnit` is used for the unit of measured dimensions, such as inches

类型s are described in the [base patterns](/model/base/#types-and-classifications) of the model documentation, and examples are present for practically every class.

For full records that describe a 类型, please see the [Concept Endpoint](../../endpoint/concept/) documentation.

## 属性定义

### 的属性 类型s

| Property 名称     | 数据类型      | 要求 | 描述 | 
|-------------------|---------------|-------------|-------------|
| `id`              | string        | 必需    | The 值 MUST be a URI identifying the concept |  
| `type`            | string        | 必需    | The class of the concept, which MUST be one of the following 值s: `"类型"`, `"Currency"`, `"Language"`, `"Material"`, or `"MeasurementUnit"` |
| `_label`          | string        | 推荐 | A human readable label for the concept, intended for developers |
| `equivalent`      | array         | 可选    | An array of references to external resources which are equivalent to the referenced resource |
| `notation`        | array         | 可选    | An array of strings, each of which is a commonly used notation or identifier for the resource. This is typically used when the `type` of the reference is `Language` and gives the [language tag](https://www.w3.org/International/articles/language-tags/). |
| `classified_as`   | array         | 可选    | An array of json objects, each of which is a further classification of the concept and MUST follow these requirements for 类型 |

### Property Diagram

> ![diagram](type_properties.png){:.diagram_img width="600px"}

### 传入属性

类型s and other instances of concepts are typically found as the object of the following properties.  This list is not exhaustive, but is intended to cover the likely cases.

| Property 名称   | Source Class   | 描述 |
|-----------------|----------------|-------------|
| `classified_as` | All            | Almost every entity can be classified as a 类型 |
| `technique`     | `Activity`     | Activities (of all sorts) can have a technique, which is modeled as a 类型 |
| `influenced_by`  | `Activity`     | Activities can also be motivated by a 类型 |
| `about`         | `LinguisticObject`, `VisualItem` | Textual and Visual Works can have subjects, which are modeled as 类型s |
| `assigned`      | `AttributeAssignment` | The classification of an object might be assigned as part of a documented Attribute Assignment |
| `language`      | `LinguisticObject`    | The language of linguistic content is modeled as a Language |
| `货币`      | `MonetaryAmount`      | The 货币 of a MonetaryAmount is modeled as a Currency |
| `unit`          | `尺寸`           | The unit of a 尺寸 is modeled as a MeasurementUnit |
| `made_of`       | `Material`            | The materials of a HumanMadeObject are modeled as Materials | 


## 示例

A painting is classified as a painting, which is in turn classified as a type of work.

* It has an `id` of _aat:300033618_
* It has a `type` of "类型"
* It has a human readable `_label` of "Painting"
* It is classified as a meta-type, which ...
    * ... has an `id` of _aat:300435443_
    * ... also has a `type` of "类型"
    * ... and has a human readable `_label` of "类型 of Work"

```crom
top = vocab.Painting(ident="auto int-per-segment")
```
