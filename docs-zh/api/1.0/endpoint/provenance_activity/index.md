---
title: "Linked Art API：流传历史活动"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

流传历史活动 API 是获取流传历史活动描述的方法，包括获得、转移、出售、赠与或其他改变艺术品所有权或保管状态的活动。这些活动是构成艺术品流传历史的核心元素。

关于流传历史活动用法的更多信息，请参阅[流传历史模型](/model/provenance/)描述。


## 属性定义

通过流传历史活动端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 流传历史活动的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是流传历史活动表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 流传历史活动的类，必须是 `"Activity"` 值，并且通常会通过 `classified_as` 进一步分类为特定类型的流传历史活动 |
| `_label`          | string        | 推荐    | 流传历史活动的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是流传历史活动的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是流传历史活动的名称，必须遵循[名称](../../shared/name/)的要求，或流传历史活动的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于流传历史活动的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对当前流传历史活动外部身份的[引用](../../shared/reference) |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前流传历史活动，必须遵循[引用](../../shared/reference/)的要求 |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前流传历史活动的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前流传历史活动与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前流传历史活动所属的另一个活动的[引用](../../shared/reference/) |
| `timespan`        | json object   | 推荐    | 记录流传历史活动发生时间的 JSON 对象，必须遵循[时间段](../../shared/timespan/)的要求 |
| `took_place_at`   | array         | 可选    | JSON 对象数组，每个对象都是对流传历史活动发生的[地点](../place/)的[引用](../../shared/reference/) |
| `caused_by`       | array         | 可选    | JSON 对象数组，每个对象都是对导致此流传历史活动发生的另一个活动的[引用](../../shared/reference/) |
| `influenced_by`   | array         | 可选    | JSON 对象数组，每个对象都是对以某种显著方式影响流传历史活动的实体的[引用](../../shared/reference/) |
| `carried_out_by`  | array         | 可选    | JSON 对象数组，每个对象都是对执行流传历史活动的[个人](../person/)或[群体](../group/)的[引用](../../shared/reference/) |
| `used_specific_object` | array    | 可选    | JSON 对象数组，每个对象都是对在执行流传历史活动中起重要作用的对象的[引用](../../shared/reference) |
| `technique` | array | 可选 | JSON 对象数组，每个对象都是流传历史活动中使用的技术，必须遵循[类型](../../shared/type)的要求 |
| `transferred_title_of` | array | 可选 | JSON 对象数组，每个对象都是所有权转移的对象的[引用](../../shared/reference) |
| `transferred_custody_of` | array | 可选 | JSON 对象数组，每个对象都是保管权转移的对象的[引用](../../shared/reference) |

### 属性图

> ![diagram](provenance_activity_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/provenance_activity)和[模式本身](../../schema/provenance_activity.json)