# Linked Art 中文文档 - 可交互式学习环境

## 为什么需要这个项目？

想象一下，你正在为GLAM机构建立数字化档案系统。你需要记录：每件艺术品是谁创作的、何时何地完成、经历过哪些收藏者的流转、参加过哪些展览...如果把这些信息分散在不同的表格和数据库中，不仅难以维护，更无法与其他机构共享数据。

这就是 Linked Art 要解决的问题——它提供了一套**标准的数据模型**，让文化遗产信息的记录和共享变得简单。就像图书馆使用 ISBN 标准来标识书籍一样，Linked Art 让博物馆、美术馆、档案馆可以用同一种"语言"来描述他们的收藏。

## 这个项目提供了什么？

这是一个**纯 Jupyter Notebook 交互式学习环境**，包含 341 个可执行笔记本（171 中文 + 170 英文），专注于 Linked Art 数据模型和 API 规范。

**核心特点**：

1. **即学即用** - 每个 Notebook 都是可执行的，代码可以实时运行、修改、实验
2. **双语言支持** - 提供中文和英文两个版本，满足不同学习需求
3. **标准化代码** - 所有代码示例遵循统一的 5 步结构模板，清晰易懂
4. **自动输出** - 每个代码块自动显示生成的 JSON-LD，直观理解数据结构

**覆盖内容**：
- **数据模型** (Model): 17 个主题，包括对象、行动者、流传历史、展览等
- **API 规范** (API): 完整的 RESTful API 文档和关系属性定义

## 快速开始

### 1. 安装依赖

打开终端，执行以下命令：

```bash
pip install cromulent jupyter
```

**安装说明**：
- `cromulent` - Linked Art 的 Python 库，用于生成文化遗产数据
- `jupyter` - 交互式 Notebook 环境

### 2. 打开学习环境

**中文版**：
```bash
jupyter lab notebooks
```
然后在浏览器中打开 `00-README.ipynb`

**英文版**：
```bash
jupyter lab notebooks-en
```

### 3. 运行第一个代码示例

打开任意 Notebook，你会看到类似这样的代码：

```python
# Step 1: 导入 cromulent 库
from cromulent import model, vocab

# Step 2: 配置工厂设置
model.factory.auto_assign_id = False
vocab.add_attribute_assignment_check()

# Step 3: 创建主对象
# Who: 未知艺术家
# What: 人工制品对象
# Why: 记录一件艺术品的基本信息
artwork = model.HumanMadeObject(
    ident="painting/1",
    label="星空"
)

# Step 4: 创建相关对象和关系
# (本示例是最简单的对象，无额外关系)

# Step 5: 显示生成的 JSON 数据
print(model.factory.toString(artwork, compact=False))
```

**5 步模板说明**：
- **Step 1**: 导入必要的库
- **Step 2**: 配置代码生成环境
- **Step 3**: 创建主对象，说明涉及的人/物/目的
- **Step 4**: 创建相关对象和关系，包含行内注释
- **Step 5**: 显示生成的 JSON-LD

运行后，你会看到结构化的 JSON 输出：

```json
{
  "@context": "https://linked.art/ns/v1/linked-art.json",
  "id": "http://test.com/museum/HumanMadeObject/painting/1",
  "type": "HumanMadeObject",
  "_label": "星空"
}
```

## 项目结构

```
linked-art-docs-zh/
├── notebooks/         # 中文版 Jupyter Notebooks (171 个)
│   ├── 00-README.ipynb    # 导航索引 & 入口
│   ├── index.ipynb        # 总目录
│   ├── model/             # 数据模型文档
│   │   ├── actor/        # 行动者（人、群体）
│   │   ├── object/       # 对象（创作、所有权、物理属性）
│   │   ├── provenance/   # 流传历史（获得、转移、监护）
│   │   ├── place/        # 地点
│   │   ├── event/        # 事件
│   │   ├── exhibition/   # 展览
│   │   └── ...
│   └── api/               # API 规范
│       ├── 1.0/          # 版本 1.0 端点文档
│       └── rels/         # 关系属性定义
├── notebooks-en/      # 英文版 Jupyter Notebooks (170 个)
│   └── (同上结构)
├── scripts/           # 转换工具
└── 术语对照表.md       # 专业术语标准参考
```

