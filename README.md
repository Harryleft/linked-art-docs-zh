# Linked Art 中文文档 — 可交互式学习笔记本

面向 Linked Art 数据模型和 API 的双语言可执行 Jupyter Notebook 学习环境。

## 快速链接

- 从这里开始（中文）: `notebooks/00-README.ipynb`

- 从这里开始（英文）: `notebooks-en/00-README.ipynb`



## 目录

- [为什么选择 Linked Art](#为什么选择-linked-art)
- [本项目提供了什么](#本项目提供了什么)
- [快速开始](#快速开始)
- [仓库结构](#仓库结构)
- [学习路径](#学习路径)
- [Notebook 规范（5 步模板）](#notebook-规范5-步模板)
- [常见任务：创建最简艺术品记录](#常见任务创建最简艺术品记录)
- [术语指南](#术语指南)
- [许可证](#许可证)
- [致谢](#致谢)
- [故障排查](#故障排查)
- [贡献](#贡献)

---

## 为什么选择 Linked Art

在 GLAM 机构的数字化馆藏系统中，你通常需要记录：

- 谁创作了艺术品以及相关背景
- 创作时间和地点
- 所有权和监护权的变更（流传历史）
- 展览和相关事件
- 对象、人物、地点和组织之间的关系

如果这些信息分散在不同的表格或孤立数据库中，就会变得难以维护、难以验证，而且几乎无法在机构之间共享。

**Linked Art** 通过提供一套**标准化的 JSON-LD 数据模型**来解决这个问题，用一致、互操作的方式描述文化遗产信息——让不同系统在交换馆藏数据时能够"使用同一种语言"。

---

## 本项目提供了什么

本仓库是 Linked Art 的**完全可执行的 Jupyter Notebook 学习环境**。

### 核心特点

1. **即学即用**
   每个 notebook 都可运行。修改代码并立即查看 JSON-LD 输出的变化。

2. **双语言（中文 + 英文）**
   并行的 notebook 集支持不同的学习偏好和教学场景。

3. **一致的代码风格**
   示例遵循统一的"5 步模板"，保持结构可预测且易于浏览。

4. **自动 JSON-LD 输出**
   每个示例都会打印或显示生成的 JSON-LD，使数据模型具体可见。



---

## 快速开始

### 1) 前置要求

- Python 3.9+ 推荐（3.10+ 更佳）
- JupyterLab（或 Jupyter Notebook）

### 2) 安装依赖

```bash
pip install cromulent jupyterlab
````

**依赖包说明**

* `cromulent`: 用于生成 Linked Art / CIDOC-CRM 兼容 JSON-LD 的 Python 库
* `jupyterlab`: 交互式 notebook 环境

### 3) 启动 Notebooks

**中文版**

```bash
jupyter lab notebooks/
```

打开：`00-README.ipynb`

**英文版**

```bash
jupyter lab notebooks-en/
```

打开：`00-README.ipynb`

---

## 仓库结构

```text
.
├── notebooks/              # 中文 Jupyter Notebooks (171 个)
│   ├── 00-README.ipynb     # 导航索引 & 入口
│   ├── index.ipynb         # 目录
│   ├── model/              # Linked Art 数据模型
│   │   ├── actor/          # 人、群体和其他行动者
│   │   ├── object/         # 对象（创作、所有权、物理属性）
│   │   ├── provenance/     # 获得、转移、监护等
│   │   ├── place/          # 地点建模
│   │   ├── event/          # 事件
│   │   ├── exhibition/     # 展览
│   │   └── ...
│   └── api/                # API 文档
│       ├── 1.0/            # 版本 1.0 端点
├── notebooks-en/           # 英文 Jupyter Notebooks (170 个，镜像结构)
├── scripts/                # 实用工具脚本（如转换工具）
└── 术语对照表.md             # 术语参考
```

---

## 学习路径

### 初学者（推荐）

1. 开始（中文）: `notebooks/00-README.ipynb`
2. 核心概览: `notebooks/model/index.ipynb`
3. 第一次动手建模: `notebooks/model/object/production.ipynb`

### 进阶用户

1. 流传历史深入: `notebooks/model/provenance/index.ipynb`
2. API 基础: `notebooks/api/1.0/index.ipynb`
3. 使用端点构建应用: 跟随 API 端点 notebooks 学习



---

## Notebook 规范（5 步模板）

所有 notebooks 都遵循一致的 5 步结构：

1. **导入** 所需库
2. **配置** 工厂/验证设置
3. **创建** 主资源（记录谁/什么/为什么）
4. **关联** 相关资源和关系
5. **输出** JSON-LD 以供检查

这个模板确保示例保持可读、可比较且易于扩展。

---

## 常见任务：创建最简艺术品记录

```python
# Step 1: 导入 cromulent 库
from cromulent import model, vocab

# Step 2: 配置工厂设置
model.factory.auto_assign_id = False
vocab.add_attribute_assignment_check()

# Step 3: 创建主对象
# Who: 未知艺术家（最简示例）
# What: 代表艺术品的人工制品对象
# Why: 在 Linked Art 中记录基本的文化遗产对象
artwork = model.HumanMadeObject(
    ident="painting/1",
    label="星空"
)

# Step 4: 创建相关对象和关系（最简示例中可选）
# （无额外关系）

# Step 5: 显示生成的 JSON-LD
print(model.factory.toString(artwork, compact=False))
```

示例输出：

```json
{
  "@context": "https://linked.art/ns/v1/linked-art.json",
  "id": "http://test.com/museum/HumanMadeObject/painting/1",
  "type": "HumanMadeObject",
  "_label": "星空"
}
```

---

## 术语指南

你会经常看到的一些常见术语：

| 英文            | 中文     | 说明                |
| --------------- | -------- | ------------------- |
| Linked Art      | Linked Art | 保持原名            |
| HumanMadeObject | 人工制品    | 人造的文化遗产对象     |
| Provenance      | 流传历史    | 所有权/监护历史       |
| Actor           | 行动者     | 人或群体            |
| Collection      | 集藏       | 博物馆/机构馆藏       |
| Production      | 创作/生产   | 对象的创造/生产       |
| Acquisition     | 获得/收藏   | 获得事件            |

完整术语列表请查看：`术语对照表.md`

---

## 许可证

本仓库采用 **CC BY 4.0** 许可证发布

---

## 致谢

感谢 Linked Art 社区和贡献者，特别是 Rob Sanderson 和所有项目维护者。

---

## 故障排查

* **`ModuleNotFoundError: cromulent`**
  运行：`pip install cromulent`

* **找不到 Jupyter 命令**
  运行：`pip install jupyterlab` 并重新启动终端

* **Notebook 打开但代码无法运行**
  确保你的 Jupyter 内核使用的是安装了依赖的同一 Python 环境

---

## 贡献

欢迎贡献，包括：

* 修复 notebook 中的拼写错误或改进说明
* 改进双语言对齐或术语一致性

建议的工作流程：

1. Fork 本仓库
2. 创建功能分支
3. 提交 pull request 并清晰说明更改内容
