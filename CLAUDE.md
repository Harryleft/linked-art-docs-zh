# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Jupyter Notebook-based interactive learning environment** for Linked Art documentation. The project contains executable notebooks covering the Linked Art Data Model and API specifications, available in both Chinese and English.

**Project Status**: Complete - Interactive Notebooks Only
- Chinese Notebooks: `notebooks/` (171 files)
- English Notebooks: `notebooks-en/` (170 files)
- Coverage: Data Model + API documentation

## Project Structure

```
linked-art-docs-zh/
├── notebooks/         # Chinese Jupyter Notebooks
│   ├── 00-README.ipynb    # Navigation & entry point
│   ├── model/             # Data Model documentation
│   │   ├── actor/        # Persons, Groups
│   │   ├── object/       # Physical objects, production, ownership
│   │   ├── provenance/   # Acquisition, movement, custody
│   │   ├── place/        # Locations
│   │   └── ...
│   └── api/               # API specification
│       ├── 1.0/          # Version 1.0 endpoints
│       └── rels/         # Relationship properties
├── notebooks-en/      # English Jupyter Notebooks (same structure)
├── scripts/           # Conversion utilities
└── 术语对照表.md      # Chinese terminology standard (reference)
```

## Jupyter Notebook Format

### Code Cell Standard (5-Step Template)

All executable code blocks follow a consistent 5-step structure:

```python
# Step 1: Import cromulent library
from cromulent import model, vocab

# Step 2: Configure factory settings
model.factory.auto_assign_id = False
vocab.add_attribute_assignment_check()

# Step 3: Create the main object
# Who: [Actor involved]
# What: [Entity being created]
# Why: [Purpose of this code]
main_object = model.HumanMadeObject(ident="example", label="Example")

# Step 4: Create related objects and relationships
# [Inline comments explaining each relationship]
related = model.Person(ident="artist", label="Artist")
production = model.Production()
production.carried_out_by = related
main_object.produced_by = production

# Step 5: Display the generated JSON data
print(model.factory.toString(main_object, compact=False))
```

### Critical Implementation Details

- Every executable cell includes `from cromulent import model, vocab`
- JSON output uses `model.factory.toString()` with `compact=False` for readability
- Comments use **English** for consistency (even in Chinese notebooks)
- The `# Who/What/Why` format provides context for each code example

## Running Notebooks

### Environment Setup

```bash
pip install cromulent jupyter
```

### Entry Points

- **Chinese**: `notebooks/00-README.ipynb`
- **English**: `notebooks-en/00-README.ipynb`

### Execution

```bash
# Chinese version
jupyter lab notebooks

# English version
jupyter lab notebooks-en
```

## Translation Principles

When updating notebook content, reference [`术语对照表.md`](术语对照表.md):

| English | Chinese |
|---------|---------|
| Linked Art | Linked Art (keep original) |
| Cultural Heritage | 文化遗产 |
| HumanMadeObject | 人工制品 |
| Provenance | 流传历史 |
| Collections | 集藏 |
| Actors | 行动者 |
| Production | 创作/生产 |

**Core Translation Philosophy**:
1. **意境相通 > 字面对应** - Capture the spirit, not just words
2. **引发共鸣 > 准确传达** - Evoke resonance in target audience
3. **文化重构 > 机械转换** - Reconstruct culturally
4. **余味悠长 > 一目了然** - Leave room for interpretation

## Conversion Tool

**Location**: `scripts/md_to_ipynb_converter.py`

**Key Functions**:
- `convert_file(md_path, ipynb_path)` - Convert single Markdown to Notebook
- `convert_directory(src_dir, dst_dir)` - Batch convert directory

**Features**:
- Parses YAML front matter (`title`, `up_href`, `up_label`)
- Auto-adds cromulent imports to code blocks
- Detects main variables for JSON output
- Creates proper Jupyter structure using nbformat.v4

## Original Project References

- **Official Site**: https://linked.art/
- **Original Repository**: https://github.com/linked-art/linked.art
- **License**: CC BY 4.0
- **Maintainers**: Linked Art Editorial Board
