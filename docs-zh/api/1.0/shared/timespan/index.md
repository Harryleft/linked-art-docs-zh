---
title: "Linked Art API: TimeSpan Structure"
up_href: "/api/1.0/shared/"
up_label: "Linked Art API 1.0 共享数据结构"
---




## 简介

The details of time spans are recorded using a data structure called a `TimeSpan`. Each period, event, activity or further more specific class can have its own time span with fuzzy starting and ending points, and a duration of time that the event lasted between the start and end.  They are always approximations, but allow for searching computation.

时间范围s are used for all temporal entities, and described in the [base patterns](/model/base/#time-span-details) of the model.

## 属性定义

The time span data structure has the following properties.

### 的属性 TimeSpans

| Property 名称     | 数据类型      | 要求 | 描述 | 
|-------------------|---------------|-------------|-------------|
| `id`              | string        | 可选    | If present, the 值 MUST be a URI identifying the timespan, from which a representation of the timespan can be retrieved | 
| `type`            | string        | 必需    | The class for the name, which MUST be the 值 `"TimeSpan"` |
| `_label`          | string        | 推荐 | A human readable label, intended for developers |
| `_complete`       | boolean       | 可选    | Non-Semantic. If there is an `id` property with a URI, and there is more information about the timespan available from the representation at that URI, then `_complete` MUST be present with a 值 of `false` to inform the consuming application that it might want to retrieve it |
| `classified_as`   | array         | 推荐 | An array of json objects, each of which is a further classification of the time span and MUST follow the requirements for [类型](../type/) |
| `identified_by`   | array         | 推荐 * | An array of json objects, each of which is a textual representation of the structured data in the time span, and MUST follow the requirements for [名称](../name/) |
| `begin_of_the_begin` | date       | 推荐 * | A string containing an ISO8601 formatted date-time, representing the earliest possible date at which the timespan could have started |
| `end_of_the_end`  | date          | 推荐 * | A string containing an ISO8601 formatted date-time, representing the latest possible date at which the timespan could have ended |
| `end_of_the_begin` | date         | 可选    | A string containing an ISO8601 formatted date-time, representing the latest possible date at which the timespan could have started |
| `begin_of_the_end` | date         | 可选    | A string containing an ISO8601 formatted date-time, representing the earliest possible date at which the timespan could have ended |
| `referred_to_by`  | array         | 可选    | An array of json objects, each of which is either a [reference](../reference/) to a [textual work](../../endpoint/textual_work/) that refers to the time span, or an embedded [statement](../statement/) about the time span. |
| `duration`        | json object   | 可选    | A json object representing the length of time for the time span within the date range, which MUST follow the requirements for [尺寸s](../dimension/) | 


* * Note Well that TimeSpans MUST have at least one of `identified_by`, `begin_of_the_begin` and `end_of_the_end`. Without these, there is no information to convey to the consuming application, and it becomes impossible to distinguish with a reference if the `id` is given, as there are no other properties that would be present.

### Property Diagram

> ![diagram](timespan_properties.png){:.diagram_img width="600px"}

### 传入属性

尺寸 instances are typically found as the object of the following properties.  This list is not exhaustive, but is intended to cover the likely cases.

| Property 名称   | Source Endpoint   | 描述 |
|-----------------|-------------------|-------------|
| `timespan`      | All endpoints     | The timespan is the range of time for an activity in any endpoint |


## 示例

An activity has a time span with a duration of 1 day, sometime circa 1750

* It has a `type` of "TimeSpan"
* It has a `_label` which briefly describes it as "1 day, c. 1750"
* It is `identified_by` a 名称, with `content` of "1 day, during circa 1750"
* It is `referred_to_by` a description statement, with the `content` of "About 1750, as estimated by C. U. Rata"
* It has a `begin_of_the_begin` earliest start date of 1720
* It has a `end_of_the_begin` latest start date of 1751
* It has a `begin_of_the_end` earliest end date of 1749
* It has a `end_of_the_end` latest end date of 1780
* It took a `duration` of time which ...
    * ... has a `type` of "尺寸"
    * ... has a `值` of 1
    * ... has a `unit` of days, which has an `id` of _aat:300379242_ and has a `type` of "MeasurementUnit"

```crom
top = model.Activity(ident="auto int-per-segment")
ts = model.TimeSpan(label="1 day, c. 1750")
ts.identified_by = model.名称(content="1 day, during circa 1750")
ts.referred_to_by = vocab.描述(content="About 1750, as estimated by C. U. Rata")
ts.begin_of_the_begin = "1720-01-01T00:00:00Z"
ts.end_of_the_begin = "1751-01-01T00:00:00Z"
ts.begin_of_the_end = "1749-01-01T00:00:00Z"
ts.end_of_the_end = "1780-01-01T00:00:00Z"
dur = model.尺寸()
dur.值 = 1
dur.unit = vocab.instances['days']
ts.duration = dur
top.timespan = ts
```
