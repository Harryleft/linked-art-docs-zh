---
title: "对象：物理特征"
up_href: "/model/object/"
up_label: "对象"
---



## 简介

艺术品有几个重要的物理特征需要捕捉，包括尺寸、形状、颜色和制作材料。模型允许在数据中明确表示这些特征，也允许简单地包括文本描述。明确形式是首选，但认识到并非所有系统都能提供。

除了尺寸和材料，模型允许使用基础模式描述对象的部分以及部分的部分。这些部分可以被认为是独立的对象，因此有标题（三联画的"左翼"）、描述、权利、图像、尺寸、材料等等。

## 尺寸

对象的物理尺寸，如高度、宽度、直径或重量，包含在`dimension`属性中，由三个主要信息组成：

* `value`中的数值。
* `classified_as`中的尺寸类型（如高度vs宽度），引用外部尺寸类型词汇表。
* 用于将值与现实世界对齐的`unit`，如英寸、磅或秒。单位也应从受控词汇表中给出。

**示例**：

《夜巡》高379.5厘米，宽453.5厘米。

```crom
top = vocab.Painting(ident="nightwatch/6", label="伦勃朗的夜巡")
w = vocab.Width(value=453.5)
w.unit = vocab.instances['cm']
top.dimension = w
h = vocab.Height(value=379.5)
h.unit = vocab.instances['cm']
top.dimension = h
```

### 尺寸断言

如果尺寸文本的记录方式不利于生成完整集合，那么可以作为`LinguisticObject`给出，通过引用_aat:300435430_分类为尺寸，并在`content`中提供文本。这是断言基础模式的一个示例。

**示例**：

《夜巡》的尺寸，包括重量，以人类可读文本描述。

```crom
top = vocab.Painting(ident="nightwatch/7", label="伦勃朗的夜巡")
dims = vocab.DimensionStatement()
dims.content = "高度 379.5 cm × 宽度 453.5 cm × 重量 337 kg"
top.referred_to_by = dims
```

### 尺寸显示标签

另一种方法是让数据中的尺寸包含尺寸所代表的值的人类可读标签。这允许客户端以特定样式呈现数据，而不必从尺寸值、单位和类型生成文本。

同样的方法可以用于许多数据结构，这里只是为了比较仅数据结构的机器导向观点和仅完整描述作为断言的人类导向观点而特别提及。

**示例**：

再次是《夜巡》，每个尺寸都描述了人类可读的标签。

```crom
top = vocab.Painting(ident="nightwatch/8", label="伦勃朗的夜巡")
w = vocab.Width(value=453.5)
w.unit = vocab.instances['cm']
top.dimension = w
h = vocab.Height(value=379.5)
h.unit = vocab.instances['cm']
top.dimension = h
w.identified_by = vocab.DisplayName(value="宽 453.5 cm")
h.identified_by = vocab.DisplayName(value="高 379.5 cm")
```


### 尺寸测量

在某些情况下，拥有关于尺寸如何测量的更多信息也很重要。这可能很有用，例如，为了区分测量进行的时间和方法，或者在保护研究环境中了解谁使用了哪种仪器以促进结果的准确性和可重用性。

为了在上述尺寸模型的基础上构建，模型向`Dimension`添加一个`AttributeAssignment`活动，即测量活动，遵循[断言](/model/assertion/)模式。`Dimension`通过`AttributeAssignment``assigned_by`给具有该尺寸的对象。在这种特殊情况下，由于尺寸特定于对象，并且`dimension`属性在模型中已经明确，不需要从`AttributeAssignment`链接回对象，或者给出被分配的属性。这是允许的，但没有添加新信息，因此不推荐。

**示例**：

《夜巡》的测量由"夜巡行动"团队在"[夜巡行动](https://www.rijksmuseum.nl/en/stories/operation-night-watch)"期间进行

```crom
top = vocab.Painting(ident="nightwatch/9", label="伦勃朗的夜巡")
h = vocab.Height(value=379.5)
h.unit = vocab.instances['cm']
top.dimension = h
aa = model.AttributeAssignment(label="夜巡测量")
h.assigned_by = aa
aa.carried_out_by = model.Group(ident="nightwatchteam", label="夜巡行动团队")
aa.part_of = model.Activity(ident="operationnightwatch", label="夜巡行动")
```

### 对象特征的测量

测量特定对象的部分是很常见的，如雕像的底座或绘画的载图部分，或者对象在特定状态下的测量，如箱子盖子打开而不是关闭时的高度。如果有部分的记录，与完整对象分离，那么尺寸可以直接与对象的那部分关联，但为所有可测量的方面制作单独记录是不方便的，并且以这种方式管理对象状态是不可能的。

