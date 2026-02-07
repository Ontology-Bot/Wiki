---
Auther: Ahmed
Date: 2026-01-22
Source: "[[2510.20345v1.pdf]]"
---
## Traditional Methods 

The survey breaks KG construction into the classic **three layers** and shows how LLMs are reshaping each:


![[02_Resources/Draws/Drawing 2026-01-22 20.43.38.excalidraw.md#^group=KFkSh0VK|100%]]
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

- We use LLMs in the three steps to help automate and enhance the process. 
---
## Step 1: Ontology Engineering

> [!info]+ Not Relevant to us
> We already have the schema anyway, No need to generate it

This is the blueprint of the graph. what types of entities exist, what relations connect them.

### Two Paradigms in the paper (Chapter 3)

#### Top-Down (LLM as Assistant): 
LLMs Help human experts build formal ontologies, humans can feed them user stories or competency questions for example. We can feed them OWL or other standard documents as well.
1. **Competency Questions (CQs) Methods**
    - **Ontogenia** uses "Metacognitive Prompting", the LLM reflects on its own output to build consistent structures
    - **CQbyCQ** turns natural language questions directly into OWL schemas
    - **Others** proposed "memoryless" and semi-automated pipelines, with human experts intervening only at critical checkpoints.
2. **Natural Language Methods**
    - Directly from unstructured or semi-structured text. No dependency on formulated questions.
    - Used LLMS like GPT-4 and frameworks like LLMs4OL
    - **LLMs4OL**, **NeOn-GPT** and **LLMs4life** derive schemas directly from text corpora

![[Pasted image 20260129112931.png]]



#### Bottom-Up (KGs for LLMs): 
Generating schemas from data to help LLMs. mostly for RAG applications. 
- This is gaining traction because of **GraphRAG**
- You don't design the schema first; you extract data and then *induce* the schema
- The process follows an **EDC Framework**: Extract -> Define -> Canonicalize
- Systems like **AdaKGC** allow the schema to evolve dynamically as new data comes in, without retraining
- Goal here is less about "perfect semantics" and more about creating **structured memory** for the LLM
![[Pasted image 20260129115118.png]]
---


## Step 2: Knowledge Extraction

> [!info] This is also not relevant to our work? 
> It's about populationg the graph with data fom a text corpora. We already have the graph.

Actually populating the graph with data. The paper splits this into **Schema-Based** and **Schema-Free** approaches.

### Schema-Based Methods

1. **Static:** The LLM is given a strict ontology and told to "fill in the blanks."
    - Pros: High consistency
    - Cons: Rigid, doesn't handle new domains well

2. **Adaptive/Dynamic:** The schema evolves with the extraction.
    - **AutoSchemaKG** uses unsupervised clustering to discover relations on the fly
    - **AdaKGC** uses "Schema-Enriched Prefix Instructions" to adapt prompts based on context

### Schema-Free Methods
What to do if not provided with a schema?

1. **Structured Generative:** No external ontology. The LLM uses Chain-of-Thought (CoT) to figure out relations.
    -  **AutoRE** (Xue et al., 2024) introduced an RHF (Relation–Head–Facts) pipeline via instruction fine-tuning, enabling the model to internalize relational regularities and improve coherence and scalability across documents.
    - **ChatIE** turns extraction into a multi-turn conversation with the bot to refine results
    - **KGGEN** (Mo et al., 2025) decomposed extraction into two sequential LLM invocations—first detecting entities, then generating relations—to reduce cognitive load and mitigate error propagation.

> [!note] We can actually use that by providing it with AML directly


1. **Open Information Extraction (OIE):** Just grabs all (Entity, Relation, Object) triples it finds.
    - Prioritizes discovery over structure
    - Messy but useful for exploration

![[Pasted image 20260129120640.png]]

---
## 3. Knowledge Fusion
Putting it all together, cleaning duplicates, resolving conflicts, merging sources.

LLMs are moving fusion from "string matching" to **semantic reasoning**.

### Schema-Level Fusion
Merging duplicate concepts (e.g., "Human" vs. "Person").
![[Pasted image 20260129123659.png]]
### Instance-Level Fusion (Entity Alignment)
![[Pasted image 20260129123800.png]]
### Hybrid Frameworks
![[Pasted image 20260129123852.png]]

---

## Where This Is Going

The survey points to three directions:

**KG-Based Reasoning for LLMs:** Using the graph to verify LLM outputs and reduce hallucinations. Makes inference explainable.

**Agentic Memory:** KGs acting as long-term, dynamic memory for AI Agents (e.g., **A-MEM**, **Zep**). Helps agents "remember" interactions over time instead of losing context.

**Multimodal KGs:** Moving beyond text to include images and video (**VaLiK**).

**Beyond RAG:** KGs can be used as a middle layer in the reasoning pipeline; enabling querying, planning and decision making.

