---
title: JSON-LD 序列化
up_href: "/api/1.0/"
up_label: "Linked Art API 1.0"
---



## 简介

JSON-LD 是使用流行 JSON（JavaScript 对象表示法）格式的关联开放数据序列化，对后端和基于浏览器的开发都很方便。它由 [W3C](https://www.w3.org/TR/json-ld11/) 指定为官方序列化。持续的开发工作在数据链接 JSON W3C [社区组](https://www.w3.org/community/json-ld/)中进行。

JSON-LD 的序列化通过使用上下文文档对开发人员友好，上下文文档指定了 json 对象中使用的键与模型中使用的 RDF 谓词之间的映射。这种抽象允许开发人员使用现有的模式和框架，而数据仍然在底层作为图进行管理。本文档描述了用于 CIDOC-CRM 和其他本体的上下文。

提供模型中使用的术语映射的上下文发布为：
> `https://linked.art/ns/v1/linked-art.json`

## 媒体类型

用于使用上下文的 JSON-LD 表示的媒体类型是：

> `application/ld+json;profile="https://linked.art/ns/v1/linked-art.json"`

这将是响应上 `Content-Type` HTTP 头的值，如果通过内容协商有其他表示可用，那么它可以在请求中的 `Accept` 头中发送。


## 核心要求

对于 JSON 和 JSON-LD 表示，有几个核心要求需要牢记：