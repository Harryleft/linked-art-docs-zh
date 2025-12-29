# Linked Art 中文翻译项目

## 项目概述

本项目是 Linked Art 文档的中文翻译版本。Linked Art 是一个基于 Linked Open Usable Data (LOUD) 的文化遗产描述数据模型，专注于艺术品描述，同时也包括档案和书目材料。

## 项目状态

**当前版本**: 翻译准备阶段
**原文版本**: Linked Art 1.0
**翻译进度**: 准备工作完成，待开始翻译

### 已完成的工作

- ✅ 清理项目结构，删除非翻译相关文件
- ✅ 保留218个需要翻译的 Markdown 文档
- ✅ 建立完整的中文术语对照表
- ✅ 创建翻译工作指南

## 项目结构

```
linked-art-docs-zh/
├── docs/                    # 需要翻译的文档 (218个文件)
│   ├── index.md            # 项目首页
│   ├── about/              # 关于 Linked Art
│   ├── model/              # 数据模型文档 (核心)
│   ├── api/                # API 文档
│   ├── community/          # 社区信息
│   ├── cookbook/           # 实施指南
│   └── ...
├── 术语对照表.md           # 中文翻译术语标准
├── README.md              # 项目说明文件
├── LICENSE                # 许可证文件
└── .claude/              # Claude 配置文件
```

## 翻译资源

### 📋 术语对照表
项目根目录下的 `术语对照表.md` 文件提供了：
- 11个类别的专业术语翻译
- 翻译原则和使用指南
- 专业术语的选择依据
- 特殊情况的处理建议

### 🎯 翻译优先级

**第一批 (核心概念)**:
1. `docs/index.md` - 项目首页
2. `docs/about/index.md` - 项目介绍
3. `docs/model/index.md` - 数据模型概述
4. `docs/model/object/index.md` - 核心对象概念

**第二批 (主要功能)**:
5. `docs/api/1.0/index.md` - API 概述
6. `docs/model/actor/index.md` - 人物和组织
7. `docs/model/collection/index.md` - 集藏
8. `docs/community/index.md` - 社区信息

**第三批 (详细内容)**:
9. 其他 model 子文件夹
10. API 详细文档
11. 实施指南和案例

## 翻译指南

### 翻译原则

1. **专业性优先** - 采用博物馆学界和艺术史领域的标准译法
2. **一致性原则** - 使用术语对照表确保术语统一
3. **完整性保证** - 确保不遗漏任何技术细节
4. **格式保持** - 保持原始 Markdown 文件的结构不变

### 技术要求

- **文件编码**: 所有文件必须使用 UTF-8 编码
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

*本 README 文件随翻译项目进展持续更新*
*最后更新: 2025年*