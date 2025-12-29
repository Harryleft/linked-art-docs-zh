---
title: "Linked Art API：事件"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

事件 API 是获取时间段、事件或活动描述的方法，这些时间段、事件或活动不直接与其他实体相关联，也不是流传历史活动或展览，但仍然是以某种方式与艺术品相关的值得注意的事件。例如可能包括烧毁博物馆从而造成许多艺术品毁坏的火灾、研究艺术品某些方面的项目，或对象被创建的命名时期。虽然这些是不同的类，但在此用法中它们如此相似，以至于从 API 的角度来看它们被组合到单个端点中。事件 API 具有中等复杂度，具有许多其他端点的熟悉属性和模式，以及嵌入式事件熟悉的事件和活动属性。

## 属性定义

通过事件端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 事件的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是事件表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 事件的类，必须是值 `"Period"`、`"Event"` 或 `"Activity"` |
| `_label`          | string        | 推荐    | 事件的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是事件的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是事件的名称/标题，必须遵循[名称](../../shared/name/)的要求，或事件的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于事件的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对当前事件的外部身份和描述的[引用](../../shared/reference) |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前事件的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前事件成员的集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前事件，必须遵循[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前事件与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前事件直接所属的另一个事件的[引用](../../shared/reference/) |
| `timespan`        | json object   | 推荐    | 记录事件发生时间的 JSON 对象，必须遵循[时间段](../../shared/timespan/)的要求 |
| `during`          | array         | 可选    | JSON 对象数组，每个对象都是对发生此事件的广泛[时期](../event/)的[引用](../../shared/reference) |
| `before`          | array         | 可选    | JSON 对象数组，每个对象都是对此事件发生之前的时期、事件或活动的[引用](../../shared/reference) |
| `after`          | array         | 可选    | JSON 对象数组，每个对象都是对此事件发生之后的时期、事件或活动的[引用](../../shared/reference) |
| `took_place_at`   | array         | 可选    | JSON 对象数组，每个对象都是对事件发生的[地点](../place/)的[引用](../../shared/reference/) |
| `caused_by`       | array         | 可选    | JSON 对象数组，每个对象都是对导致此事件发生的另一个事件的[引用](../../shared/reference/)。**仅在 `type` 为 `"Event"` 或 `"Activity"` 时可用** |
| `influenced_by`   | array         | 可选    | JSON 对象数组，每个对象都是对以某种显著方式影响事件的实体的[引用](../../shared/reference/)。**仅在 `type` 为 `"Activity"` 时可用** |
| `carried_out_by`  | array         | 可选    | JSON 对象数组，每个对象都是对执行活动的[个人](../person/)或[群体](../group/)的[引用](../../shared/reference/)。**仅在 `type` 为 `"Activity"` 时可用** |
| `participant`  | array         | 可选    | JSON 对象数组，每个对象都是对参与事件但未执行事件的[个人](../person/)或[群体](../group/)的[引用](../../shared/reference/)。**仅在 `type` 为 "Event" 或 "Activity" 时可用** |
| `used_specific_object` | array    | 可选    | JSON 对象数组，每个对象都是对在执行活动中起重要作用的实体的[引用](../../shared/reference)。**仅在 `type` 为 `"Activity"` 时可用** |
| `technique` | array | 可选 | JSON 对象数组，每个对象都是活动中使用的技术，必须遵循[类型](../../shared/type)的要求。**仅在 `type` 为 `"Activity"` 时可用** |

### 属性图

> ![diagram](event_properties.png){:.diagram_img width="600px"}