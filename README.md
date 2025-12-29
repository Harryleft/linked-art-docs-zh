# Linked Art 中文翻译项目

## 项目概述

本项目是 Linked Art 文档的中文翻译版本，同时提供可交互的 Jupyter Notebook 学习环境。Linked Art 是一个基于 Linked Open Usable Data (LOUD) 的文化遗产描述数据模型，专注于艺术品描述，同时也包括档案和书目材料。

## 项目状态

**当前版本**: 翻译完成 + Jupyter Notebook 交互版本
**原文版本**: Linked Art 1.0
**翻译进度**: ✅ 187 个文档已翻译完成
**Notebook**: ✅ 257 个交互式 Notebook 已生成

### 完成内容

- ✅ 中文翻译文档 (docs-zh/) - 187 个文件
- ✅ 中文版 Jupyter Notebook (notebooks/) - 70 个文件
- ✅ 英文版 Jupyter Notebook (notebooks-en/) - 187 个文件
- ✅ Markdown 转 Notebook 转换脚本 (scripts/)
- ✅ 中文术语对照表
- ✅ 完整的导航索引

## 项目结构

```
linked-art-docs-zh/
├── docs/                        # 原始英文文档 (保留)
│   ├── index.md
│   ├── model/                   # 数据模型文档
│   ├── api/                     # API 文档
│   └── ...
│
├── docs-zh/                     # 中文翻译文档 ⭐ NEW
│   ├── index.md
│   ├── model/
│   ├── api/
│   └── ... (187 个翻译文件)
│
├── notebooks/                   # 中文版 Jupyter Notebook ⭐ NEW
│   ├── 00-导航索引.ipynb
│   ├── model/
│   └── api/1.0/ (70 个文件)
│
├── notebooks-en/                # 英文版 Jupyter Notebook ⭐ NEW
│   ├── 00-导航索引.ipynb
│   ├── model/
│   ├── api/
│   └── ... (187 个文件)
│
├── scripts/                     # 转换工具 ⭐ NEW
│   └── md_to_ipynb_converter.py
│
├── 术语对照表.md                # 中文术语标准
├── 翻译任务计划.md             # 翻译任务管理
├── CLAUDE.md                   # 项目配置
├── README.md                   # 本文件
└── LICENSE                     # CC BY 4.0
```

## Jupyter Notebook 使用指南

### 环境要求

```bash
# 安装 Python 库
pip install cromulent
pip install jupyter
```

### 快速开始

**中文版入口**: `notebooks/00-导航索引.ipynb`
**英文版入口**: `notebooks-en/00-导航索引.ipynb`

### Notebook 特性

| 特性 | 说明 |
|------|------|
| **交互式代码** | 所有 crom 代码示例可直接运行和修改 |
| **自动导入** | 每个代码块自动添加 `from cromulent import model, vocab` |
| **JSON 输出** | 自动显示生成的 JSON-LD 数据 |
| **独立行显示** | 代码按行独立显示，便于编辑 |
| **环境设置** | 自动配置 base_url 以获得清晰的输出 |

### 运行示例

```python
# 每个 Notebook 开头会自动设置环境
from cromulent import model, vocab

# 创建对象
obj = model.HumanMadeObject(ident="example", label="示例对象")
print(model.factory.toString(obj, compact=False))
```

## 翻译资源

### 📋 术语对照表
项目根目录下的 `术语对照表.md` 文件提供了：
- 11个类别的专业术语翻译
- 翻译原则和使用指南
- 专业术语的选择依据
- 特殊情况的处理建议

### 📚 文档内容

| 类别 | 英文版 | 中文版 | Notebook |
|------|--------|--------|----------|
| **数据模型** | 37 个文件 | ✅ 37 个 | ✅ 中英文版 |
| **API 规范** | 47 个文件 | ✅ 47 个 | ✅ 中英文版 |
| **HAL 关系** | 92 个文件 | ✅ 92 个 | ✅ 中英文版 |
| **其他文档** | 11 个文件 | ✅ 11 个 | ✅ 中英文版 |

### 🎯 学习路径建议