## 核心概念速览

### 数据模型是什么？

数据模型定义了如何描述一个文化遗产对象。例如，描述一幅画作需要：

| 属性 | 说明 | Linked Art 术语 |
|------|------|-----------------|
| **创作** | 谁在何时何地创作了它 | Production |
| **材质** | 用什么材料制成 | Material |
| **尺寸** | 有多大 | Dimension |
| **流传** | 曾被谁收藏 | Provenance |
| **展览** | 参加过哪些展览 | Exhibition |

### 为什么选择 Linked Art？

- **标准化**：被 Getty、Smithsonian、Yale 等机构采用
- **可扩展**：可以记录从简单到复杂的各种信息
- **互操作**：数据可以在不同系统间无缝交换
- **免费开源**：遵循 CC BY 4.0 许可证

## 学习路径建议

### 初学者（推荐）

1. **从入口开始**：`notebooks/00-README.ipynb`
2. **理解核心概念**：`notebooks/model/index.ipynb`
3. **实践创建对象**：`notebooks/model/object/production.ipynb`

### 进阶用户

1. **深入数据模型**：`notebooks/model/provenance/index.ipynb`
2. **学习 API 使用**：`notebooks/api/1.0/index.ipynb`
3. **构建自己的应用**：参考 API 端点文档

### 开发者

1. **阅读 API 文档**：`notebooks-en/api/1.0/index.ipynb`
2. **查看关系属性**：`notebooks-en/api/rels/1/index.ipynb`
3. **使用转换工具**：参考 `scripts/md_to_ipynb_converter.py`

## 常见任务

### 创建一个新的艺术品记录

```python
# Step 1: 导入 cromulent 库
from cromulent import model, vocab

# Step 2: 配置工厂设置
model.factory.auto_assign_id = False
vocab.add_attribute_assignment_check()

# Step 3: 创建主对象（蒙娜丽莎画作）
# Who: 列奥纳多·达·芬奇（艺术家）
# What: 人工制品对象 - "蒙娜丽莎"画作
# Why: 记录这件世界著名艺术品的基本信息和创作背景
painting = model.HumanMadeObject(
    ident="mona-lisa",
    label="蒙娜丽莎"
)

# Step 4: 创建相关对象和关系
# 创作事件
production = model.Production()
painting.produced_by = production

# 谁创作了这件作品：达·芬奇
leonardo = model.Person(
    ident="leonardo-da-vinci",
    label="列奥纳多·达·芬奇"
)
production.carried_out_by = leonardo

# Step 5: 显示生成的 JSON 数据
print(model.factory.toString(painting, compact=False))
```

## 术语对照（重要）

在阅读本文档时，以下术语会频繁出现：

| 英文 | 中文 | 说明 |
|------|------|------|
| Linked Art | Linked Art | 保持原文，项目名称 |
| HumanMadeObject | 人工制品 | 人造的文化遗产对象 |
| Provenance | 流传历史 | 所有权的转移历史 |
| Actor | 行动者 | 人或组织 |
| Collection | 集藏 | 博物馆的收藏 |
| Production | 创作/生产 | 艺术品的创造过程 |
| Acquisition | 获得/收藏 | 所有权的获取 |

完整术语表请参考 [`术语对照表.md`](术语对照表.md)。

## 原项目信息

- **官方网站**: https://linked.art/
- **GitHub**: https://github.com/linked-art/linked.art
- **许可证**: CC BY 4.0

## 致谢

感谢 Linked Art 社区，特别是 Rob Sanderson 和所有贡献者。

---

**项目统计**：
- 中文 Notebook: 171 个
- 英文 Notebook: 170 个
- 覆盖主题: 数据模型 (17) + API (2)
