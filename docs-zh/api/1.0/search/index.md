---
title: "Linked Art 搜索 API"
up_href: "/api/1.0/"
up_label: "Linked Art API 1.0"
---


## 概述

遵循每个关系应该只在一个记录中的[原则](../principles/)，需要一个解决方案让客户端能够从被引用记录而不是具有关系的记录中确定关系存在。例如，对象记录列出了负责创建它的人，因此艺术家记录没有该人创建的对象列表。然而，能够确定哪些对象是由艺术家创作的显然很重要。对此的解决方案是有一个明确定义的搜索交互，这可能是预先计算而不是动态计算的，可用于列出记录之间每个关系的逆关系。此外，为了不定义搜索查询语法（这将很难一致实现），我们使用 HAL 链接模式让客户端简单地检索结果而不是自己生成查询。

## 引用记录链接

指向引用记录列表的链接可以添加到`_links`块中，在[HAL](../hal/)规范中定义。

链接根据当前记录的类型、它与响应中实体的关系以及这些实体的预期类型以驼峰命名法命名。例如，关于当前对象的作品集合将是`object`加上`SubjectOf`（作为`about`的逆）加上`Work`。这种约定有助于确保将来版本中不会发生命名冲突。

在浏览器中检索链接名称的 URI（通过使用`curies`部分中的模板扩展名称生成），将显示关于该特定链接的文档。例如，参见 [objectPartOfObject](https://linked.art/api/rels/1/objectPartOfObject)。可能的链接完整集合在`curies`块中给出的[URI](/api/rels/1/)中描述。

如果没有其他记录参与该关系（例如，该人没有创建任何对象，或者该对象没有任何部分），那么链接不应该出现在`_links`列表中。这将防止客户端发出不必要的请求来检索不存在的信息。

`href`中给出的 URI 没有结构要求。它可以是带查询参数的搜索、链接名称和对象标识符的直接转换，或任何其他内容。唯一的要求是它在检索时产生正确的响应格式，如下定义。

一个完整的 HAL `_links`块可能看起来像：

```
{
  "_links": {
    "self": "http://example.org/linked_art/objects/1234"
    "curies": [
      {"name":"la","href":"https://linked.art/api/rels/1/{rel}","templated":true}
    ],
    "la:modelVersion": {"href":"https://linked.art/model/1.0/", "name": "v1.0"},
    "la:apiVersion": {"href":"https://linked.art/api/1.0/", "name": "v1.0"},
    "la:localVersion": {"href":"https://example.org/extension/maps/geo-210", "name": "v2.1.0-beta-01"},

    "la:objectHasPartObject": {"href": "https://example.org/api/objectHasPartObject/1234/1"},
    "la:objectSubjectOfWork": {"href": "https://example.org/api/objectSubjectOfWork/1234/1"}
  }
}
```

## 搜索响应格式


下面描述的格式不是新的，在文化遗产 API 生态系统内的各种地方使用。它基于[Activity Streams 2.0](https://www.w3.org/TR/activitystreams-core/#collections)的集合模型，并在诸如[IIIF 更改发现 API](https://iiif.io/api/discovery/)、[IIIF 内容搜索 API](https://iiif.io/api/search/)、[W3C 的 Web 注释模型](https://www.w3.org/TR/annotation-model/#collections)等规范中使用。这是一个非常直接的分页模型，其中服务器而不是客户端定义页面大小。

本文档不会详细介绍格式，而是专注于实现所需的核心功能。如果需要极其详细的说明，那么阅读上述链接将提供那种体验。

该格式有两个主要响应：项目或结果的整体集合，它包含枚举所包含项目的一个或多个页面。来自记录的[HAL](../hal/index.md)链接将引用集合的第一页，而不是直接引用集合。然后集合嵌入在每个页面中，意味着它永远不必单独解析。


### 结果页面

结果页面具有非常简单的结构，具有以下属性：

* `@context` - 必须存在，值为 `"https://linked.art/ns/v1/search.json"`
* `id` - 必须存在，值为页面的 URI
* `type` - 必须存在，值为字符串 `"OrderedCollectionPage"`
* `partOf` - 必须存在，值为集合的 JSON 对象，在下一节描述。
* `next` - 必须存在，除非是最后一页。值是一个 JSON 对象，恰好有两个属性：`id`是集合中下一页的 id，`type`值为 `"OrderedCollectionPage"`。
* `prev` - 必须存在，除非是第一页。值是一个 JSON 对象，恰好有两个属性：`id`是集合中上一页的 id，`type`值为 `"OrderedCollectionPage"`。
* `startIndex` - 应该存在，值为整体集合中`orderedItems`列表中第一个条目的从0开始的索引。
* `orderedItems` - 必须存在，值为项目数组。每个项目是一个 JSON 对象，恰好有两个属性：来自包含的 Linked Art 记录的`id`和`type`。

因此，一个示例页面将是：

```json
{
	"@context": "https://linked.art/ns/v1/search.json",
	"id": "https://example.org/api/objectHasPartObject/1234/2",
	"type": "OrderedCollectionPage",
	"partOf": { },
	"next": {
		"id":"https://example.org/api/objectHasPartObject/1234/3",
		"type": "OrderedCollectionPage"
	},
	"prev": {
		"id":"https://example.org/api/objectHasPartObject/1234/1",
		"type": "OrderedCollectionPage"
	},
	"startIndex": 20,
	"orderedItems": [
		{
			"id":"https://example.org/data/object/1234-21",
			"type": "HumanMadeObject"
		},
		{
			"id":"https://example.org/data/object/1234-22",
			"type": "HumanMadeObject"
		}
	]
}
```

### 集合

集合代表整体搜索结果（或其他项目集合）。在 Linked Art 中，它嵌入在每个页面中，但也可能单独可用。

集合具有以下属性：

* `@context` - 如果集合被单独请求，则必须存在，值为 `"https://linked.art/ns/v1/search.json"`。嵌入时不得存在。
* `id` - 必须存在，值为集合的 URI。
* `type` - 必须存在，值为字符串 `"OrderedCollection"`
* `first` - 必须存在。值是一个 JSON 对象，恰好有两个属性：`id`是集合第一页的 id，`type`值为 `"OrderedCollectionPage"`。
* `last` - 必须存在。值是一个 JSON 对象，恰好有两个属性：`id`是集合最后一页的 id，`type`值为 `"OrderedCollectionPage"`。
* `totalItems` - 应该存在，值为整个集合中条目的计数。
* `label` - 可能存在。如果存在，值是一个 JSON 对象，键是语言的双字母代码，值是字符串数组，其中每个字符串是该语言中集合的名称或标签。
* `summary` - 可能存在。如果存在，值是一个 JSON 对象，键是语言的双字母代码，值是字符串数组，其中每个字符串是该语言中集合的描述或摘要。

嵌入在页面中的集合可能看起来像：

```json
{
	"@context": "https://linked.art/ns/v1/search.json",
	"id": "https://example.org/api/objectHasPartObject/1234/2",
	"type": "OrderedCollectionPage",
	"partOf": {
		"id": "https://example.org/api/objectHasPartObject/1234/",
		"type": "OrderedCollection",
		"first": {
			"id": "https://example.org/api/objectHasPartObject/1234/1",
			"type": "OrderedCollectionPage"
		},
		"last": {
			"id": "https://example.org/api/objectHasPartObject/1234/10",
			"type": "OrderedCollectionPage"
		},
		"totalItems": 195,
		"label": {
			"en": ["手稿1234的部分"]
		},
		"summary": {
			"en": ["手稿1234有195页，每页分别描述"]
		}
	}
}
```