**初学者**:
1. 从 [数据模型概述](notebooks/model/index.ipynb) 开始
2. 学习 [基础模式](notebooks/model/base/index.ipynb)
3. 了解 [对象](notebooks/model/object/index.ipynb) 和 [行动者](notebooks/model/actor/index.ipynb)

**进阶用户**:
1. 深入 [流传历史](notebooks/model/provenance/index.ipynb)
2. 学习 [API 端点](notebooks/api/1.0/endpoint/index.ipynb)
3. 掌握 [共享结构](notebooks/api/1.0/shared/index.ipynb)

**高级用户**:
1. 研究 [词汇表](notebooks/model/vocab/index.ipynb)
2. 探索 [类分析](notebooks/model/profile/class_analysis.ipynb)
3. 理解 [JSON-LD 扩展](notebooks/api/1.0/json-ld/extensions.ipynb)

## 转换工具使用

### Markdown 转 Notebook

项目提供了完整的转换脚本 `scripts/md_to_ipynb_converter.py`：

```python
# 转换单个文件
python -c "from scripts.md_to_ipynb_converter import convert_file; \
    convert_file('docs/model/index.md', 'notebooks/model/index.ipynb')"

# 批量转换目录
python -c "from scripts.md_to_ipynb_converter import convert_directory; \
    convert_directory('docs/model', 'notebooks/model')"
```

### 转换特性

- ✅ 自动解析 YAML front matter
- ✅ 识别 crom 代码块并增强
- ✅ 添加自动导入和 JSON 输出
- ✅ 保持文档结构完整
- ✅ 支持中英文文档

## 翻译指南

### 翻译原则 (已采用)

1. **专业性优先** - 采用博物馆学界和艺术史领域的标准译法
2. **一致性原则** - 使用术语对照表确保术语统一
3. **完整性保证** - 确保不遗漏任何技术细节
4. **格式保持** - 保持原始 Markdown 文件的结构不变

### 技术要求

- **文件编码**: 所有文件使用 UTF-8 编码
- **格式保持**: 保持 Markdown 文件的原有格式
- **代码处理**: 技术代码和 API 示例保持英文
- **链接处理**: 内部链接文字翻译，但路径保持不变

### 质量控制

- 翻译完成后进行交叉检查
- 确保术语使用的一致性
- 验证所有链接和引用的正确性
- 检查中文表达的流畅性和专业性

## 原项目信息

### 关于 Linked Art

Linked Art 是一个社区驱动的项目，致力于：
- 创建基于 Linked Open Usable Data 的文化遗产描述模型
- 制定便于交互的 API 规范
- 提供软件工具和实施方案
- 推动文化遗产领域的互操作性

### 原始项目

- **官方网站**: https://linked.art/
- **GitHub仓库**: https://github.com/linked-art/linked.art
- **许可证**: CC BY 4.0
- **维护者**: Linked Art Editorial Board

### 贡献指南

#### 翻译贡献

我们欢迎中文翻译贡献：

1. **术语讨论**: 对术语翻译有建议，请在术语对照表基础上讨论
2. **翻译分工**: 可以认领特定模块进行翻译
3. **质量检查**: 协助检查已翻译内容的准确性和一致性
4. **文档改进**: 改进翻译指南和工作流程

#### 技术贡献

技术改进建议请先通过社区讨论：
- 翻译工具和流程改进
- 自动化检查脚本
- 文档构建优化

## 联系方式

### 中文翻译协调

如需参与翻译工作或有疑问，请：
- 通过 GitHub Issues 提交问题
- 参与翻译讨论
- 查阅术语对照表和工作指南

### 原项目社区

- **社区页面**: https://linked.art/community/
- **Slack频道**: linked-art.slack.com
- **编辑委员会**: https://linked.art/community/#editorial-board

## 致谢

感谢 Linked Art 原项目团队和社区：
- Rob Sanderson (robert.sanderson@yale.edu)
- Linked Art Editorial Board
- 所有为 Linked Art 项目做出贡献的社区成员

特别感谢为中文翻译工作提供支持和建议的所有人员。

---

## 许可证

本项目翻译内容遵循原项目的 CC BY 4.0 许可证。

---

*本 README 文件随项目进展持续更新*
*最后更新: 2025年1月*
*翻译完成度: 100% (187/187 文档)*
*Notebook 生成: 257 个交互式文档*