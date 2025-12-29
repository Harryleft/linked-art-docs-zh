---
title: "Linked Art API: 嵌入活动结构"
---




## 简介

虽然数据模型是以活动为中心的，但将活动的描述嵌入到活动创建、销毁或使用的实体的描述中通常更有效。这种模式用于将事物带入存在（制作、创作、形成）、将事物带出存在（毁坏、解散、死亡）以及人们进行的活动，如他们的专业活动。


## 属性定义

活动数据结构具有以下属性。

### 活动的属性

| 属性名称          | 数据类型      | 要求        | 描述 |
|-------------------|---------------|-------------|-------------|
| `id`              | string        | 可选        | 如果存在，值必须是标识活动的 URI，可以从该 URI 检索活动的表示 |
| `type`            | string        | 必需        | 活动的类，其值必须取自下表 |
| `_label`          | string        | 推荐        | 非语义。活动的易读标签，面向开发人员 |
| `_complete`       | boolean       | 可选        | 非语义。如果存在带有 URI 的 `id` 属性，并且从该 URI 的表示中可以获得关于活动的更多信息，那么 `_complete` 必须存在，值为 `false`，以通知消费应用程序它可能想要检索它 |
| `identified_by`   | array         | 推荐        | json 对象数组，每个都是活动的名称，必须遵循 [名称](../name/) 的要求，或者是活动的标识符，必须遵循 [标识符](../identifier/) 的要求|
| `classified_as`   | array         | 推荐        | json 对象数组，每个都是活动的进一步分类，必须遵循 [类型](../type/) 的要求 |
| `referred_to_by`  | array         | 可选        | json 对象数组，每个都是关于活动的嵌入 [陈述](../statement/) |
| `took_place_at`   | array         | 可选        | json 对象数组，每个都是对活动发生的 [地点](../../endpoint/place/) 的 [引用](../reference/) |
| `timespan`        | json object   | 可选        | 描述活动发生时间的 json 对象，必须遵循 [时间范围](../timespan/) 的要求|
| `during`          | array         | 可选        | json 对象数组，每个都是对活动发生期间的 [时期](../../endpoint/event/) 的 [引用](../reference) |
| `before`          | array         | 可选        | json 对象数组，每个都是对此事件发生之前的时期、事件或活动的 [引用](../reference) |
| `after`          | array         | 可选        | json 对象数组，每个都是对此事件发生之后的时期、事件或活动的 [引用](../reference) |
| `caused_by`       | array         | 可选        | json 对象数组，每个都是对导致此事件发生的 [事件](../../endpoint/event/) 的 [引用](../reference/) |
| `carried_out_by`  | array         | 可选        | json 对象数组，每个都是对执行活动的 [个人](../../endpoint/person) 或 [群体](../../endpoint/group) 的 [引用](../reference/)。**当 `type` 是 `"Birth"` 或 `"Death"` 时不可用**|
| `influenced_by`   | array         | 可选        | json 对象数组，每个都是对以某种可注意方式影响或激励活动的实体的 [引用](../reference/)。**当 `type` 是 `"Birth"` 或 `"Death"` 时不可用** |
| `used_specific_object` | array    | 可选        | json 对象数组，每个都是对执行此活动时具有重要作用的实体的 [引用](../reference/)。**当 `type` 是 `"Birth"` 或 `"Death"` 时不可用** |
| `technique` | array | 可选 | json 对象数组，每个都是活动中使用的技术，必须遵循 [类型](../type) 的要求。**当 `type` 是 `"Birth"` 或 `"Death"` 时不可用** |
| `part` | array | 可选 | json 对象数组，每个都是此相同事件类型的另一个实例。**当 `type` 是 `"Birth"` 或 `"Death"` 时不可用** |
| `diminished` | json object | 可选 | json 对象，是对此事件从中移除此对象的另一个物理对象的 [引用](../reference/)。**仅当 `type` 是 `"PartRemoval"` 时可用**|

### 可用的活动类

| 端点/模式        | 开始         | 结束        | 其他        |
|-------------------|---------------|-------------|-------------|
| 抽象作品     | 创作      | -           | -           |
| 概念           | 创作      | -           | -           |
| 数字对象    | 创作      | -           | 活动    |
| 群体             | 形成     | 解散 | 活动    |
| 个人            | 出生         | 死亡       | 活动    |
| 物理对象   | 制作、部分移除 | 毁坏 | 遭遇、修改、活动 |
| 集合               | 创作      | -           | 活动    |
| 文本作品      | 创作      | -           | 活动    |
| 视觉作品       | 创作      | -           | 活动    |
| 陈述         | 创作      | -           | -           |


### 属性图

> ![图](activity_properties.png){:.diagram_img width="600px"}

### 传入属性

活动实例通常作为以下属性的对象被找到。

| 属性名称    | 类        | 描述 |
|------------------|--------------|-------------|
| `created_by`     | 创作     | 概念或数字事物的开始 |
| `formed_by`      | 形成    | 群体的开始 |
| `dissolved_by`   | 解散  | 群体的结束 |
| `born`           | 出生        | 个人的开始 |
| `died`           | 死亡        | 个人的结束 |
| `produced_by`    | 制作   | 物理事物的开始 |
| `removed_by`     | 部分移除  | 物理事物的开始，当它从其他东西中移除时 |
| `modified_by`    | 修改 | 物理事物的修改 |
| `destroyed_by`   | 毁坏  | 物理事物的结束 |
| `encountered_by` | 遭遇    | 物理事物的发现或交互 |
| `used_for`       | 活动     | 事物用于某些活动，通常是发布 |
| `participated_in`| 活动     | 个人或群体参与的活动 |
| `carried_out`    | 活动     | 个人或群体直接进行的活动 |


## 示例

[蒙娜丽莎](../../endpoint/physical_object/)：

  * ... 由列奥纳多·达·芬奇制作
  * ... 在1503年和1506年之间
  * ... 在佛罗伦萨
  * ... 使用绘画技术
  * ... 制作受到丽莎·德尔·乔孔多的影响


```crom
top = vocab.Painting(ident="auto int-per-segment", label="Mona Lisa")
prod = model.Production()
prod.carried_out_by = model.Person(ident="http://vocab.getty.edu/ulan/500010879", label="Leonardo da Vinci")
ts = model.TimeSpan()
ts.begin_of_the_begin = "1503-01-01T00:00:00Z"
ts.end_of_the_end = "1506-12-31T23:59:59Z"
ts.identified_by = vocab.DisplayName(content="1503-1506")
prod.timespan = ts
prod.took_place_at = model.Place(ident="http://vocab.getty.edu/tgn/7000457", label="Florence, Italy")
prod.technique = model.Type(ident="http://vocab.getty.edu/aat/300054216", label="Painting Technique")
prod.influenced_by = model.Person(ident="http://vocab.getty.edu/ulan/500341678", label="Lisa del Giocondo")
top.produced_by = prod
```