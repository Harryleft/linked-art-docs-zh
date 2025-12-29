---
title: 对象的创作与毁坏
up_href: "/model/object/"
up_label: "对象"
---



## 简介

本节涵盖对象存在的开始与结束，以及艺术家与对象创作的归属关系。

## 基础创作活动

对象生命周期中的第一个活动是其创作，使用 `Production` 类来描述。从对象到活动的关系是 `produced_by`，而 `Production` 活动本身遵循通用的[基础活动模型](/model/base/#events-and-activities)，包括时间、地点和行动者的描述。

**示例**：

与基本模式中的制作示例类似，《夜巡》由伦勃朗于1642年在阿姆斯特丹创作。

```crom
top = model.HumanMadeObject(ident="nightwatch/5", label="伦勃朗的夜巡")
prod = model.Production()
top.produced_by = prod
prod.carried_out_by = model.Person(ident="rembrandt", label="伦勃朗")
when = model.TimeSpan(label="1642")
when.begin_of_the_begin = "1642-01-01T00:00:00Z"
when.end_of_the_end = "1642-12-31T23:59:59Z"
prod.timespan = when
prod.took_place_at = model.Place(ident="amsterdam", label="阿姆斯特丹")
```

## 技法与分类

我们区分用于创作艺术品的技法和其它分类。技法有自己的属性（`technique` 而不是 `classified_as`），因此可以很容易地与其它分类区分开来。

### 技法

如果已知在对象创作中使用了特定技法，可以使用 `technique` 属性来表达，引用该技法的受控词表术语。这应该用于捕捉特定技法或方法，而基础的 `classified_as` 属性用于活动的更一般分类。更一般的分类在单个角色中更常见，将在下面讨论。

**示例**：

[雕塑《男子半身像》](https://collections.britishart.yale.edu/catalog/tms:54430)由弗朗西斯·哈德伍德使用雕塑技法创作。

```crom
top = vocab.Sculpture(ident="bust/1", label="男子半身像")
prod = model.Production()
prod.carried_out_by = model.Person(ident="http://vocab.getty.edu/ulan/500015886", label="弗朗西斯·哈德伍德")
prod.technique = vocab.instances['sculpting']
top.produced_by = prod
```

## 多位艺术家（不同角色）

如果多位艺术家合作创作同一件艺术品，我们遵循分割模式，创建主 `Production` 活动的独立部分。每个组成部分捕捉特定艺术家在对象创作中角色的详细信息。这使我们能够为每位艺术家的贡献声明不同的属性，包括不同的时间、技法、角色、地点或影响。

为了保持一致性，建议在只知道一位艺术家的情况下也使用此模式，以便更容易地为作品添加更多贡献者而无需重构内容。然而，这不是必需的，以确保与现有系统的兼容性。

请注意，这些制作部分也可以有与之关联的断言，除了分类、技法或其他结构化数据之外，更详细地描述角色。

**示例**：

一幅名为《RÜN》的[彩绘纺织品](https://artgallery.yale.edu/collections/objects/153900)，其中亚麻布由莎拉·帕克手工编织，然后由马克·巴罗绘画。


```crom
top = vocab.Painting(ident="run/1", label = "RUN")
prod = model.Production()
top.produced_by = prod
act1 = model.Production()
act1.technique = vocab.instances['painting']
act1.carried_out_by = model.Person(ident="barrow", label="马克·巴罗")
prod.part = act1
act2 = model.Production()
act2.technique = model.Type(ident="http://vocab.getty.edu/aat/300053643", label="手工编织")
act2.carried_out_by = model.Person(ident="parke", label="莎拉·帕克")
prod.part = act2
```

## 与创作相关的对象

其他对象在艺术品的创作中可能发挥关键作用，如复制其他艺术品或受其启发，或使用相同来源创作艺术品，无论是机械还是手工，如用于打印照片的底片或用于印刷蚀刻版的版材。

### 灵感、研究或复制品

一些艺术品是其他艺术品的复制品，或明显直接受其他作品启发。与另一作品的这种关系可以用 `Production` 活动的 `influenced_by` 属性来捕捉。复制品可能来自记忆或在复制品实物在场的情况下制作，可以是忠实的复制品或仅仅是可识别的相似。这包括为作品的最终版本所做的研究。模型中不捕捉影响的确切性质。

**示例**：

1964年，迪恩·凯勒创作了丹尼尔·亨廷顿1858年[詹姆斯·德怀特·达纳的肖像](https://artgallery.yale.edu/collections/objects/52687)的[复制品](https://artgallery.yale.edu/collections/objects/54339)。

```crom
top = vocab.Painting(ident="kellerdana/1", label="亨廷顿肖像复制品")
prod = model.Production()
top.produced_by = prod
copied = model.HumanMadeObject(ident="huntingtondana", label="达纳的亨廷顿肖像")
prod.influenced_by = copied
prod.carried_out_by = model.Person(ident="keller", label="迪恩·凯勒")
```

### 从可识别来源的复制

许多对象直接从来源创作，如从底片打印的照片、从木刻版创作的版画，或从模具制作的雕塑。特定来源对象的使用可以用 `used_specific_object` 属性作为对象 `Production` 描述的一部分来捕捉。

请注意，从同一来源创作的所有艺术对象将显示相同的图像，无论是平面的还是三维的。来源也显示相同的图像，虽然可能以某种方式反转。图像被建模为所有物理对象显示的 `VisualItem`，允许我们将对象组合在一起。关于作品的更多信息，请参见[相关性](../aboutness/)部分。

设备或工具，如特定的相机或调色板，也将使用相同的属性 `used_specific_object` 建模，但是当然不会显示与主作品相同的视觉项目。

**示例**：

阿尔弗雷德·斯蒂格利茨拍摄的乔治亚·奥基夫的照片复制品，在不同时间从同一底片打印，现在由不同机构拥有：[耶鲁大学美术馆](https://artgallery.yale.edu/collections/objects/198690)、[国家美术馆](https://www.nga.gov/collection/art-object-page.60057.html)和[乔治亚·奥基夫博物馆](https://collections.okeeffemuseum.org/object/6627/)

```crom
top = vocab.Photograph(ident="okeeffe-gok/1", label = "GOK 1918, GOKM")
top.identified_by = vocab.AccessionNumber(content="2014.3.78")
prod = model.Production(label = "照片打印")
top.produced_by = prod
negative = model.HumanMadeObject(ident="okeeffe-negative", label = "GOK 1918底片")
prod.used_specific_object = negative
vi = model.VisualItem(ident="okeeffe", label="GOK 1918的视觉内容")
top.shows = vi
```

```crom
top = vocab.Photograph(ident="okeeffe-yuag/1", label = "GOK 1918, YUAG")
top.identified_by = vocab.AccessionNumber(content="2016.101.242")
prod = model.Production(label = "照片打印")
top.produced_by = prod
negative = model.HumanMadeObject(ident="okeeffe-negative", label = "GOK 1918底片")
prod.used_specific_object = negative
vi = model.VisualItem(ident="okeeffe", label="GOK 1918的视觉内容")
top.shows = vi
```

**示例**：

耶鲁大学英国艺术中心的一幅[版画](https://collections.britishart.yale.edu/catalog/tms:6141)，乔叟的《坎特伯雷朝圣者》，使用耶鲁大学美术馆持有的特定[铜版](https://artgallery.yale.edu/collections/objects/11787)制作。

```crom
top = vocab.Print(ident="ccp/1", label="乔叟的坎特伯雷朝圣者")
prod = model.Production(label="从版材印刷")
top.produced_by = prod
prod.used_specific_object = model.HumanMadeObject(ident="ccp-plate", label="CCP版材")
```

```crom
top = model.HumanMadeObject(ident="ccp-plate/1", label="CCP版材")
top.made_of = vocab.instances['copper']
```

## 创作原因

艺术品经常被委托制作，艺术家同意创作艺术品，委托人同意补偿艺术家的努力。[委托](/model/provenance/promises/#commissions-for-artwork)的建模在流传历史部分描述，作为承诺的交换，可能还包括付款。对象可以在其创作中使用 `caused_by` 属性引用此活动。

**示例**：

[Nuveen绘画](https://artgallery.yale.edu/collections/objects/290048)的创作是由其委托引起的。

```crom
top = model.HumanMadeObject(ident="nuveen/1", label="Nuveen绘画")
top.identified_by = vocab.PrimaryName(content="Nuveen绘画")
prod = model.Production()
prod.carried_out_by = model.Person(ident="dine", label="吉姆·戴恩")
prod.caused_by = model.Activity(ident="nuveen_commission", label="委托")
top.produced_by = prod
```

## 未识别或未知艺术家

许多对象由未知或未识别的艺术家创作。虽然可以有一个名为"未识别艺术家"的不同人物记录，但这会很快在系统中创建大量已识别的人，每个只有一次引用。相反，建议创建一个群体记录来代表所有未识别的艺术家，然后每个对象都有其创作由该群体`carried_out_by`，意味着该人工群体集合中的一个（或多个）人。

如果知道艺术家的某些特征，例如他们的国籍或他们活跃的世纪，这些可以是具有这些属性的附加群体。

**示例**：

[Coppa Amatoria](https://artgallery.yale.edu/collections/objects/138452)由来自意大利的未识别艺术家或艺术家创作。

```crom
top = model.HumanMadeObject(ident="coppa/1", label="Coppa Amatoria")
top.identified_by = vocab.PrimaryName(content="Coppa Amatoria")
prod = model.Production()
prod.carried_out_by = model.Group(ident="unknown_italian", label="未识别的意大利人")
top.produced_by = prod
```


## 归属限定符

### 受艺术家影响

如果对象创作与某人之间存在某种联系，该人不是直接的艺术家但影响了创作，那么可以使用 `influenced_by` 属性引用该人。这些通常表达为"仿"、"以...风格"或"以...方式"的归属——它们通过将创作与直接影响它的人（可能是通过其作品体现，而不是通过个人联系）相关联来限定归属。

**示例**：

绘画《洗衣日》有意以温斯洛·霍默的方式创作。

```crom
top = vocab.Painting(ident="washday/1", label="洗衣日")
top.identified_by = vocab.PrimaryName(content="洗衣日")
prod = model.Production()
prod.influenced_by = model.Person(ident="whomer", label="温斯洛·霍默")
top.produced_by = prod
```

### 与艺术家相关的群体归属

即使艺术家或艺术家群体的身份不完全清楚，这些人可能已知是某个群体的一部分，如更著名的"大师"的工作室。在这种情况下，代表工作室的`Group`可以是执行`Production`的行动者：这并不意味着群体的每个成员都参与了，只是其中至少一个参与了，就像说文档由组织编写或发布并不意味着所有员工都为该努力做出了贡献。

我们可以使用群体的`Formation`（创建）上的`influenced_by`属性将其与已知的人连接起来——在示例用例中是工作室的"大师"。"大师"可能没有参与群体，甚至在群体形成时还活着，因此不必然形成群体甚至是其成员。

这种方法可以用于工作室、画室、学生集合、追随者等。不是整个群体创作了对象，而是其中之一或多个创作了。

**示例**：

上述描述的"男子半身像"对象以前被认为由弗朗西斯·哈德伍德工作室创作，这是一个群体。下面的示例是该群体的记录。

```crom
top = vocab.Studio(ident="harwoodstudio/1", label="弗朗西斯·哈德伍德工作室")
fm = model.Formation()
top.formed_by = fm
fm.influenced_by = model.Person(ident="http://vocab.getty.edu/ulan/500015886", label="弗朗西斯·哈德伍德")
```

### 不确定或变化的归属

与历史艺术品相关的一条信息，随着研究和理解的改进而变化的是创作它的艺术家的身份。在`carried_out_by`中引用的行动者是当前的意见，但以前的归属仍然可以记录。用于此的模式在文档的[断言](/model/assertion/)部分有更详细的描述。


## 通过移除的创作

当一个对象从较大的对象中移除时，它可能进入文档存在状态。部分的制作只是整体制作的一部分，但在它被移除之前，它不需要单独的身份或存在。

这种情况相当频繁地发生，既有合法的动机，也有不诚实的动机。在保护工作中，通常需要在将方法应用于整体之前从对象中移除一个微小的碎片进行实验。如果实验有意想不到的副作用，那么整体对象被保存，而以几乎不可察觉的变化为代价。知道样品是在过去生产而现在被移除很重要，而不是在现在创作。

这种情况发生的第二种情景不幸地很常见。如果一个对象，如中世纪手稿，可以通过拆分成部分并单独销售每个部分来获得更高的利润，那么不诚实的卖家就会这样做。不是将一本无害的时祷书出售给单个买家，而是每个照明画都可以单独出售，然后剩余的载文页面要么被丢弃，要么随着时间的推移以大大降低的价格出售。手稿的这种分散今天仍在发生。

为了对此建模，不是使用`Production`，对象通过`PartRemoval`活动`removed_by`。该活动与所有其他活动一样，但它还有一个`diminished`属性，引用部分被移除的整体对象。如果知道来源对象被移除的信息，通常不会对部分有单独的`Production`。


**示例**：

收藏品是Libro dei Notai大师的一页渐进（手稿）页面。[来源](https://artgallery.yale.edu/collections/objects/51500)

```crom
top = vocab.Page(ident="gradualpage/1", label="渐进页面")
rm = model.PartRemoval()
whole = model.HumanMadeObject(ident="gradual", label="渐进")
rm.diminished = whole
top.removed_by = rm
```

## 发现与创作

如果对象通过被发现而不是被创作而进入有记载的历史，那么不是`Production`条目，而是`Encounter`。这适用于化石、宝石或其他自然历史物品，以及被创作但没有关于该创作的信息可用，或者对象的"发现"是物品流传历史的第一个重要条目。此模式可能仅用于对象的发现，而不是其他类型的相遇。

相遇也可以作为单独的事件记录，如[流传历史部分](../../provenance/encounters/)所述。单独的事件必须用于任何不是发现的相遇。

不使用`produced_by`，使用的属性是`encountered_by`，活动的类是`Encounter`。所有其他模式都是相同的，包括相遇发生的地点、谁遇到它、何时发生等等。角色模式也适用，相遇的`part`也是`Encounter`。

**示例**：

化石Torosaurus（VP.04072）于1891年被约翰·贝尔·哈彻发现。

```crom
top = model.HumanMadeObject(ident="torosaurus/1", label="Torosaurus Gladius")
enc = model.Encounter()
enc.carried_out_by = model.Person(ident="hatcher", label="约翰·贝尔·哈彻")
ts = model.TimeSpan()
ts.begin_of_the_begin = "1891-01-01T00:00:00Z"
ts.end_of_the_end = "1891-12-31T23:59:59Z"
enc.timespan = ts
top.encountered_by = enc
```

## 毁坏

对象流传历史链的终点是已知被毁坏时。对象的丢失使链保持开放，因为它可能在将来被找回，但是如果对象被毁坏，那么就没有回头路。因此，对象只有在已知被毁坏时才应被记录为毁坏。

模型使用一个`Destruction`类，表示对象的不复存在。毁坏只适用于单个对象，因此每个对象都有自己的毁坏，即使该毁坏是由相同的更广泛事件或活动引起的。这意味着毁坏不是由行动者`carried_out_by`，而是（如下一节所述）另一个活动引起毁坏。

**示例**：

毕加索的绘画《Le Peintre》于1998年9月2日晚约10:30被毁坏（在飞机失事中）。[来源](https://en.wikipedia.org/wiki/Swissair_Flight_111)

```crom
top = vocab.Painting(ident="lepeintre/1", label="毕加索的Le Peintre")
dest = model.Destruction(label="Le Peintre的毁坏")
top.destroyed_by = dest
when = model.TimeSpan()
when.begin_of_the_begin = "1998-09-02T22:20:00Z"
when.end_of_the_end = "1998-09-02T22:40:00Z"
dest.timespan = when
```

### 毁坏原因

如上所述，同一事件或活动可能是许多单个对象毁坏的原因。博物馆被烧毁或以其他方式被毁坏会毁坏许多对象，包括建筑物本身。在较小的规模上，个人毁坏可能是由个人的特定活动引起的。

为了区分毁坏本身及其原因，我们使用毁坏与引起它的活动或事件之间的`caused_by`关系。事件应该像模型中的任何其他事件一样被描述和分类。

**示例**：

Le Peintre因飞机坠毁而被毁坏。（这也可能导致飞机的毁坏、机组人员和乘客的死亡以及许多其他后果）

```crom
top = vocab.Painting(ident="lepeintre/2", label="毕加索的Le Peintre")
dest = model.Destruction(label="Le Peintre的毁坏")
top.destroyed_by = dest
when = model.TimeSpan()
when.begin_of_the_begin = "1998-09-02T22:20:00Z"
when.end_of_the_end = "1998-09-02T22:40:00Z"
dest.timespan = when
act = model.Event(ident="sr111crash", label="瑞士航空111航班坠毁")
dest.caused_by = act
```