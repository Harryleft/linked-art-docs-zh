---
title: "Linked Art API：文本作品"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

文本作品 API 是获取文本作品描述的方法，包括书籍、文章、手稿、诗歌或任何其他主要由文本组成的创作。文本作品模型具有中等复杂度，具有许多熟悉的属性和模式，以及描述语言、内容主题等的字段。

关于文本作品用法的更多信息，请参阅相关模型描述。


## 属性定义

通过文本作品端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 文本作品的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是文本作品表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 文本作品的类，必须是值 `"LinguisticObject"` |
| `_label`          | string        | 推荐    | 文本作品的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是文本作品的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是文本作品的名称/标题，必须遵循[名称](../../shared/name/)的要求，或文本作品的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于文本作品的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对当前文本作品外部身份的[引用](../../shared/reference) |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前文本作品成员的集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对其他[文本作品](../textual_work/)的引用，其内容聚焦于当前文本作品，必须遵循[引用](../../shared/reference/)的要求 |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前文本作品的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前文本作品与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前文本作品所属的另一个文本作品的[引用](../../shared/reference/) |
| `about` | array | 可选 | JSON 对象数组，每个对象都是对文本作品关于的实体的[引用](../../shared/reference/) |
| `language` | array | 可选    | JSON 对象数组，每个对象都是文本作品语言的[引用](../../shared/reference) |
| `created_by` | json object | Optional | 表示文本作品创建的 JSON 对象，遵循[创建](../../shared/activity)的要求 |
| `digitally_carried_by` | array | Optional | JSON 对象数组，每个对象都是承载此文本作品的数字对象的[引用](../../shared/reference/) |

### 属性图

> ![diagram](textual_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/textual)和[模式本身](../../schema/textual.json)