---
title: "Linked Art API：数字对象"
up_href: "/api/1.0/endpoint/"
up_label: "Linked Art API 1.0 端点"
---




## 简介

数字对象 API 是获取数字内容**描述**的方法，如图像、文档或其他电子媒体，无论该文件是否可以通过网络访问。当数字内容在线可用时，对其本身的访问通过描述中的 `access_point` 属性提供。数字对象 API 具有中等复杂度，具有许多熟悉的属性和模式，以及几个描述对象与其他实体关系的附加内容。

关于数字对象记录用法的更多信息，请参阅[数字模型](/model/digital/)描述。

## 属性定义

通过数字对象端点解析实体会得到一个包含单个 JSON 对象的 JSON-LD 文档，该对象具有以下属性。

### 数字对象的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是数字对象描述可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 数字对象的类，必须是值 `"DigitalObject"` |
| `_label`          | string        | 推荐    | 数字对象的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是数字对象的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是数字对象的名称/标题，必须遵循[名称](../../shared/name/)的要求，或数字对象的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于数字对象的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `equivalent`      | array         | 可选    | JSON 对象数组，每个对象都是对当前数字对象外部身份的[引用](../../shared/reference) |
| `member_of`       | array         | 可选    | JSON 对象数组，每个对象都是当前数字对象成员的集合，必须遵循对集合的[引用](../../shared/reference/)的要求 |
| `subject_of`      | array         | 可选    | JSON 对象数组，每个对象都是对[文本作品](../textual_work/)的引用，其内容聚焦于当前对象，必须遵循[引用](../../shared/reference/)的要求 |
| `representation`  | array         | 可选    | JSON 对象数组，每个对象都是对代表当前对象的[视觉作品](../visual_work)的引用，必须遵循[引用](../../shared/reference/)的要求 |
| `attributed_by`   | array         | 可选    | JSON 对象数组，每个对象都是将当前数字对象与另一个实体相关联的[关系分配](../../shared/assignment/) |
| `dimension` | array | 可选 | JSON 对象数组，每个对象都是所描述数字对象的[维度](../../shared/dimension)，如高度、宽度或总字节数 |
| `part_of` | array | 可选 | JSON 对象数组，每个对象都是对当前数字对象所属的另一个数字对象的[引用](../../shared/reference/) |
| `format` | string | 可选 | 所描述数字对象的媒体类型，例如 "image/jpeg" |
| `conforms_to` | array | 可选 | JSON 对象数组，每个对象都是对当前数字对象符合的外部规范的[引用](../../shared/reference/)。引用的 `type` 值必须是 `"InformationObject"` |
| `digitally_carries` | array | 可选 | JSON 对象数组，每个对象都是对此数字对象承载的[文本作品](../textual_work/)的[引用](../../shared/reference/) |
| `digitally_shows` | array | 可选 | JSON 对象数组，每个对象都是对此数字对象显示的[视觉作品](../visual_work/)的[引用](../../shared/reference/) |
| `digitally_available_via` | array | 可选| JSON 对象数组，每个对象都是数字服务结构，定义如下 |
| `access_point` | array | 可选 | JSON 对象数组，每个对象都是对可以从中检索实际文件表示的 URI 的[引用](../../shared/reference/)，而不是关于它的元数据 |
| `created_by` | json object | 可选 | 表示数字对象创建的 JSON 对象，遵循[创建](../../shared/activity)的要求 |
| `used_for` | array | 可选 | JSON 对象数组，每个对象都是发布活动，遵循[活动](../../shared/activity)的要求 |

### 数字服务的属性

| 属性名称     | 数据类型      | 要求 | 描述 |
|-------------------|---------------|-------------|-------------|
| `@context`        | string, array | 必需    | 值必须是[Linked Art 上下文](../../json-ld/)的 URI，作为字符串 `"https://linked.art/ns/v1/linked-art.json"` 或数组，其中 URI 是最后一个条目以允许[扩展](../../json-ld/extensions) |
| `id`              | string        | 必需    | 值必须是数字对象描述可以[解析](../../protocol/)的 HTTP(S) URI |
| `type`            | string        | 必需    | 数字对象的类，必须是值 `"DigitalService"` |
| `_label`          | string        | 推荐    | 数字对象的人类可读标签，面向开发者 |
| `classified_as`   | array         | 推荐    | JSON 对象数组，每个对象都是数字对象的分类，必须遵循[类型](../../shared/type/)的要求 |
| `identified_by`   | array         | 推荐    | JSON 对象数组，每个对象都是数字对象的名称/标题，必须遵循[名称](../../shared/name/)的要求，或数字对象的标识符，必须遵循[标识符](../../shared/identifier/)的要求 |
| `referred_to_by`  | array         | 可选    | JSON 对象数组，每个对象都是关于数字对象的人类可读声明，必须遵循[声明](../../shared/statement/)的要求 |
| `access_point` | array | 可选 | JSON 对象数组，每个对象都是对可以与之交互的服务 URI 的[引用](../../shared/reference/) |
| `conforms_to` | array | 可选 | JSON 对象数组，每个对象都是对数字服务符合的外部规范的[引用](../../shared/reference/)。引用的 `type` 值必须是 `"InformationObject"` |

