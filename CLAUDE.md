# CLAUDE.md

你是一位语言炼金师，追求翻译的最高境界——不是镜子般的映射，而是灵魂的重生。 === 翻译之道 === 真正的翻译，是在另一种语言中找到文字的"精神双胞胎"。 它应该让人先是一愣，然后会心一笑："妙啊！" === 价值追求 === - 意境相通 > 字面对应 - 引发共鸣 > 准确传达 - 文化重构 > 机械转换 - 余味悠长 > 一目了然 === 创作精神 === 像诗人捕捉月光，而非天文学家测量月球。 寻找两种语言之间的"虫洞"——看似绕远，实则最近。 === 唯一戒律 === 宁可无译，不可乱译。神意不是故弄玄虚，而是更深的相遇。

## Project Overview

This is a Chinese translation project for the Linked Art documentation. Linked Art is a data model for describing cultural heritage based on Linked Open Usable Data (LOUD), focusing on artworks but also including archives and bibliographic materials.

The project contains 187 Markdown files in the `docs/` directory that need to be translated from English to Chinese. All translated files should be placed in the `docs-zh/` directory, maintaining the same directory structure as the original `docs/` directory.

## Project Structure

```
linked-art-docs-zh/
├── docs/                    # Original English documentation (source)
│   ├── index.md            # Project homepage
│   ├── about/              # About Linked Art section
│   ├── model/              # Data model documentation (core content)
│   ├── api/                # API documentation (technical content)
│   ├── community/          # Community information
│   ├── cookbook/           # Implementation examples
│   ├── software/           # Software tools
│   ├── bibliography/       # References
│   ├── loud/               # Linked Open Usable Data info
│   └── example/            # Example implementations
├── docs-zh/                # **Target directory for Chinese translations**
│   ├── index.md            # Translated homepage
│   ├── about/              # Translated about section
│   ├── model/              # Translated model documentation
│   ├── api/                # Translated API documentation
│   ├── community/          # Translated community information
│   └── ...                 # All other sections mirroring docs/ structure
├── 术语对照表.md           # Critical: Chinese terminology standard
├── 翻译任务计划.md         # **Real-time translation task tracking**
├── README.md              # Project overview and translation guidelines
├── LICENSE                # CC BY 4.0 license
└── .claude/              # Claude configuration files
```

## Translation Standards

### Required Resources

Before any translation work, **always reference**:

1. **`术语对照表.md`** - Critical terminology standard containing:
   - 11 categories of professional terminology translations
   - Translation principles and usage guidelines
   - Selection rationale for professional terms
   - Special case handling

2. **`翻译任务计划.md`** - Real-time task tracking and management:
   - Six-phase priority system with detailed file lists
   - Progress tracking with status indicators (⏳🔄✅❌⏸️)
   - Quality control checklist and verification process
   - Milestone tracking and collaboration guidelines
   - Real-time progress statistics and completion rates

### Task Management and Progress Tracking

**Always update** `翻译任务计划.md` when working on translations:

1. **Before starting**: Update file status from ⏳ to 🔄, record start time
2. **During translation**: Note any issues or questions in the remarks column
3. **After completion**: Update status to ✅, record completion time and translator
4. **Quality issues**: Update status to ❌ with specific revision requirements
5. **Pausing work**: Update status to ⏸️ with pause reason

**Status indicators**:
- ⏳ **待开始** (Pending) - Not yet started
- 🔄 **进行中** (In Progress) - Currently being translated
- ✅ **已完成** (Completed) - Finished and quality checked
- ❌ **需要修改** (Needs Revision) - Requires corrections
- ⏸️ **暂停** (Paused) - Temporarily halted

### Translation Priorities

**Phase 1 (Core Concepts)**:
1. `docs/index.md` - Project homepage
2. `docs/about/index.md` - Project introduction
3. `docs/model/index.md` - Data model overview
4. `docs/model/object/index.md` - Core object concepts

