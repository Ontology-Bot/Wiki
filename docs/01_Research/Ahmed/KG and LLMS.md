---
Auther: Ahmed
Date: 2026-01-22
Source: "[[2510.20345v1.pdf]]"
---

## Traditional Methods 

The survey breaks KG construction into the classic **three layers** and shows how LLMs are reshaping each:

![[Drawing 2026-01-22 19.09.32.excalidraw]]

Suffered From:
- Scalability issues and data sparsity
- Expert dependence
- Fragmented pipelines
- Limited adaptability to new domains
- Error propagation across stages
---

## So with LLMs?

![[Pasted image 20260122194155.png]]
We're moving from rule-based, statistical, human-heavy pipelines to something generative and language-driven. 

---
## 1. Ontology Engineering

This is the blueprint of the graph. what types of entities exist, what relations connect them.

### Two Paradigms Emerging

**Top-Down (LLM as Assistant):** Helping humans build formal ontologies.
- Instead of manually coding OWL files, you feed the LLM "User Stories" or **Competency Questions (CQs)**, and it generates the ontology
- **Ontogenia** uses "Metacognitive Prompting", the LLM reflects on its own output to build consistent structures
- **CQbyCQ** turns natural language questions directly into OWL schemas
- **LLMs4OL** and **NeOn-GPT** derive schemas directly from text corpora

**Bottom-Up (KGs for LLMs):** Generating schemas from data to help LLMs. mostly for RAG applications.
- This is gaining traction because of **GraphRAG**
- You don't design the schema first; you extract data and then *induce* the schema
- The process follows an **EDC Framework**: Extract → Define → Canonicalize
- Systems like **AdaKGC** allow the schema to evolve dynamically as new data comes in, without retraining
- Goal here is less about "perfect semantics" and more about creating **structured memory** for the LLM

---
## 2. Knowledge Extraction

Actually populating the graph with data. The paper splits this into **Schema-Based** and **Schema-Free** approaches.
### Schema-Based Methods

**Static:** The LLM is given a strict ontology and told to "fill in the blanks."
- Pros: High consistency
- Cons: Rigid, doesn't handle new domains well

**Adaptive/Dynamic:** The schema evolves with the extraction.
- **AutoSchemaKG** uses unsupervised clustering to discover relations on the fly
- **AdaKGC** uses "Schema-Enriched Prefix Instructions" to adapt prompts based on context

### Schema-Free Methods

**Structured Generative:** No external ontology. The LLM uses Chain-of-Thought (CoT) to figure out relations. -> Give AML directly???
- **ChatIE** turns extraction into a multi-turn conversation with the bot to refine results

**Open Information Extraction (OIE):** Just grabs all (Entity, Relation, Object) triples it finds.
- Prioritizes discovery over structure
- Messy but useful for exploration

---
## 3. Knowledge Fusion

Putting it all together, cleaning duplicates, resolving conflicts, merging sources.

LLMs are moving fusion from "string matching" to **semantic reasoning**.
### Schema-Level Fusion
Merging duplicate concepts (e.g., "Human" vs. "Person").
- Newer methods (like in EDC) generate natural language definitions for concepts and compare their **vector embeddings**

### Instance-Level Fusion (Entity Alignment)
- **LLM-Align** and **EntGPT** treat alignment as a reasoning task (multi-step prompting) rather than just comparing similarity scores

### Hybrid Frameworks
Doing extraction and fusion simultaneously.
- **Graphusion** uses a single generative cycle to extract, align, and infer all at once

---

## Where This Is Going

The survey points to three directions:

**KG-Based Reasoning for LLMs:** Using the graph to verify LLM outputs and reduce hallucinations. Makes inference explainable.

**Agentic Memory:** KGs acting as long-term, dynamic memory for AI Agents (e.g., **A-MEM**, **Zep**). Helps agents "remember" interactions over time instead of losing context.

**Multimodal KGs:** Moving beyond text to include images and video (**VaLiK**).

