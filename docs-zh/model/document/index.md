---
title: 文本和文档
---



## 简介

本节记录包含文本的文档的模型，包括中世纪手稿等艺术品，信件、账本或日记等档案材料，期刊、文章和专著等学术交流，网页等数字对象，或任何其他类型的书面交流。

目的不是成为一个全面的模型，适用于基于图的图书馆管理系统、档案查找辅助工具或任何数字资源的目录，而是提供足够的描述，使对象能够被识别、理解，并能够在其他更具体的系统和本体中被引用。该模型旨在足以用于引用与艺术品相关的文本的基本用例，无论它们是在图书馆、档案馆、博物馆还是互联网上保存。

值得注意的是，它不尝试重现 [FRBR](https://www.ifla.org/node/2016) 和类似抽象模型的形式化，如 [FRBRoo](https://www.ifla.org/publications/node/11240)、[BibFrame](http://www.loc.gov/bibframe/docs/index.html) 或其他复杂的概念层次结构，而是提供尽可能简单的模型来完成核心的书目引用任务。

## 物理对象、概念文本

第一个需要的区别是文本的物理或数字载体与文本本身之间的区别。像[对象显示的艺术品视觉内容](/model/object/aboutness/#depiction)的 `VisualItem` 模式一样，代表作品文本的 `LinguisticObject` 可以被多个 `HumanMadeObject` `carried`，并被 `DigitalObject` 实例 `digitally_carried_by`。这样，特定书籍的所有副本都携带相同的信息内容，只需要描述一次，并可以作为单个连接点。

像其他 `LinguisticObject` 一样，它可以有用于作品实际文本的 `content` 属性、分类、语言等。

!!! note "口述历史"
    语言内容不需要用符号写下来才能被认为是 `LinguisticObject`，它可以完全通过口头传统传播。同样，采访可以在没有转录的情况下被记录，传播的信息仍然是 `LinguisticObject`，因为它是通过人类语言的使用传播的，而不是视觉描述。


__示例：__