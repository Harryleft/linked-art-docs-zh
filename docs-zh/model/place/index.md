---
title: "地点"
---



## 概述

地点是模型中的基础类之一。事件和活动发生在地点，对象存在于某个位置，个人和组织有相关的位置，他们居住或以其他方式与之关联。地点是空间中的范围，独立于时间或该空间中可能存在或不存在的内容。对于建筑作品和由于介质而固定在位置的作品（例如洞穴绘画），地点是一个决定性特征。

地点也形成了与地理信息系统（GIS）和基于地图的用户界面的核心集成点。通过与这些其他系统对齐，我们能够实现更好的可用性和与我们的数据的交互性。假设地点是陆地的，然而这也未必是这种情况。太阳系与巴黎市一样是一个地点。


## 核心信息

实体的所有核心信息都可用于地点，包括标识符、分类、标签、名称、断言、等价物等等。

建议使用外部地理名称系统记录地点的空间层次结构，然而能够将历史位置定位在其更大的地理空间上下文中仍然很有用。这使用与模型中所有其他类相同的分区模式。

**示例：**

荷兰有一个叫阿姆斯特丹的城市。

```crom
top = vocab.City(ident="amsterdam/1", label="Amsterdam")
top.identified_by = model.Name(content="Amsterdam")
top.referred_to_by = vocab.Description(content="Amsterdam is a city in the Netherlands")
top.part_of = vocab.Nation(ident="netherlands", label="Netherlands")
```

## 地理空间位置

地点的预期用户界面需求之一是能够在地图上绘制它们。为了做到这一点，或计算地点的地理空间重叠，有一个描述地点在现实世界中边界的几何形状是很有用的。这可能非常详细，一个地点适合的简单边界框，或接近区域中心的点。

这是通过使用 `defined_by` 属性将[WKT](https://en.wikipedia.org/wiki/Well-known_text_representation_of_geometry)字符串与地点关联来处理的。

坐标参考系统假设使用纬度和经度。规范的未来版本可能有关于不同坐标系统（如非地球位置或相对定位）的更多细节。


**示例：**

一个（非常粗略地）定义新西兰国家的多边形。

```crom
top = vocab.Nation(ident="new_zealand/1", label="New Zealand")
top.defined_by = "POLYGON((165.74 -33.55, -179.96 -33.55, -179.96 -47.8, 165.74 -47.8, 165.74 -33.55))"
```

### 地理空间近似

所有记录的位置在某种程度上都是近似的。可能需要将确切位置与已知的更广泛区域分开捕获，特别是当这种近似非常不确定时。如果地点是几个事件的确切位置，并且地点的名称可用但没有确切的地理空间坐标或完整地址，那么这种模式特别有价值。这是使用 `part_of` 构造管理的——特定地点在更广泛区域内的某个地方。


**示例：**

许多艺术品销售随时间在拍卖行发生，虽然城市可能已知，但城市内的确切地址可能未知，将整个城市的所有艺术品销售收集在一起可能会产生误导。

```crom
top = model.Place(ident="amsterdam_auction_house/1", label="Christie's AMS")
top.identified_by = model.Name(content="Christie's Amsterdam Location")
p2 = model.Place(ident="amsterdam", label="Amsterdam")
top.part_of = p2
```


## 建筑物和"不可移动"对象

很容易将地点与存在于地点的构造混淆。虽然罕见，但有建筑物在不同位置之间移动的情况。建筑物，就像绘画一样，因此被建模为在空间中有当前位置的对象。活动发生在地点，而不是对象中。由于底层数据管理，地点与建筑物的粒度可能不同。

这适用于任何其他"不可移动"对象，如大型石碑通过金字塔、废墟，或任何其他可能在特定位置"永久"的构造对象。


**示例：**

[弗兰克·劳埃德·赖特住宅](https://crystalbridges.org/frank-lloyd-wright/)最初建在新泽西州，随后被移动到它在阿肯色州的当前位置。

```crom
top = vocab.Building(ident="flw_house/1", label="Frank Lloyd Wright House")
top.identified_by = model.Name(content="Frank Lloyd Wright House")
top.current_location = model.Place(ident="crystal_bridges", label="Crystal Bridges")
```