**RQ1**: How can Ontology information be efficiently embedded to be used by RAG?


## Overview paper
[[ONTOLLM_2025_Aug20v11.pdf]]
- **RQ1: the property chains found in ontologies serve as the data being embedded, ontology design is particularly important**
- found 4,641 publications, revieved top 30 cited 
- resulting embeddings do not retain the semantics and do not support
reasoning
-  fine-tuning offers better reasoning-like capabilities
- LMs can convert unstructured text into graph representations that reflect
contextual knowledge through subgraph traversal, often up to two hops deep
- **Evaluation** is conducted through LLM-based scoring against human-labeled ground
truth
- (Approach 1) Hierarchical retrieval mechanisms over hypergraphs, where hyperedges cluster related factual units, allow for multi-level reasoning over structured content
- Query templates like “Considering \<CONTEXT\>, answer \<QUESTION\>” structure
the interaction between retrieved knowledge and LLMs

## Approach 1 - Ontology-Grounded RAG
[[2025.emnlp-main.1674.pdf|Source]]
- General-Purpose approach - can be applied to any domain
- Nicely documented - with provided algorithm and expected benefits over base RAG.
- Proposes how to work with the documents, which are not inside ontology!
- Provides samples of prompts
- RQ1: by embedding prop chains, detailed algorithm below

### Simplified description:
1. Per each subject (s) construct Factual Blocks (F) (*which subjects are relevant, a decision has to be made, overall its TBox defined domain subjects with attributes and other* )
	1. Recursively extract attributes (a), until literal value (v) is reached (number/string), unwrapping subject s attributes
	2. Every such path from subject s to the leaf attribute is a node (n). Node is a (key, value) pair, where key is concatenated path, `(s concat v)+`, value is the leaf attribute value v (*node is literally is a pair of string path and value*)
	3. All such paths (nodes) are linked to the same edge (e) *store, with ability to search e using n* (e corresponds and describes F)
2. Embed nodes: separately embed key and value (keep them in separate storages, but same (?) vector space)
3. Retrieval:
	1. Embed user query Q
	2. Find k closest nodes to the Q: k closes nodes by key, and by value (so 2\*k sets from two embedding storages).
	3. Perform greedy algorithm; find the smallest amount of edges, which can cover all nodes (or up to set limit of edges)
	4. Use extracted edges as the context and Q to get final answer

### Pipeline:
![[Pasted image 20260210210343.png]]


## Approach 2: “Think-on-Graph"
[[2307.07697v6.pdf]]
- Using the beam search algorithm
- (have to read it)