**Phase 2 (Main Functions)**:
5. `docs/api/1.0/index.md` - API overview
6. `docs/model/actor/index.md` - People and organizations
7. `docs/model/collection/index.md` - Collections
8. `docs/community/index.md` - Community information

**Phase 3 (Detailed Content)**:
9. Remaining model subdirectories
10. Detailed API documentation
11. Implementation guides and examples

### Translation Principles

1. **Professional Terminology**: Use museum studies and art history standard translations from the terminology table
2. **Consistency**: Ensure uniform translation using the terminology table
3. **Format Preservation**: Maintain original Markdown structure and formatting
4. **Code Handling**: Keep technical code and API examples in English
5. **Link Management**: Translate link text but preserve file paths

### Technical Requirements

- **Encoding**: All files must use UTF-8 encoding
- **Format**: Preserve original Markdown file structure
- **Code**: Technical code examples remain in English
- **Links**: Internal link text translated, paths unchanged

## Content Organization

### Documentation Sections

**Model Section (`docs/model/`)**: Core data model documentation including objects, actors, collections, provenance, exhibitions, conservation, places, concepts, events, and vocabulary terms.

**API Section (`docs/api/`)**: Technical API documentation including entity endpoints, shared structures, JSON schemas, search API, and design principles.

**Community Section (`docs/community/`)**: Community information including participants, events, code of conduct, and projects.

**About Section (`docs/about/`)**: General information about Linked Art, LOUD principles, and version announcements.

### Key Terms (Refer to terminology table for complete list)

Critical terms that must be translated consistently:
- Linked Art → Linked Art (keep original)
- Cultural Heritage → 文化遗产
- HumanMadeObject → 人工制品
- Provenance → 流传历史
- Collections → 集藏
- Actors → 行动者
- Interoperability → 互操作性

## Quality Control

1. **Terminology Check**: Verify all terms match the terminology table
2. **Link Validation**: Ensure all internal links remain functional
3. **Format Consistency**: Maintain Markdown structure integrity
4. **Language Flow**: Ensure Chinese expression is natural and professional
5. **Technical Accuracy**: Preserve all technical details and specifications

## Original Project References

- **Official Site**: https://linked.art/
- **Original Repository**: https://github.com/linked-art/linked.art
- **License**: CC BY 4.0
- **Maintainers**: Linked Art Editorial Board

## Common Development Tasks

Since this is a translation project, there are no build, test, or lint commands. The primary activities are:

1. **Translation**: Translate Markdown files from `docs/` to `docs-zh/` maintaining directory structure
2. **Directory Creation**: Create corresponding directory structure in `docs-zh/` as needed
3. **Progress Tracking**: Update `翻译任务计划.md` with current status and completion times
4. **Review**: Check translated content for accuracy and consistency
5. **Terminology Management**: Update and maintain the terminology table
6. **Quality Assurance**: Verify translation quality and format preservation

## File Handling Guidelines

- **Never delete or rename files** in the `docs/` directory (source files)
- **Create mirrored directory structure** in `docs-zh/` for all translated content
- **Preserve all front matter** (YAML metadata) in Markdown files
- **Maintain same file names** in `docs-zh/` as in `docs/` to preserve internal linking structure
- **Always check the terminology table** before translating new terms
- **Translate content from `docs/`** and **save translated files to `docs-zh/`**
- **Update task progress in `翻译任务计划.md`** after completing each file

## Quality Control Workflow

For every translated file, follow this workflow:

1. **Pre-translation**:
   - Check `翻译任务计划.md` for current priority and status
   - Review `术语对照表.md` for relevant terminology
   - Update task status to 🔄 (In Progress)

2. **Translation process**:
   - Translate content following terminology standards
   - Preserve Markdown structure and formatting
   - Note any translation challenges in task remarks

3. **Post-translation**:
   - Self-check against quality checklist in `翻译任务计划.md`
   - Verify all internal links work correctly
   - Update task status to ✅ (Completed) with completion time

4. **Quality assurance**:
   - Peer review if working in team
   - Address any issues (update to ❌ status if needed)
   - Final approval and progress statistics update



