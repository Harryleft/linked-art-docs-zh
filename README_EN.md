# Linked Art Documentation - Interactive Learning Environment

## Why This Project Exists?

Imagine you're building a digital archive system for a GLAM. You need to track: who created each artwork, when and where it was made, which collectors owned it, what exhibitions it appeared in... If this information is scattered across different spreadsheets and databases, it's hard to maintain and impossible to share with other institutions.

This is the problem Linked Art solves—it provides a **standard data model** that makes recording and sharing cultural heritage information simple. Just as libraries use ISBN standards to identify books, Linked Art lets museums, galleries, and archives describe their collections using a common "language."

## What This Project Provides

**1. Complete Chinese Translation**
- 187 translated documents covering data model, API specifications, and implementation guides
- All translations follow professional terminology standards from museum studies and art history

**2. Interactive Jupyter Notebooks**
- 257 Notebooks containing all code examples
- Every code block can be run, modified, and experimented with directly
- Automatically displays generated JSON-LD data for intuitive understanding of data structures
- **Standardized Code**: All code examples follow a consistent 5-step template with clear English comments explaining "Who/What/Why"

**3. One-Click Conversion Tool**
- Python script to convert Markdown to Notebook anytime
- Supports batch conversion for customizing learning materials

## Quick Start

### 1. Install Dependencies

Open your terminal and run:

```bash
# Install Python dependencies
pip install cromulent jupyter
```

**What these packages do**:
- `cromulent` - Python library for Linked Art, generates cultural heritage data
- `jupyter` - Interactive Notebook environment

### 2. Open the Learning Environment

Choose your preference:

**Chinese version**:
```bash
jupyter lab notebooks
```
Then open `00-README.ipynb` in your browser

**English version**:
```bash
jupyter lab notebooks-en
```

### 3. Run Your First Code Example

Open any Notebook and you'll see code like this:

```python
# Step 1: Import cromulent library
from cromulent import model, vocab

# Step 2: Configure factory settings
model.factory.auto_assign_id = False
vocab.add_attribute_assignment_check()

# Step 3: Create the main object
# Who: Unknown artist
# What: HumanMadeObject representing an artwork
# Why: To record basic information about a cultural heritage object
artwork = model.HumanMadeObject(
    ident="painting/1",
    label="Starry Night"
)

# Step 4: Create related objects and relationships
# (This is a minimal example with no additional relationships)

# Step 5: Display the generated JSON data
print(model.factory.toString(artwork, compact=False))
```

**5-Step Template Explanation**:
- **Step 1**: Import required libraries
- **Step 2**: Configure code generation environment
- **Step 3**: Create main object, documenting Who/What/Why
- **Step 4**: Create related objects and relationships with inline comments
- **Step 5**: Display generated JSON-LD

When you run it, you'll see structured JSON output:

```json
{
  "@context": "https://linked.art/ns/v1/linked-art.json",
  "id": "http://test.com/museum/HumanMadeObject/painting/1",
  "type": "HumanMadeObject",
  "_label": "Starry Night"
}
```

## Project Structure

```
linked-art-docs-zh/
├── docs/              # Original English documentation (preserved)
├── docs-zh/           # Chinese translations
├── notebooks/         # Chinese Notebooks
├── notebooks-en/      # English Notebooks
├── scripts/           # Conversion utilities
└── 术语对照表.md        # Chinese terminology standard
```

## Core Concepts at a Glance

### What is a Data Model?

A data model defines how to describe a cultural heritage object. For example, describing a painting requires:

| Property | Description | Linked Art Term |
|----------|-------------|-----------------|
| **Creation** | Who, when, where created it | Production |
| **Materials** | What it's made from | Material |
| **Dimensions** | How big it is | Dimension |
| **Provenance** | Who owned it | Provenance |
| **Exhibitions** | What it appeared in | Exhibition |

### Why Choose Linked Art?

- **Standardized**: Adopted by Getty, Smithsonian, Yale and others
- **Extensible**: Can record everything from simple to complex information
- **Interoperable**: Data can be seamlessly exchanged between systems
- **Free & Open**: Licensed under CC BY 4.0

## Learning Paths

### Beginners (Recommended)

1. **Get Started**: `notebooks-en/00-README.ipynb`
2. **Understand Core Concepts**: `notebooks-en/model/index.ipynb`
3. **Practice Creating Objects**: `notebooks-en/model/object/production.ipynb`

### Intermediate Users

1. **Dive Deeper**: `notebooks-en/model/provenance/index.ipynb`
2. **Learn the API**: `notebooks-en/api/1.0/endpoint/index.ipynb`
3. **Build Your Own Apps**: Reference `notebooks-en/cookbook/`

### Developers

1. **Read API Documentation**: `notebooks-en/api/1.0/index.ipynb`
2. **View Implementation Examples**: `notebooks-en/example/index.ipynb`
3. **Use Conversion Tools**: Reference `scripts/md_to_ipynb_converter.py`

## Common Tasks

### Create a New Artwork Record

```python
# Step 1: Import cromulent library
from cromulent import model, vocab

# Step 2: Configure factory settings
model.factory.auto_assign_id = False
vocab.add_attribute_assignment_check()

# Step 3: Create the main object (Mona Lisa painting)
# Who: Leonardo da Vinci (artist)
# What: HumanMadeObject representing the "Mona Lisa" painting
# Why: To document this world-famous artwork with its creation context
painting = model.HumanMadeObject(
    ident="mona-lisa",
    label="Mona Lisa"
)

# Step 4: Create related objects and relationships
# Production event
production = model.Production()
painting.produced_by = production

# Who created this work: Leonardo da Vinci
leonardo = model.Person(
    ident="leonardo-da-vinci",
    label="Leonardo da Vinci"
)
production.carried_out_by = leonardo

# Step 5: Display the generated JSON data
print(model.factory.toString(painting, compact=False))
```

### Convert Your Own Markdown Documents

```python
# Install required dependencies
pip install nbformat

# Convert single file
python -c "from scripts.md_to_ipynb_converter import convert_file; \
    convert_file('your-doc.md', 'output.ipynb')"

# Batch convert directory
python -c "from scripts.md_to_ipynb_converter import convert_directory; \
    convert_directory('source-dir', 'target-dir')"
```

## Terminology Guide

When reading this documentation, you'll frequently encounter these terms:

| English | Chinese | Description |
|---------|---------|-------------|
| Linked Art | Linked Art | Project name (keep original) |
| HumanMadeObject | 人工制品 | Man-made cultural heritage object |
| Provenance | 流传历史 | Transfer of ownership history |
| Actor | 行动者 | Person or group |
| Collection | 集藏 | Museum's holdings |

For complete terminology, refer to [`术语对照表.md`](术语对照表.md).

## Contributing

### Translation Improvements

If you find translation issues or have improvement suggestions:

1. Check [`术语对照表.md`](术语对照表.md) for standard translations
2. Open a GitHub Issue or Pull Request
3. Explain the reason for changes and provide references

### Conversion Tool Improvements

If you want to improve the conversion script:

1. Modify `scripts/md_to_ipynb_converter.py`
2. Ensure backward compatibility
3. Add test cases

## Original Project

- **Official Site**: https://linked.art/
- **GitHub**: https://github.com/linked-art/linked.art
- **License**: CC BY 4.0

## Acknowledgments

Thanks to the Linked Art community, especially Rob Sanderson and all contributors.

