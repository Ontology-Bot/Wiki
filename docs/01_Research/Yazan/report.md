# Ontology-Based Question Answering for Industrial Plant Models

## 1. Introduction

Industrial plant data is often represented using ontologies such as AutomationML. These ontologies provide a structured and machine-readable representation of the system, including components, connections, and attributes.

However, while the data is technically accessible, it is not easily usable for humans. Understanding the structure of a plant model requires navigating large graphs or inspecting raw data representations, which is time-consuming and unintuitive.

The goal of this project is to explore how Large Language Models (LLMs) can make ontology-based data more accessible by enabling natural language interaction.

---

## 2. Problem Statement

The core problem is not how to query the data, but how to make ontology-based information understandable and usable.

Key challenges:

- Ontology data is complex and highly structured
- Information is distributed across many entities and relationships
- Raw representations (e.g., RDF triples) are difficult to interpret
- Users need summaries and explanations, not raw data

We aim to bridge this gap by transforming ontology data into a format that can be easily consumed by both humans and LLMs.

---

## 3. State of the Art

Recent work explores combining LLMs with structured knowledge sources.

### LLM + Knowledge Graph Interaction

Research shows that directly applying LLMs to knowledge graphs is challenging. Graph data is not naturally aligned with how LLMs process text.

From the paper:
https://arxiv.org/pdf/2306.08302

Key observations:

- LLMs struggle with raw graph structures
- Generated queries are often unreliable
- Structured intermediate representations improve results

---

### Retrieval-Based Approaches

Another common approach is to retrieve relevant information and provide it as context to the LLM.

However:

- Raw graph data is not well suited for retrieval
- Unstructured context leads to weak answers

---

### Key Insight from Literature

> LLMs perform better when knowledge is presented in structured, human-readable formats rather than raw graph data.

---

## 4. Prototype: Query Caching as Structured Knowledge Layer

### 4.1 Idea

Instead of interacting with the ontology directly at runtime, we transform it into a structured and reusable representation.

We call this **Query Caching**, where:

- Important queries are executed once
- Results are stored as markdown pages
- These pages act as a persistent knowledge layer

---

### 4.2 Architecture

GraphDB → SPARQL Queries → Markdown Wiki → OpenWebUI → LLM

---

### 4.3 What We Implemented

- Automatic generation of overview pages (stations, components)
- Dynamic generation of:
  - station-specific pages
  - component-type pages
- Validation pages (e.g., open ends in the plant)

The result is a structured "plant wiki" that represents the ontology in a human-readable format.

---

### 4.4 Why This Works

This approach changes how the ontology is consumed:

- Instead of navigating a graph → users read structured pages
- Instead of raw triples → LLM sees tables and summaries
- Instead of runtime complexity → data is precomputed

---

## 5. Findings

### 5.1 Ontology Representation Matters

We observed that:

- Raw ontology data is difficult to use directly
- Converting it into structured documents makes it significantly easier to interpret

---

### 5.2 LLM Performance Improves with Structure

- LLM answers were more accurate when using markdown tables
- Clear page organization improved retrieval quality
- Hallucination was reduced when context was structured

---

### 5.3 Preprocessing is Valuable

Although query caching requires preprocessing:

- It reduces complexity during interaction
- It enables faster and more stable responses

---

## 6. Limitations

- The system depends on predefined queries
- It does not fully capture all relationships in the ontology
- Updates to the ontology require regeneration of the wiki

---

## 7. Future Work

- Automatically generate queries from ontology structure
- Improve coverage of relationships between entities
- Combine cached knowledge with live querying
- Integrate with other approaches (e.g., direct graph reasoning)

---

## 8. Conclusion

This project shows that the main challenge is not accessing ontology data, but making it usable.

By transforming the ontology into a structured knowledge layer, we enable both humans and LLMs to interact with complex plant data more effectively.

Query caching, in this context, is not just a performance optimization, but a way to reshape how ontology data is consumed.

---