### 属性图

> ![diagram](digital_properties.png){:.diagram_img width="600px"}

### JSON 模式

请参阅[模式文档](../../schema_docs/digital)和[模式本身](../../schema/digital.json)

### 传入属性

数字对象实例通常作为以下属性的对象被发现，除了上述自引用属性外。此列表并非详尽无遗，但旨在涵盖其他端点引用数字对象的可能情况。

| 属性名称              | 源端点 | 描述 |
|----------------------------|-----------------|-------------|
| `digitally_carried_by`     | [文本作品](../textual_work/) | 文本可以由物理对象承载，或由数字对象数字承载 |
| `digitally_shown_by`       | [视觉作品](../visual_work/)   | 类似地，图像内容可以由数字对象数字显示 |


## 示例

梵高自画像数字图像的数字对象条目的 JSON 可能如下所示。

* 它在 `@context` 中包含 Linked Art 上下文文档引用
* 它在 `id` 中自文档化其 URI
* 它的 `type` 是 "DigitalObject"
* 它有一个 `_label`，值为 "Digital Image of Self-Portrait of Van Gogh"，供阅读 JSON 的人员使用
* 它被 `classified_as` 为 "Digital Image"，其 `id` 为 "aat:300215302"
* 它被 `identified_by` 为...
    * ...一个 `Name`，内容为 "Self-Portrait Dedicated to Paul Gauguin"
    * ...和一个 `Identifier`，内容为 "47174896"，被 `classified_as` 为所有者分配的编号
* 它有两个 `Dimension` 条目...
    * ...高度（"aat:300055644"）为 2550 像素（"aat:300266190"）
    * ...宽度（"aat:300055647"）为 2087 像素（"aat:300266190"）
* 它是梵高自画像集合的 `member_of`（可能包括数字和物理）
* 它可以从 `access_point` 中的 URI 检索
* 它的媒体类型（或 MIME 类型）为 "image/jpeg"
* 它 `digitally_shows` 与物理绘画相同的视觉内容
* 它是另一个数字对象的 `part_of`，在这种情况下是 IIIF 清单
* 它通过数字服务 `digitally_available_via`，该服务...
    * ... `conforms_to` IIIF 图像 API
    * ...可以在 `access_point` 中的 URI 处交互
* 它被 `created_by` 一个创建，该创建...
    * ...由哈佛艺术博物馆 `carried_out_by`
    * ... `used_specific_object` 物理绘画

```crom
top = vocab.DigitalImage(ident="auto int-per-segment", label="Digital Image of Self-Portrait of Van Gogh")
top.identified_by = model.Name(content="Self-Portrait Dedicated to Paul Gauguin")
top.identified_by = vocab.LocalNumber(content="47174896")

top.access_point = model.DigitalObject(ident="https://ids.lib.harvard.edu/ids/iiif/47174896/full/full/0/default.jpg")
top.digitally_shows = model.VisualItem(ident="", label="Visual Content of Self-Portrait of Van Gogh")
top.format = "image/jpeg"
h = vocab.Height(value=2550)
w = vocab.Width(value=2087)
h.unit = vocab.instances['pixels']
w.unit = vocab.instances['pixels']
top.dimension = h
top.dimension = w
svc = model.DigitalService(label="IIIF Service")
svc.access_point = model.DigitalObject(ident="https://ids.lib.harvard.edu/ids/iiif/47174896")
svc.conforms_to = model.InformationObject(ident="https://iiif.io/api/image/2/context.json")
top.digitally_available_via = svc
cre = model.Creation()
cre.carried_out_by = model.Group(ident="harvardartmuseums.org", label="Harvard Art Museums")
cre.used_specific_object = model.HumanMadeObject(ident="https://harvardartmuseums.org/collections/object/299843", label="Self-Portrait of Van Gogh")
top.created_by = cre
top.member_of = model.Set(ident="auto int-per-segment", label="Images of Self-Portraits of Van Gogh")
top.part_of = model.DigitalObject(ident="https://iiif.harvardartmuseums.org/manifests/object/299843", label="IIIF Manifest")

```