---
title: "数字集成"
up_href: "/model"
up_label: "模型"
---



## 简介

Linked Art模型中提供的描述很可能不是它们描述的实体的唯一数字表示。还有数字图像、网页和其他应该从实体描述中引用的相关内容。数字对象也可能是感兴趣的实体，如电子书、网络艺术或具有自己独立记录的数字装置。本节描述如何在Linked Art模型中描述和链接数字资源。

数字对象通常以与物理对象相同的方式处理——它们是信息的载体，而不是信息本身。信息由[作品](/model/object/aboutness/)描述，然后由数字对象数字承载或显示。这确保了数字复制品和物理对象本身都与相同的信息相关。例如，PDF（`DigitalObject`）和该PDF的印刷副本（`HumanMadeObject`）都承载完全相同的文本内容（`LinguisticObject`）。


## 核心数字对象属性

所有数字对象共享一些基本特征，无论它们的特定性质如何。名称、标识符、分类和断言的[基础模式](/model/base/)都以常规方式应用。除了基线之外，数字对象可以具有以下描述特征：

* 访问点 - 实际文件本身可用的URL。为了一致性，URL被赋予`DigitalObject`的`type`，但URL是重要的方面。例如，图像的访问点将是您获得实际像素的URL，而不是图像的链接数据描述。
* 格式 - 数字对象的`format`是其媒体类型，通常称为MIME类型，作为字符串给出。
* 标准 - 许多数字对象进一步符合标准规范，可以使用`conforms_to`属性引用。这与`format`不同，因为规范可能没有媒体类型，也与`classified_as`不同，后者是更广泛的分类（图像，而不是符合JPEG 2000标准）
* 尺寸 - 数字尺寸遵循与[物理尺寸](/model/object/physical/#dimensions)相同的模式，但可能使用不同类型（文件大小）或相同类型（图像的高度、宽度）和不同单位（字节、像素）。
* 创作 - 数字对象由`Creation`事件而不是`Production`事件创建，但具有相同的活动模型。

这使我们能够一致且连贯地将物理和数字信息载体建模为核心感兴趣的项目。特别是，数字图像文件`digitally_shows``VisualItem`，或`digitally_carries``LinguisticObject`。

!!! note "删除/擦除"
	目前在模型中不可能删除或擦除数字对象。这将在未来的次要版本中添加，可以在[github问题](https://github.com/linked-art/linked.art/issues/524)中讨论


**示例**：

国家博物馆在网上发布了关于他们对《夜巡》保护工作的数字出版物。

```crom
top = vocab.WebPage(ident="operation_nw/1", label="夜巡行动出版物")
top.access_point = model.DigitalObject(ident="https://www.rijksmuseum.nl/en/stories/operation-night-watch")
top.format = "text/html"
top.conforms_to = model.InformationObject("http://w3.org/TR/html")
top.identified_by = model.Name(content="夜巡行动")
dim = model.Dimension(label="220 kb")
dim.unit = vocab.instances['kilobytes']
dim.value = 220
dim.classified_as = model.Type(ident="http://vocab.getty.edu/aat/300265863", label="文件大小")
top.dimension = dim
cre = model.Creation()
cre.carried_out_by = model.Group(ident="rijksmuseum", label="国家博物馆")
ts = model.TimeSpan()
ts.begin_of_the_begin = "2019-07-19T00:00:00Z"
ts.end_of_the_end = "2019-07-21T00:00:00Z"
cre.timespan = ts
top.created_by = cre
top.digitally_carries = model.LinguisticObject(ident="operation_nw_en", label="英文版夜巡行动")
```

### 数字替代品

一些数字表示旨在成为物理对象的忠实复制品。特别是在数字化二维作品时，区分一般描绘对象但可能与其他对象、人物和环境一起的数字图像，与仅显示与物理对象相同视觉内容的数字图像是有用的。我们可以更明确地表示物理对象`shows`与数字图像`digitally_shows`相同的智力内容。

这些图像有时被称为"数字替代品"，因为它们可以代替物理对象。数字替代品可能显示的不仅仅是对象，如色条和尺子，然而视觉项目的主要焦点必须清楚地是对象本身。替代品和描绘之间的界限留给实施组织的政策和实践。

**示例**：

相同的视觉项目由物理绘画和绘画的数字化图像显示。

```crom
top = model.HumanMadeObject(ident="spring/8", label="马奈的珍妮（春天）")
top.identified_by = model.Name(content="珍妮（春天）")
top.shows = model.VisualItem(ident="spring", label="春天的视觉内容")
```

```crom
top = model.DigitalObject(ident="spring/1", label="珍妮（春天）（数字）")
top.identified_by = model.Name(content="珍妮（春天）")
top.digitally_shows = model.VisualItem(ident="spring", label="春天的视觉内容")
```

## 对数字内容的引用

### 数字图像

许多使用Linked Art描述的实体将有描绘它们的数字图像。这些图像对于为数据构建引人注目的用户界面很有用，并且经常在这些界面中占据突出位置。然而这些图像可能不是感兴趣的主要实体，只是被描述实体的表示。如果是这种情况，那么数字对象仅在相对于主要实体的文档中有意义，因此将图像描述嵌入主要实体的记录中既是可接受的也是更方便的。该模式旨在促进在用户界面中显示图像，因此只应使用一些核心属性。


**示例**：

伦勃朗在维基媒体托管的数字图像中被描绘。

```crom
top = model.Person(ident="rembrandt/15", label="伦勃朗")
vi = model.VisualItem()
top.representation = vi
img = vocab.DigitalImage(label="伦勃朗图像")
vi.digitally_shown_by = img
img.format = "image/jpeg"
img.access_point = model.DigitalObject("https://upload.wikimedia.org/wikipedia/commons/b/bd/Rembrandt_van_Rijn_-_Self-Portrait_-_Google_Art_Project.jpg")
```


### 网页

另一个非常常见的场景是有一个关于对象的网页，可能由集合管理系统管理。对人类来说，这个页面比为机器设计的数据有用得多。它可以用`subject_of`属性引用，指向一个分类为网页或_aat:300264578_的`DigitalObject`。主页可以有"text/html"的`format`和其他属性。

**示例**：

在盖蒂收藏中有珍妮的主页。

```crom
top = vocab.Painting(ident="spring/9", label="马奈的珍妮（春天）")
top.identified_by = model.Name(content="珍妮（春天）")
lo = model.LinguisticObject()
top.subject_of = lo
page = vocab.WebPage()
lo.digitally_carried_by = page
page.format = "text/html"
page.access_point = model.DigitalObject("https://www.getty.edu/art/collection/object/103QTZ")
```

### IIIF 清单

[IIIF](http://iiif.io/)，国际图像互操作框架，是使旨在向人类显示的图像和描述可用的非常常见的方式。与数字对象模型有两种主要对齐方式——来自IIIF Presentation API的清单和来自IIIF Image API的图像。

[IIIF Presentation API](http://iiif.io/api/presentation/)清单被认为是一个关于对象的`DigitalObject`，方式与集合信息系统中对象的主页相同。清单中有语言内容，可能与一种或多种语言相关联，因此我们有相同的中间`LinguisticObject`作为`subject_of`属性的值。数字对象的`conformsTo`属性应该用于引用API的顶级URI：[http://iiif.io/api/presentation/](http://iiif.io/api/presentation/)

根据该规范，格式中使用的媒体类型遵循模式：`application/ld+json;profile="http://iiif.io/api/presentation/3/context.json"`

主要版本存在于媒体类型中，允许消费者在多个版本同时可用时区分使用哪个。

**示例**：

珍妮有一个IIIF Presentation API清单。

```crom
top = vocab.Painting(ident="spring/10", label="马奈的珍妮（春天）")
top.identified_by = model.Name(content="珍妮（春天）")
lo = model.LinguisticObject()
top.subject_of = lo
mfst = model.DigitalObject()
mfst.access_point = model.DigitalObject(ident="https://media.getty.edu/iiif/manifest/db379bba-801c-4650-bc31-3ff2f712eb21")
mfst.conforms_to = model.InformationObject("http://iiif.io/api/presentation/")
mfst.format = "application/ld+json;profile='http://iiif.io/api/presentation/3/context.json'"
lo.digitally_carried_by = mfst
```

### IIIF 图像

[IIIF Image API](http://iiif.io/api/image/)是一个`DigitalService`，从中可以请求图像内容的各种衍生版本。此服务通过代表数字图像的`DigitalObject`的`digitally_available_via`属性引用。同一图像可能既有访问点又有图像服务。此模式适用于嵌入表示的图像和具有自己记录的图像。

IIIF图像服务，而不是图像本身，应该具有`conforms_to`属性，该属性引用"http://iiif.io/api/image/"作为`InformationObject`的URI，以便应用程序知道引用的是哪种服务。`format`属性指的是具有`application/ld+json;profile="http://iiif.io/api/image/3/context.json"`媒体类型的图像信息文档（info.json）

**示例**：

珍妮的图像也可通过IIIF Image API服务获得。

```crom
top = vocab.Painting(ident="spring/11", label="马奈的珍妮（春天）")
top.identified_by = model.Name(content="珍妮（春天）")
img = model.VisualItem()
top.representation = img
do = vocab.DigitalImage()
img.digitally_shown_by = do
do.access_point = model.DigitalObject("https://media.getty.edu/iiif/image/8094f61e-e458-42bd-90cf-a0ed0dcc90b9/full/full/0/default.jpg")
svc = model.DigitalService()
svc.access_point = model.DigitalObject(ident="https://media.getty.edu/iiif/image/8094f61e-e458-42bd-90cf-a0ed0dcc90b9")
svc.conforms_to = model.InformationObject("http://iiif.io/api/image")
svc.format = "application/ld+json;profile='http://iiif.io/api/image/3/context.json'"
do.digitally_available_via = svc
```