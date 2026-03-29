# Ontology-Based Question Answering for Industrial Plant Models

## 1. Introduction

Modern industrial systems generate large amounts of structured data, often represented using standards such as AutomationML and stored in knowledge graphs. While these graphs are powerful, accessing their information typically requires expertise in query languages such as SPARQL.

This creates a gap between domain experts (e.g., engineers) and the data itself.

The goal of this project is to explore how Large Language Models (LLMs) can be used to enable natural language access to ontology-based plant models.

---

## 2. Problem Statement

The main challenges addressed in this work are:

- SPARQL queries are difficult to write and require technical knowledge
- Direct LLM-to-SPARQL generation is unreliable and error-prone
- Large ontologies can lead to slow query execution and timeouts
- LLMs tend to hallucinate when not properly grounded

We aim to design and evaluate different prototype architectures that:

- Improve reliability
- Reduce latency
- Maintain correctness of answers

---

## 3. State of the Art

Recent research explores combining LLMs with knowledge graphs using different approaches.

---

### 3.1 Direct SPARQL Generation

LLMs translate natural language directly into SPARQL queries.

📄 Example paper:
- https://arxiv.org/pdf/2306.08302

**Advantages:**
- Flexible
- No preprocessing required

**Limitations (from paper + experiments):**
- High error rate in query generation
- Requires validation and retry mechanisms
- Sensitive to ontology schema complexity
- Often produces syntactically correct but semantically wrong queries

👉 **Our finding:**  
We observed timeouts and unstable behavior when queries became complex (e.g., station-related queries).

---

### 3.2 Retrieval-Augmented Generation (RAG)

Relevant knowledge is retrieved and passed as context to the LLM.

📄 Example paper:
- https://arxiv.org/abs/2005.11401

**Advantages:**
- Reduces hallucination
- Easier to implement

**Limitations:**
- Retrieval over raw RDF triples is inefficient
- Context quality heavily affects answer quality

👉 **Paper insight:**  
LLMs struggle when context is unstructured or too noisy.

---

### 3.3 Hybrid Approaches (Key Paper Insight)

From:  
📄 https://arxiv.org/pdf/2306.08302

The paper proposes:

- Generating multiple query candidates
- Using validation steps before execution
- Combining symbolic querying with LLM reasoning

**Key insight:**

> Pure LLM-based querying is unstable — hybrid systems are more reliable.

👉 **Important takeaway for our work:**  
Instead of letting the LLM generate SPARQL at runtime, we move part of the logic **offline**.

---

## 4. Prototype: Query Caching (Wiki Generation Layer)

### 4.1 Motivation

From both literature and experiments:

- SPARQL queries can be slow and expensive
- LLM-generated queries are unreliable
- Many user questions are repetitive

We introduce **Query Caching as a structured knowledge layer**.

---

### 4.2 Core Idea

Instead of querying GraphDB at runtime:

> We precompute frequently useful queries and store their results as structured markdown pages.

This acts as a **cached knowledge representation**.

---

### 4.3 Architecture

GraphDB → SPARQL Queries → Cached Markdown Wiki → OpenWebUI → LLM

---

### 4.4 What “Query Caching” Means Here

In our prototype, caching is not just storing results temporarily.

It is:

- Precomputing important queries
- Persisting results as markdown
- Reusing them across all user queries

👉 This turns expensive SPARQL queries into **fast retrieval operations**.

---

### 4.5 Key Features

- Dynamic page generation (stations, components)
- Separation of:
    - discovery queries (what exists)
    - template queries (how to describe it)
- Validation pages (e.g., open ends detection)
- Structured tabular outputs for LLM consumption

---

## 5. Assumptions and Design Decisions

### 5.1 Assumptions

We assumed that:

- Users ask similar questions repeatedly
- Ontology structure changes infrequently
- Structured representations improve LLM performance
- Full LLM → SPARQL automation is not reliable

---

### 5.2 Why Query Caching Was Selected

Based on literature and experiments:

- Reduces dependency on runtime SPARQL execution
- Avoids instability of LLM-generated queries
- Improves latency significantly
- Provides structured and interpretable knowledge

👉 Compared to alternatives:

| Approach | Issue |
|--------|------|
| Direct SPARQL | Unstable |
| Raw RAG | Weak structure |
| Query Caching | Balanced and reliable |

---

## 6. Findings

### 6.1 Reliability

From paper + experiments:

- Direct SPARQL generation is unstable
- Precomputed structured knowledge significantly improves answer correctness

---

### 6.2 Performance

- Complex SPARQL queries caused timeouts
- Query caching eliminates repeated execution
- System becomes significantly faster

---

### 6.3 LLM Behavior

We observed:

- LLM performs better with:
    - structured tables
    - clearly named pages
- LLM struggles with:
    - raw RDF triples
    - unstructured graph data

👉 Matches findings from RAG literature.

---

### 6.4 Trade-offs

| Approach          | Strength            | Weakness               |
|------------------|--------------------|------------------------|
| SPARQL Generation | Flexible           | Unreliable             |
| RAG (raw)         | Simple             | Weak context           |
| Query Caching     | Fast & structured  | Requires preprocessing |

---

## 7. Limitations

- Requires preprocessing time to generate wiki
- Cache invalidation not handled dynamically
- Queries still manually designed
- Limited reasoning over graph structure

---

## 8. Future Work

- Automatic query generation from ontology schema
- Smarter caching (semantic similarity instead of exact queries)
- Hybrid system:
    - cached knowledge + live SPARQL fallback
- Integration with other prototypes

---

## 9. Conclusion

This work shows that combining LLMs with structured, cached representations of ontology data significantly improves both reliability and performance.

Instead of relying on direct SPARQL generation, we introduce a query caching layer that transforms knowledge graphs into reusable structured documents.

This results in a more robust and scalable approach to ontology-based question answering.

---