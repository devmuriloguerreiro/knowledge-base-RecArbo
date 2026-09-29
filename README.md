# RecArbo Recommendation Knowledge Base

This repository contains the recommendation knowledge base used by **RecArbo**, a contextual recommender system designed to support urban arboviruses prevention (Dengue, Zika, Chikungunya) through semantic retrieval.

The knowledge base was developed as part of the PhD research of Murilo Guerreiro Arouca at the Federal University of Bahia (UFBA).

---

# Overview

Unlike traditional rule-based recommender systems, RecArbo retrieves preventive recommendations according to the semantic similarity between an observed environmental context and a previously modeled epidemiological scenario.

Each recommendation represents a distinct environmental situation and contains both:

- information presented to the end user;
- semantic information used internally by the recommendation engine.

The knowledge base is employed exclusively for **semantic retrieval** and **contextual re-ranking**.

It is **not** used to train Machine Learning models.

---

# Repository Structure

```
knowledge-base/
│
├── recommendations.csv
├── prompt.md
└── README.md
```

---

# Knowledge Base

The dataset contains **120 preventive recommendations** distributed across three epidemiological risk levels:

| Risk Level | Records |
|------------|---------|
| Low | 40 |
| Medium | 40 |
| High | 40 |

Each recommendation contains the following attributes:

| Attribute | Description |
|-----------|-------------|
| id | Unique identifier |
| risk_level | Low, Medium or High |
| title | Short recommendation title |
| message | Preventive message presented to users |
| semantic_context | Environmental scenario used for semantic retrieval |
| tags | Contextual keywords |
| target_categories | Environmental categories |
| source | Public health institution used as technical reference |
| source_url | Official source URL |

During system initialization, additional attributes are automatically generated:

- search_text
- embedding

These attributes are not stored in the original dataset and are generated during the indexing process.

---

# Knowledge Base Construction

The knowledge base was generated with the assistance of a Large Language Model (LLM).

Model used:

> **Google Gemini 3.6 Flash**

The LLM was employed **only during the knowledge engineering phase** to assist in generating diverse epidemiological scenarios and preventive recommendations.

The LLM **does not participate in the production system**.

After generation, the recommendations were manually reviewed before being incorporated into the knowledge base.

---

# Prompt

The complete prompt used to generate the recommendation dataset is available in:

```
prompt.md
```

The prompt defines:

- dataset structure;
- risk level distribution;
- environmental categories;
- diversity requirements;
- semantic_context specification;
- output format.

---

# Dataset Design Principles

The following principles guided the construction of the knowledge base:

- semantic diversity;
- epidemiological plausibility;
- balanced risk distribution;
- contextual richness;
- environmental variability;
- recommendation diversity;
- compatibility with embedding-based retrieval.

The most important field is:

```
semantic_context
```

Instead of describing the recommendation itself, this attribute describes the environmental and epidemiological conditions under which the recommendation is appropriate.

This textual description is transformed into an embedding vector during the indexing stage.

---

# Usage in RecArbo

The recommendation pipeline is composed of the following stages:

1. Risk calculation
2. Risk discretization
3. Knowledge base filtering
4. Context representation
5. Semantic retrieval
6. Contextual re-ranking
7. Recommendation selection

Only the indexed knowledge base is used during runtime.

The LLM is not queried during recommendation generation.
