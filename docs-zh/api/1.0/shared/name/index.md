---
title: "Linked Art API: 名称结构"
up_href: "/api/1.0/shared/"
up_label: "Linked Art API 1.0 共享数据结构"
---




## 简介

名称是实体的易读标签，通常用自然语言表示。所有实体都可以有多个名称，用于不同的上下文或语言。

## 属性定义

### 名称的属性

| 属性名称          | 数据类型      | 要求        | 描述 |
|-------------------|---------------|-------------|-------------|
| `id`              | string        | 可选        | 标识名称的 URI |
| `type`            | string        | 必需        | 必须是值 `"Name"` |
| `_label`          | string        | 推荐        | 易读标签 |
| `content`         | string        | 必需        | 名称的内容 |
| `language`        | string        | 推荐        | 名称的语言代码 |
| `classified_as`   | array         | 可选        | 名称类型的分类 |
| `referred_to_by`  | array         | 可选        | 关于名称的引用或陈述 |
| `assigned_by`     | array         | 可选        | 名称的分配活动 |

### 使用场景

名称用于为所有类型的实体提供人类可读的标识符，包括个人、群体、地点、对象等。