如果不需要连接多个尺寸，并且没有互操作性或可搜索性要求能够以计算方式区分它们，那么显示名称或断言可能足以向人类读者解释测量的是什么。

如果这是一个要求，那么我们改为在前一节讨论的`AttributeAssignment`上添加`technique`属性，作为引用测量进行方式的方法。技法将表示，例如，"测量底座"或"打开时测量"。相同的技法将添加到特定特征的每个测量中——雕像底座的高度、宽度和深度都将具有"测量底座"技法，作为将它们连接在一起的方式。

/// note | 注意：缺失词汇表
这些技法不太可能存在于共享词汇表中，因此实施者很可能必须根据本地实践创建自己的。
///

**示例**：

《春天》有"装裱[外尺寸]"和"未装裱"尺寸。"未装裱"高度和宽度为74和51.5厘米。

```crom
top = vocab.Painting(ident="spring/29", label="春天")
h = vocab.Height(value=74)
h.unit = vocab.instances['cm']
top.dimension = h
aa = model.AttributeAssignment(label="未装裱测量")
aa.technique = model.Type('measuring_unframed', label="未装裱测量")
h.assigned_by = aa
w = vocab.Width(value=51.5)
w.unit = vocab.instances['cm']
top.dimension = w
aa2 = model.AttributeAssignment(label="未装裱测量")
aa2.technique = model.Type('measuring_unframed', label="未装裱测量")
w.assigned_by = aa2
```


### 颜色

对象的主要颜色可以通过两种非常不同的方式确定和记录——通过捕捉光波长或颜色成分的非常特定值（例如，在红/绿/蓝色彩空间中），或者将对象分类为更广泛、主观的颜色类型（"淡绿色"、"赭色"）。第一种方法可能通过测量原始反射光的仪器，或通过数字摄影并从生成的数字图像计算颜色来完成。第二种方法可能由策展人在集合管理系统中描述对象时进行，希望使用受控的术语集合。由于希望在只有一个地方查找信息，颜色模型试图以尽可能简单的方式同时捕捉这两种可能性，允许对任何给定颜色进行其中一种或两种操作。

测量记录一个`Dimension`，因此我们创建类的实例来记录颜色，即使测量是分类。尺寸有`value`和`unit`，就像上面描述的更明显的物理尺寸一样。对于RGB色彩空间，值必须从更传统的三部分十六进制值转换为整数，因为值总是十进制的。这允许记录真实值。尺寸也可以`classified_as`为特定的颜色族——例如，对象具有绿色的颜色。可以使用这些模式中的一个或两个，并且可以使用此模式记录多个尺寸，而不必匹配哪些类别映射到哪些值。颜色的传统十六进制字符串可以作为尺寸标识符的`content`给出。

**示例**：

《夜巡》主要是棕色（`B35A1F`），被分类为棕色（_aat:300127490_）

```crom
top = vocab.Painting(ident="nightwatch/10", label="伦勃朗的夜巡")
c = vocab.Color(label="棕色")
c.identified_by = model.Identifier(content="#B35A1F")
c.classified_as = vocab.instances['color brown']
c.value = 11754015.0
c.unit = vocab.instances['rgb_colorspace']
top.dimension = c
```

!!! note "实施注意"

	在大多数编程语言中，从十六进制值生成整数值通常非常容易。例如，在Python中，它只是`int("B35A1F", 16)`。反过来也是如此，等价的是`hex(11754015)`。因此，从数据可读性的角度来看，`11754015`的不明显值并不理想，但实施非常简单，因此与所有其他尺寸的一致性被认为比具有取字符串而不是整数的`value`特殊情况提供更多的可用性。包含十六进制代码的字符串可以作为维度实例上的标识符携带。


## 形状

虽然一些尺寸组合可以给出对象形状的感觉，但通常更明确也很有用。例如，盾形绘画（可能因为在实际盾牌上绘画）可能仍然只给出高度和宽度。没有形状的额外信息，可能会得出绘画是矩形的结论。类似地，圆形对象可能被误认为是正方形，因为高度和宽度在任一情况下都相同。

形状通过`classified_as`属性作为对象的分类给出。分类然后进一步分类为形状，使用术语_aat:300056273_，与绘画进一步分类为作品类型的方式相同。

**示例**：

《夜巡》是横向格式的绘画，因为它比高更宽。

