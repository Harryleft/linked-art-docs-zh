---
title: "Linked Art API：群体"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

群体 API 是获取人群和/或子群组描述的方法，如家庭、组织、公司、部门或任何其他可识别的行动者集合。群体模型具有中等复杂度，具有许多熟悉的属性和模式，加上一些更特定的字段。这产生了一个中等复杂度的 API，与[个人 API](../person/) 非常相似，如果所有字段都有值，可能会导致相当长的 JSON 响应。

关于群体数据用法的更多信息，请参阅[群体模型](/model/actor/)描述。


## 属性定义

通过群体端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 群体的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是群体表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 群体的类，必须是值 `"Group"` |
| `_label`          | string        | 推荐    | 群体的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是群体的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是群体的名称，必须遵循[名称](../../shared/name/)的要求，或群体的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于群体的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对当前群体外部身份的[引用](../../shared/reference) |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前群体成员的集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前群体，必须遵循[引用](../../shared/reference/)的要求 |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前群体的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前群体与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前群体所属的另一个群体的[引用](../../shared/reference/) |
| `formed_by` | json object | Optional | 表示群体形成的 JSON 对象，遵循[形成](../../shared/activity)的要求 |
| `dissolved_by` | json object | Optional | 表示群体解散的 JSON 对象，遵循[解散](../../shared/activity)的要求 |
| `founded_by` | array | Optional | JSON 对象数组，每个对象都是创建群体的[个人](../person/)或[群体](../group/)的[引用](../../shared/reference/) |
| `member` | array | Optional | JSON 对象数组，每个对象都是群体成员的[个人](../person/)或[群体](../group/)的[引用](../../shared/reference/) |

### 属性图

> ![diagram](group_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/group)和[模式本身](../../schema/group.json)