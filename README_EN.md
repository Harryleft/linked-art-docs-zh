# Linked Art Documentation — Interactive Learning Notebooks

A bilingual, executable Jupyter Notebook learning environment for the Linked Art Data Model and API.

**English Version | [中文版](README.md)**

## Quick Links

- Start here (中文): `notebooks/00-README.ipynb`

- Start here (English): `notebooks-en/00-README.ipynb`

  

## Table of Contents

- [Why Linked Art](#why-linked-art)
- [What This Repository Provides](#what-this-repository-provides)
- [Quick Start](#quick-start)
- [Repository Structure](#repository-structure)
- [Learning Paths](#learning-paths)
- [Notebook Conventions (5-Step Template)](#notebook-conventions-5-step-template)
- [Common Task: Create a Minimal Artwork Record](#common-task-create-a-minimal-artwork-record)
- [Terminology Guide](#terminology-guide)
- [License](#license)
- [Acknowledgements](#acknowledgements)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

---

## Why Linked Art

In a GLAM digital collection system, you often need to track:

- who created an artwork and under what context
- production time and place
- ownership and custody changes (provenance)
- exhibitions and related events
- relationships among objects, people, places, and organizations

If this information lives in scattered spreadsheets or siloed databases, it becomes difficult to maintain, hard to validate, and nearly impossible to share across institutions.

**Linked Art** solves this by providing a **standardized JSON-LD data model** for describing cultural heritage information in a consistent, interoperable way—so different systems can “speak the same language” when exchanging collection data.

---

## What This Repository Provides

This repository is a **fully executable Jupyter Notebook learning environment** for Linked Art.

### Key Features

1. **Learn by Doing**  
   Every notebook is runnable. Modify the code and immediately see how the JSON-LD output changes.

2. **Bilingual (Chinese + English)**  
   Parallel notebook sets support different learning preferences and teaching contexts.

3. **Consistent Code Style**  
   Examples follow a unified “5-step template” to keep structure predictable and easy to scan.

4. **Automatic JSON-LD Output**  
   Each example prints or displays generated JSON-LD to make the data model tangible.



---

## Quick Start

### 1) Prerequisites

- Python 3.9+ recommended (3.10+ preferred)
- JupyterLab (or Jupyter Notebook)

### 2) Install Dependencies

```bash
pip install cromulent jupyterlab
````

**Packages**

* `cromulent`: Python library to generate Linked Art / CIDOC-CRM aligned JSON-LD
* `jupyterlab`: interactive notebook environment

### 3) Launch Notebooks

**Chinese**

```bash
jupyter lab notebooks/
```

Open: `00-README.ipynb`

**English**

```bash
jupyter lab notebooks-en/
```

Open: `00-README.ipynb`

---

## Repository Structure

```text
.
├── notebooks/              # Chinese Jupyter Notebooks (171)
│   ├── 00-README.ipynb     # Navigation index & entry point
│   ├── index.ipynb         # Table of contents
│   ├── model/              # Linked Art Data Model
│   │   ├── actor/          # Persons, groups, and other actors
│   │   ├── object/         # Objects (production, ownership, physical properties)
│   │   ├── provenance/     # Acquisition, transfer, custody, etc.
│   │   ├── place/          # Place modeling
│   │   ├── event/          # Events
│   │   ├── exhibition/     # Exhibitions
│   │   └── ...
│   └── api/                # API documentation
│       ├── 1.0/            # Version 1.0 endpoints      
├── notebooks-en/           # English Jupyter Notebooks (170, mirrored structure)
├── scripts/                # Utility scripts (e.g., conversion tools)
└── 术语对照表.md             # Terminology reference
```

---

## Learning Paths

### Beginners (Recommended)

1. Start (English): `notebooks-en/00-README.ipynb`
2. Core overview: `notebooks-en/model/index.ipynb`
3. First hands-on modeling: `notebooks-en/model/object/production.ipynb`

### Intermediate

1. Provenance deep dive: `notebooks-en/model/provenance/index.ipynb`
2. API basics: `notebooks-en/api/1.0/index.ipynb`
3. Use endpoints to build applications: follow API endpoint notebooks



---

## Notebook Conventions (5-Step Template)

All notebooks follow a consistent 5-step structure:

1. **Import** required libraries
2. **Configure** factory / validation settings
3. **Create** the main resource (documenting Who/What/Why)
4. **Link** related resources and relationships
5. **Output** JSON-LD for inspection

This template ensures examples remain readable, comparable, and easy to extend.

---

## Common Task: Create a Minimal Artwork Record

```python
# Step 1: Import cromulent library
from cromulent import model, vocab

# Step 2: Configure factory settings
model.factory.auto_assign_id = False
vocab.add_attribute_assignment_check()

# Step 3: Create the main object
# Who: Unknown artist (minimal example)
# What: HumanMadeObject representing an artwork
# Why: Record a basic cultural heritage object in Linked Art
artwork = model.HumanMadeObject(
    ident="painting/1",
    label="Starry Night"
)

# Step 4: Create related objects and relationships (optional in minimal example)
# (no additional relationships)

# Step 5: Display the generated JSON-LD
print(model.factory.toString(artwork, compact=False))
```

Example output:

```json
{
  "@context": "https://linked.art/ns/v1/linked-art.json",
  "id": "http://test.com/museum/HumanMadeObject/painting/1",
  "type": "HumanMadeObject",
  "_label": "Starry Night"
}
```

---

## Terminology Guide

Common terms you will see frequently:

| English         | Chinese    | Notes                             |
| --------------- | ---------- | --------------------------------- |
| Linked Art      | Linked Art | Keep original name                |
| HumanMadeObject | 人工制品       | Man-made cultural heritage object |
| Provenance      | 流传历史       | Ownership/custody history         |
| Actor           | 行动者        | Person or group                   |
| Collection      | 集藏         | Museum/institution holdings       |
| Production      | 创作/生产      | Creation/production of an object  |
| Acquisition     | 获得/收藏      | Acquisition event                 |

For the full terminology list, see: `术语对照表.md`

---

## License

This repository is released under **CC BY 4.0**

---

## Acknowledgements

Thanks to the Linked Art community and contributors, especially Rob Sanderson and all project maintainers.

---

## Troubleshooting

* **`ModuleNotFoundError: cromulent`**
  Run: `pip install cromulent`

* **Jupyter command not found**
  Run: `pip install jupyterlab` and relaunch your terminal

* **Notebooks open but code won’t run**
  Ensure your Jupyter kernel is using the same Python environment where dependencies were installed.

---

## Contributing

Contributions are welcome, including:

* fixing notebook typos or improving explanations
* improving bilingual alignment or terminology consistency

Suggested workflow:

1. Fork the repo
2. Create a feature branch
3. Submit a pull request with a clear description of changes

