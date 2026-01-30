# E2 — RAG-based SPARQL Generation over Knowledge Graphs

**Paper:**  
LLM-based SPARQL Query Generation over Federated Knowledge Graphs (CEUR-WS, 2025)  
https://ceur-ws.org/Vol-3697/paper4.pdf

## Focus

Improving the accuracy of natural language to SPARQL query generation using Retrieval-Augmented Generation (RAG).

## Core Idea

Before generating SPARQL queries, relevant schema information, entity labels, and example queries are retrieved and provided to the LLM.

## Architecture

User → Chatbot → LLM + RAG → SPARQL → Knowledge Graph → Answer

## Key Contributions

- Introduces retrieval of ontology context to guide SPARQL generation.
- Reduces errors caused by incomplete schema understanding.
- Improves robustness for large and complex knowledge graphs.

## Evaluation

- Measures query execution success and result correctness.
- Shows that retrieval improves SPARQL accuracy compared to LLM-only approaches.

## Relevance

Extends baseline chatbot–ontology architectures by improving scalability and accuracy through retrieval.