```crom
top = vocab.Painting(ident="nightwatch/11", label="伦勃朗的夜巡")
top.classified_as = vocab.instances['oblong']
```

## 材料

对象使用不同的材料创作，如帆布或大理石。这些直接使用对象上的`made_of`属性记录。材料是材料类型，而不是特定的物质，因此引用外部词汇表中的条目。如果可能，最好使用此模型，结合下一节描述的部分模型，允许全面了解哪些部分是哪些尺寸、形状、颜色和由哪些材料制成。

请注意，材料不需要像形状那样的类型-类型模式，因为它们有自己的用于区分它们的`Material`类。还要注意，材料应该是艺术品的特定材料，而不是用于应用材料的工具。例如，材料应该是石墨，而不是铅笔，因为铅笔可以用作创作（非常小的）雕塑的材料。


**示例**：

《夜巡》由油画颜料和帆布制成。

```crom
top = vocab.Painting(ident="nightwatch/12", label="伦勃朗的夜巡")
top.made_of = vocab.instances['oil']
top.made_of = vocab.instances['canvas']
```

### 材料断言

与尺寸断言类似，可以使用通过_aat:300435429_分类为关于对象材料的`LinguisticObject`来描述材料。

**示例**：

《夜巡》是"布面油画"。

```crom
top = vocab.Painting(ident="nightwatch/13", label="伦勃朗的夜巡")
top.referred_to_by = vocab.MaterialStatement(content="布面油画")
```

## 部分

如[基础模式](/model/base/)所述，使用的主要建模范式之一是将实体的部分与整体分离。物理对象特别适合于此，并根据需要允许模型的其余部分重用。部分不需要在不破坏对象的情况下物理上可分离，但需要在构成它的物质方面客观上可定义。例如，雕塑的手臂可以有尺寸和材料，而岩石构造中的拱形空间可能有尺寸，但它不能被移除，也不是由任何东西制成的，因此它不是一个部分。

物理部分使用`part_of`属性链接到整体，并使用相同的`HumanMadeObject`类。`classified_as`属性可以用于更具体地说明部分的类型，在这种情况下是绘画的支撑物，而支撑物又由帆布制成。部分类型然后进一步分类为_aat:300241583_以确保它可以区分为部分类型，而不是对象类型。

模型没有单独的部分断言以人类可读的方式描述这一点，因为这通常如上所述使用材料断言来完成。

**示例**：

《夜巡》的支撑物部分由帆布制成，是《夜巡》的一部分。

```crom
top = vocab.SupportPart(ident="nightwatch/support", label="夜巡的支撑物")
top.made_of = vocab.instances['canvas']
top.part_of = model.HumanMadeObject(ident="nightwatch", label="伦勃朗的夜巡")
```

### 对象的侧面

虽然一些艺术品可以被视为二维的，因为唯一感兴趣的部分是平面表面的正面，如绘画、素描或照片，但有许多其他对象需要分别记录正面和背面，或任何其他数量的侧面的信息。

这种模式允许页面的正面和反面、硬币的正面和背面有独立的身份，方式与绘画的画框或帆布相同。使用分类_aat:300133025_（艺术品）对于区分应被视为完整艺术品的对象、它的部分或它所属的对象很重要。

**示例**：


在马奈的《春天》背面有铭文"11505F"。

```crom
top = vocab.BackPart(ident="spring/back", label="马奈的春天的背面")
top.part_of = model.HumanMadeObject(ident="spring", label="马奈的珍妮（春天）")
top.referred_to_by = vocab.InscriptionStatement(content="11505F")
```

### 部分数量

一些对象比其他对象有更多的部分，独立描述它们都是不切实际的。例如，国际象棋可能由33个部分组成（棋盘、16个白棋子、16个黑棋子），而被打碎的花瓶可能由数百个碎片组成。可以使用上述`dimension`模式记录对象的部分数量，无论它们是否被独立描述。

**示例**：

迈克尔·莫德的"带有微型国际象棋的容器"由36个部分组成（32个棋子、棋盘、盖子和另外两个部分）

```crom
top = model.HumanMadeObject(ident="chess/1", label="微型国际象棋")
top.identified_by = vocab.PrimaryName(content="带有微型国际象棋的容器")
dim = model.Dimension()
dim.value = 36
dim.unit = model.MeasurementUnit(ident="http://vocab.getty.edu/aat/300241583", label="组件")
dim.classified_as = model.Type(ident="http://vocab.getty.edu/aat/300404433", label="计数")
top.dimension = dim
```