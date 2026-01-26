# E1 — Chatbot-Based Ontology Interaction Using Large Language Models

**Paper:**  
Chatbot-Based Ontology Interaction Using Large Language Models and Domain-Specific Standards (2024)  
https://arxiv.org/html/2408.00800v1

## Focus
Querying ontology-based technical knowledge using a chatbot and Large Language Models.

## Core Idea
Natural language questions are translated into SPARQL queries, which are executed over an ontology. The LLM is used only to generate queries, not to produce answers.

## Architecture
User → Chatbot → LLM → SPARQL → Knowledge Graph → Structured Answer

## Key Contributions
- Uses LLMs as SPARQL query generators instead of answer generators.
- Prevents hallucinations by grounding answers strictly in ontology data.
- Improves usability of ontologies for non-expert users.
- Incorporates ontology schema (TBox) into prompts for better query generation.

## Evaluation
- Evaluates correctness of generated SPARQL queries.
- Shows higher accuracy for simpler, standard-compliant questions.
- Demonstrates improved performance when ontologies include semantic annotations (e.g. rdfs:comment).

## Relevance
Provides a baseline architecture for safe chatbot-based querying of technical and engineering knowledge.
