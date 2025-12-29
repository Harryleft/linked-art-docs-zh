---
title: "概念"
---



## 简介

概念是 Linked Art 的一个重要方面，包含从对象或其他实体的分类到语言、材料及以外的"思维单元"。在大多数情况下，Linked Art 利用 Getty 的艺术与建筑词库（AAT）来处理概念，而不是定义我们自己的概念，但是模型只在非常有限的情况下[要求](/model/vocab/required/)使用 AAT 术语。

当有用或必要定义新概念，或重新定义现有概念以添加新信息时，我们可以使用模型的这部分来完全描述它们，而不仅仅是引用外部 URI。


## 概念类

有五个核心的概念类：

* `Type` 是通用概念类。以下类是它的子类。
* `Currency` 是金融货币。它的实例被用作货币金额的 `currency` 属性值。这通常只需要详细的[流传历史](/model/provenance/acquisition/)信息。
* `Language` 是人类本机理解的语言，包括通过语音、书写或手势。它的实例被用作语言对象上的 `language` 属性值。
* `Material` 是物理材料类型，如木材、黄金或油画颜料。它的实例被用作人造对象的 `made_of` 属性值。
* `MeasurementUnit` 是阐明如何理解尺寸值的单位，如秒、米或千克。它的实例被用作尺寸上的 `unit` 属性值。

上述所有类都在常规的 `type` 属性中使用，但应该注意尽可能使用正确的类，而不是总是回退到 `Type`。

__示例：__

绘画概念的最小记录。

```crom
top = model.Type(ident="painting/1", label="Painting")
```

## 等价物的重要性

如果要向现有概念添加新信息，或者需要在本地系统中作为记录而不进行更改，那么在新记录的概念中包含带有 `equivalent` 属性的对现有标识符的引用对于语义互操作性非常重要。这在[基础模式](/model/base/#equivalent-data-uris)和[记录引用](/api/1.0/shared/reference/) API 模式中也有描述，但在这里值得重复。

这既适用于新概念记录，如下面的示例，也适用于从任何其他记录到该记录的任何引用。

__示例 1：__

一个设置不同主要名称但等价于 AAT 概念的本地记录。

```crom
top = model.Type(ident="painting/2", label="Local Copy of Painting")
top.identified_by = vocab.PrimaryName(content="Painting")
top.equivalent = model.Type(ident="http://vocab.getty.edu/aat/300033618", label="painting (visual works)")
```

__示例 2：__

夜巡是一幅绘画，使用具有 AAT 概念等价物的本地记录。

```crom
top = model.HumanMadeObject(ident="nightwatch/52", label="Night Watch by Rembrandt")
ptg = model.Type(ident="painting", label="Local Copy of Painting")
ptg.equivalent = model.Type(ident="http://vocab.getty.edu/aat/300033618", label="painting (visual art)")
top.classified_as = ptg
```

## 分区与分类

当涉及概念时，很容易混淆概念作为更广泛概念的一部分与被分类为某种类型概念之间的区别。更广泛的概念是较窄概念所属的概念，与其他概念一起。更广泛的概念是比较窄概念更一般的概念。例如视觉作品是比较绘画概念更广泛或更一般的概念，动物是比较哺乳动物更一般的概念，欧洲人是比较荷兰人更一般的概念。

相反，分类第一个概念的第二个概念是将它分类但不直接包含它的概念。例如，作品类型是绘画概念的类别，分类等级将是哺乳动物的类别，国籍将是荷兰人的类别。这些分类其他概念的概念通常被称为"元类型"，也在[基础模式](/model/base/#types-of-types)中讨论。

概念可以并且应该既有更广泛的术语也有分类，如上面的示例所示。

__示例：__

绘画的概念是一种作品类型，具有视觉艺术品的更广泛概念。

```crom
top = model.Type(ident="painting/3", label="Local Copy of Painting")
top.equivalent = model.Type(ident="http://vocab.getty.edu/aat/300033618", label="painting (visual works)")
top.broader = model.Type(ident="http://vocab.getty.edu/aat/300191086", label="visual works")
top.classified_as = model.Type(ident="http://vocab.getty.edu/aat/300435443", label="type of work")
```

## 概念方案和集合

将概念分组的另一种方式是在概念方案（如 AAT）内，或为某种目的收集在一起的概念集合内。概念集合可能是为了收集具有特定用法但不属于单一层次结构的概念而创建的，如声明、对象或作品的类型。概念可以同时在多个集合中，这些集合也可以分层排列。这种分组是除分区和分类之外安排概念的第三种完全正交的方式。

__示例：__

绘画的概念在本地概念方案中。

```crom
top = model.Type(ident="painting/4", label="Local Copy of Painting")
top.member_of = model.Set(ident="conceptScheme", label="Local Concept Scheme")
```

## 创作和影响

一些概念是其他概念或实体的协调或汇编。例如，"法国历史"的概念可以被认为是与地点"法国"相关的"历史"概念。或者"法国历史，20世纪"的概念将是相同的，只是增加了相关的时间段。

由于这些相关实体不一定也是概念，它们不能属于更窄/更广泛的层次结构——"法国历史"概念不能与法国有更广泛的关系，因为法国是 `Place` 的实例，而不是 `Type` 的实例。

为了管理这些类型的关系，我们使用概念 `Creation` 的 `influenced_by` 属性，它可以引用任何实体。

__示例：__

"法国历史"的概念受到"历史"概念和"法国"地点的影响。

```crom
top = model.Type(ident='historyFrance/1', label="History of France")
cre = model.Creation()
top.created_by = cre
cre.influenced_by = model.Type(ident="history", label="History")
cre.influenced_by = model.Place(ident="france", label="France")
```

## 与 SKOS 的一致性

这个模型受到 [SKOS](https://www.w3.org/TR/skos-primer/)（W3C 的简单知识组织系统规范）的严重影响并且高度兼容。Linked Art 中的概念可以很容易地成为 skos:Concepts，具有不同类型的名称（在 skos 中称为标签）、描述/注释、更窄和更广泛的概念以及其他关系。协调概念通过创作影响模式管理。SKOS 中的概念方案在 Linked Art 中被建模为集合。

因此，任何 SKOS 描述的概念都应该能够以最小的难度转换为 Linked Art。
