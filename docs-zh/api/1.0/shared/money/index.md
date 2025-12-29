---
title: "Linked Art API: 货币金额 Structure"
up_href: "/api/1.0/shared/"
up_label: "Linked Art API 1.0 共享数据结构"
---




## 简介

货币金额s are similar to [尺寸s](../dimension/) in that they are primarily a `值` with a unit to clarify what the number refers to, but in this case the unit is a `货币`.  The amount is a particular instance of a 值/货币 combination, so there can be multiple amounts each of which have the same 值 and 货币, but are used in different models.  This is the same as the way there can be multiple dimensions with the same classification, 值 and unit used in different models.

In the Linked Art API and model, amounts are only used in the [Provenance Activity](../../endpoint/provenance_activity/) structure, as described in the [Provenance](/model/provenance/) model documentation.

## 属性定义

The monetary amount data structure has the following properties.

### 的属性 货币金额s

| Property 名称     | 数据类型      | 要求 | 描述 | 
|-------------------|---------------|-------------|-------------| 
| `id`              | string        | 可选    | If present, the 值 MUST be a URI identifying the amount, from which a representation of the amount can be retrieved | 
| `type`            | string        | 必需    | The class for the name, which MUST be the 值 `"MonetaryAmount"` |
| `_label`          | string        | 推荐 | A human readable label, intended for developers |
| `_complete`       | boolean       | 可选    | Non-Semantic. If there is an `id` property with a URI, and there is more information about the amount available from the representation at that URI, then `_complete` MUST be present with a 值 of `false` to inform the consuming application that it might want to retrieve it |
| `值`           | number        | 必需    | The numeric 值 of the amount |
| `货币`        | json object   | 必需    | The 货币 for the amount, which MUST follow the requirements for a [Currency](../type/) |
| `classified_as`   | array         | 推荐 | An array of json objects, each of which is a further classification of the amount and MUST follow the requirements for [类型](../type/) |
| `identified_by`   | array         | 推荐 | An array of json objects, each of which is a textual representation of the structured data in the amount, and MUST follow the requirements for [名称](../name/) |
| `upper_值_limit` | number      | 可选    | A number, which represents the highest possible 值 for the amount|
| `lower_值_limit` | number      | 可选    | A number, which represents the lowest possible 值 for the amount |
| `referred_to_by`  | array         | 可选    | An array of json objects, each of which is either a [reference](../reference/) to a [textual work](../../endpoint/textual_work/) that refers to the amount, or an embedded [statement](../statement/) about the amount. |

### Property Diagram

> ![diagram](monetary_amount_properties.png){:.diagram_img width="600px"}

### 传入属性

尺寸 instances are typically found as the object of the following properties.  This list is not exhaustive, but is intended to cover the likely cases.

| Property 名称   | Source Endpoint   | 描述 |
|-----------------|-------------------|-------------|
| `paid_amount`   | [Provenance Activity](../../endpoint/provenance_activity/) | Monetary amounts are mostly used to record the amount of money that changes hands in a transaction, referred to from a Payment in a Provenance Activity | 
| `dimension`     | [Set](../../endpoint/set/)      | Monetary amounts can be associated with other entities, such as a Set of objects, with the dimension property  |


## 示例

An auction lot has a monetary amount of $500 as its starting price.

* It has a `type` of "MonetaryAmount"
* It is `classified_as` a starting price, with an `id` of _aat:300417242_ and a `type` of "类型"
* It has a `值` of 500
* And a `货币` of US dollars, with an `id` of _aat:300411994_ and a `type` of "Currency"
* It has a display label with the content of "500 US Dollars"
* It is `referred_to_by` a note, with the content "From personal correspondence"

```crom
top = model.Set(ident="auto int-per-segment", label = "Set of Objects for Lot 812")
amnt = vocab.StartingPrice(label="$500", 值=500)
amnt.货币 = vocab.instances['us dollars']
amnt.identified_by = vocab.Display名称(content="500 US Dollars")
amnt.referred_to_by = vocab.Note(content="From personal correspondence")
top.dimension = amnt
```
