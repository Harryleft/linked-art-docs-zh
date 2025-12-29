---
title: "对象：权利信息"
up_href: "/model/object/"
up_label: "对象"
---



## 简介

关于物理对象及其数字表示的权利信息是重要的需要捕捉的信息。对于关于权利信息的一般、文本陈述，模型使用现在应该熟悉的LinguisticObject模式。对于可以单独识别的更具体权利，如版权，以及可选谁持有这些权利，有能力以机器可读的方式声明它们。

## 致谢/归属声明

能够提供应与对象一起显示的致谢或归属声明是很重要的。例如，被捐赠的绘画可能有说明捐赠者是谁的要求。这使用断言模式建模为`LinguisticObject`，分类为_aat:300026687_ - "致谢"的术语。文本在`content`属性中给出。

**示例**：

《夜巡》从阿姆斯特丹市出借给国家博物馆。

```crom
top = model.HumanMadeObject(ident="nightwatch/15", label="伦勃朗的夜巡")
top.referred_to_by = vocab.CreditStatement(content="阿姆斯特丹市出借")
```

## 权利声明

对于关于权利或许可的一般声明，信息可以以与致谢或归属相同的方式提供。区别在于它被分类为_aat:300435434_ - 许可或法律声明的术语。
此类权利声明可能与物理对象或视觉作品关联，但应该与作品关联（具有或曾经具有版权的图像，而不是承载它的物质片段）。


**示例**：

《夜巡》的视觉内容在公共领域。

```crom
top = model.VisualItem(ident="nightwatch/1", label="夜巡的视觉内容")
top.referred_to_by = vocab.RightsStatement(content="公共领域")
```

## 权利断言

然而，更详细的信息通常可用并且明确表示是有用的。这些模式将对象`subject_to`的`Right`关联，然后给出关于该权利性质的更多细节，如什么类型的权利，以及谁持有它。

每个权利专门与受权利约束的实体相关联，而不是此类权利的更广泛类别，因此权利是对象的状态，而不是法律构造。我们仍然需要一种方式来引用被声明的权利或许可的类型，为此我们使用`classified_as`属性。分类的URI可以是任何东西，但最常见的是rightsstatements.org URI或[知识共享](https://creativecommons.org/) URI。

最近有一项标准化权利声明的努力，在[rightsstatements.org](http://rightsstatements.org/)描述。确定了十二个基本权利声明并给出URI来标识它们。如果这些声明中有任何适用，使用这些URI以确保客户端系统可以以相同方式处理它们是有用的。

如果这些权利是关于图像的版权或其他使用而不是物理对象，那么这些权利必须与作品而不是对象关联。声明您可以重用《夜巡》并不会给您国家博物馆中对象的任何物理权利，它给您视觉内容的使用权。

**示例**：

《夜巡》的视觉内容在公共领域。

```crom
top = model.VisualItem(ident="nightwatch/2", label="夜巡的视觉内容")
r = model.Right(label="夜巡的公共领域状态")
t = model.Type(ident="https://creativecommons.org/publicdomain/zero/1.0/", label="公共领域")
r.identified_by = model.Name(content="公共领域")
r.classified_as = t
top.subject_to = r
```