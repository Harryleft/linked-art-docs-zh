---
title: "Linked Art API: 标识符结构"
up_href: "/api/1.0/shared/"
up_label: "Linked Art API 1.0 共享数据结构"
---




## 简介

标识符是分配给某个资源以在特定上下文中标识它的字符串形式的代码。所有不同类型的实体都可以分配标识符。标识符在结构上与[名称](../name/)非常相似，但明确不是自然语言的一部分，因此没有 `language` 属性，也不能被翻译或有替代形式，因此单独记录。

标识符在模型文档的[基础模式](/model/base/#types-and-classifications)中描述，实际上每个类都有示例。

## 属性定义

标识符具有以下属性。

### 标识符的属性

| 属性名称          | 数据类型      | 要求        | 描述 |
|-------------------|---------------|-------------|-------------|
| `id`              | string        | 可选        | 如果存在，值必须是标识标识符的 URI，可以从该 URI 检索分配的表示 |
| `type`            | string        | 必需        | 名称的类，必须是值 `"Identifier"` |
| `_label`          | string        | 推荐        | 易读标签，面向开发人员 |
| `_complete`       | boolean       | 可选        | 非语义。如果存在带有 URI 的 `id` 属性，并且从该 URI 的表示中可以获得关于标识符的更多信息，那么 `_complete` 必须存在，值为 `false`，以通知消费应用程序它可能想要检索它 |
| `content`         | string        | 必需        | 标识符的字符串内容 |
| `classified_as`   | array         | 推荐        | json 对象数组，每个都是标识符的进一步分类，必须遵循 [类型](../type/) 的要求 |
| `identified_by`   | array         | 推荐        | json 对象数组，每个都是为标识符显示的名称，必须遵循 [名称](../name/) 的要求 |
| `referred_to_by`  | array         | 可选        | json 对象数组，每个都是引用标识符的 [文本作品](../../endpoint/textual_work/) 的 [引用](../reference/)，或者是关于标识符的嵌入 [陈述](../statement/)。 |
| `assigned_by`     | array         | 可选        | json 对象数组，每个都是标识符的分配，必须遵循 [分配](../assignment/) 的要求 |

### 属性图

> ![图](identifier_properties.png){:.diagram_img width="600px"}


### 传入属性

标识符实例通常作为以下属性的对象被找到。此列表并不详尽，但旨在涵盖可能的情况。

| 属性名称   | 源端点   | 描述 |
|-----------------|-------------------|-------------|
| `identified_by` | 所有端点     | 实体的标识符列表 |