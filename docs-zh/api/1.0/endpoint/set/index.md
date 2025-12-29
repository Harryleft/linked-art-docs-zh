---
title: "Linked Art API：集合"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

集合 API 是获取集合描述的方法，包括藏品集合、系列、展览集合或任何其他可识别的对象集合。集合模型具有中等复杂度，具有许多熟悉的属性和模式，以及描述集合成员关系的字段。

关于集合用法的更多信息，请参阅[集合模型](/model/collection/)描述。


## 属性定义

通过集合端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 集合的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是集合表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 集合的类，必须是值 `"Set"` |
| `_label`          | string        | 推荐    | 集合的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是集合的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是集合的名称，必须遵循[名称](../../shared/name/)的要求，或集合的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于集合的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对当前集合外部身份的[引用](../../shared/reference) |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前集合成员的另一个集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前集合，必须遵循[引用](../../shared/reference/)的要求 |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前集合的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前集合与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前集合所属的另一个集合的[引用](../../shared/reference/) |
| `member` | array | 可选 | JSON 对象数组，每个对象都是集合成员的实体的[引用](../../shared/reference/) |
| `created_by` | json object | Optional | 表示集合创建的 JSON 对象，遵循[创建](../../shared/activity)的要求 |

### 属性图

> ![diagram](set_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/set)和[模式本身](../../schema/set.json)