---
title: "Linked Art API：地点"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

地点 API 是获取地点描述的方法，包括城市、建筑物、具体房间或地理区域。地点模型具有中等复杂度，具有许多熟悉的属性和模式，以及描述地理坐标、层级关系等的字段。这产生了一个中等复杂度的 API。

关于地点用法的更多信息，请参阅[地点模型](/model/place/)描述。


## 属性定义

通过地点端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 地点的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是地点表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 地点的类，必须是值 `"Place"` |
| `_label`          | string        | 推荐    | 地点的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是地点的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是地点的名称，必须遵循[名称](../../shared/name/)的要求，或地点的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于地点的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对当前地点外部身份的[引用](../../shared/reference) |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前地点成员的集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前地点，必须遵循[引用](../../shared/reference/)的要求 |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前地点的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前地点与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前地点所属的另一个地点的[引用](../../shared/reference/) |
| `defined_by` | array | 可选 | JSON 对象数组，每个对象都是定义地点几何形状的[几何形状](../../shared/geometry)的引用 |

### 属性图

> ![diagram](place_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/place)和[模式本身](../../schema/place.json)