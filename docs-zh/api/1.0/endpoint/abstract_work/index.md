---
title: "Linked Art API：抽象作品"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---



## 简介

抽象作品 API 是一种获取抽象或概念作品描述的方法，特别是当这些作品由活动而不是物理或数字对象实例化时使用。例如展览背后的"理念"、行为艺术作品的一般概念而不是实现该理念的活动，或者作品的最一般形式而不特别由图像或语言组成。因此抽象作品不经常使用，但对于连接作品的实例是必要的，如巡回展览或相同理念的不同表演。

关于抽象作品用法的更多信息，请参阅[展览概念](/model/exhibition/)描述。


## 属性定义

通过抽象作品端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 抽象作品的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是作品的表示可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 作品的类，必须是值 `"PropositionalObject"` |
| `_label`          | string        | 推荐    | 作品的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是作品的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是作品的名称/标题，必须遵循[名称](../../shared/name/)的要求，或作品的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于作品的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对同样标识当前作品的外部 URI 的[引用](../../shared/reference) |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前抽象作品，必须遵循[引用](../../shared/reference/)的要求 |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前作品的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前作品成员的集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前作品与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `dimension` | array | 可选 | JSON 对象数组，每个对象都是当前作品的抽象[维度](../../shared/dimension) |
| `conceptually_part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前作品在概念上所属的另一个抽象作品的[引用](../../shared/reference/) |
| `about` | array | 可选 | JSON 对象数组，每个对象都是对任何类型的另一个实体的[引用](../../shared/reference/)，该作品主要关于此实体 |
| `subject_to` | array | 可选 | JSON 对象数组，每个对象都是对智力作品持有的[权利](../../shared/right) |
| `created_by` | json object | 可选 | 表示作品创建的 JSON 对象，遵循[创建](../../shared/activity)的要求 |

### 属性图

> ![diagram](abstract_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/abstract)和[模式本身](../../schema/abstract.json)


### 传入属性

抽象作品实例通常作为以下属性的对象被发现，除了上述自引用属性外。此列表并非详尽无遗，但旨在涵盖其他端点引用文本的可能情况。

| 属性名称              | 源端点 | 描述 |
|----------------------------|-----------------|-------------|
| `about`                    | 文本作品    | 文本作品可以关于抽象作品  |
| `influenced_by`             | 活动        | 活动（如展览）可以受到抽象作品的影响 |


## 示例

关于庚斯博罗展览理念的抽象作品条目的 JSON 可能如下所示。

* 它在 `@context` 中包含 Linked Art 上下文文档引用
* 它在 `id` 中自文档化其 URI
* 它的 `type` 是 "PropositionalObject"
* 它有一个 `_label`，值为 "Gainsborough Exh."，供阅读 JSON 的人员使用
* 它被 `classified_as` 为展览，其 `id` 为 "aat:300417531"
* 它被 `identified_by` 为...
    * ...一个 `Name`，内容为 "Gainsborough Exhibition"
* 它被 `referred_to_by` 一个声明，该声明...
    * ...有描述抽象作品的 `content`
    * ...并被 `classified_as` 为抽象概念（"aat:300418049"）
* 它是 `about` 庚斯博罗，一个 `id` 为 "ulan:500115200" 的个人
* 它被 `created_by` 一个创建，该创建...
    * ...由 Brett Hayes `carried_out_by`，一个个人


```crom
top = vocab.ExhibitionIdea(ident="auto int-per-segment", label="Gainsborough Exh.")
top.identified_by = vocab.PrimaryName(content="Gainsborough Exhibition")
top.referred_to_by = vocab.Abstract(content="A thorough analysis of the artist's life and work")
top.about = model.Person(ident="http://vocab.getty.edu/ulan/500115200", label="Gainsborough, Thomas")
cre = model.Creation()
cre.carried_out_by = model.Person(ident="http://vocab.getty.edu/ulan/500144588", label="Hayes, Brett")
top.created_by = cre
```