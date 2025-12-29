---
title: "Linked Art API：物理对象"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

物理对象 API 是获取物理对象描述的方法，包括艺术品、文物和任何其他人造物品。物理对象模型具有较高复杂度，包含许多熟悉的属性和模式，以及描述物理特征、材料、尺寸等的多个字段。这产生了一个复杂的 API，如果所有字段都有值，可能会导致很长的 JSON 响应。

关于物理对象用法的更多信息，请参阅[物理对象模型](/model/object/)描述。


## 属性定义

通过物理对象端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 物理对象的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是物理对象表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 物理对象的类，必须是值 `"HumanMadeObject"` |
| `_label`          | string        | 推荐    | 物理对象的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是物理对象的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是物理对象的名称/标题，必须遵循[名称](../../shared/name/)的要求，或物理对象的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于物理对象的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对当前物理对象外部身份的[引用](../../shared/reference) |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前物理对象成员的集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前对象，必须遵循[引用](../../shared/reference/)的要求 |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前对象的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前物理对象与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前物理对象所属的另一个物理对象的[引用](../../shared/reference/) |
| `dimension` | array | 可选 | JSON 对象数组，每个对象都是物理对象的[维度](../../shared/dimension) |
| `made_of` | array | 可选 | JSON 对象数组，每个对象都是物理对象材料的[引用](../../shared/reference/) |
| `carries` | array | 可选 | JSON 对象数组，每个对象都是物理对象承载的[文本作品](../textual_work/)的[引用](../../shared/reference/) |
| `shows` | array | 可选 | JSON 对象数组，每个对象都是物理对象显示的[视觉作品](../visual_work/)的[引用](../../shared/reference/) |
| `current_location` | array | 可选 | JSON 对象数组，每个对象都是物理对象当前位置的[地点](../place/)的[引用](../../shared/reference/) |
| `current_owner` | array | 可选 | JSON 对象数组，每个对象都是物理对象当前所有者的[个人](../person/)或[群体](../group/)的[引用](../../shared/reference/) |
| `produced_by` | json object | Optional | 表示物理对象生产的 JSON 对象，遵循[生产](../../shared/activity)的要求 |
| `destroyed_by` | json object | Optional | 表示物理对象毁坏的 JSON 对象，遵循[毁坏](../../shared/activity)的要求 |

### 属性图

> ![diagram](physical_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/physical)和[模式本身](../../schema/physical.json)