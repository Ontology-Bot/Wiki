---
Auther: Ahmed
Date: 2026-01-29
Source: "[[2310.04560v1.pdf]]"
Status: IN PROGRESS
---

They are trying to see how LLMs can work with Graphs Databases or _Knowledge Graphs_ . 

They propose a decomposition:
- graph encoding 
- graph prompt engineering

![[Pasted image 20260129163100.png]]

Results: 
![[Pasted image 20260129163841.png]]


We formulate the problem as 
![[Pasted image 20260129173009.png]]
Where 
f: the model, An LLM here
g(.) : Graph encoding function
q(.): Question rephrasing function
A,G,Q: The answer, the graph, and the question

### They also use different Promoting Heuristics

| **Prompting Method**             | **Abbreviation** | **Key Characteristics / Description**                                                                                                 | **Key Reference**                                           |
| -------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| **Zero-shot prompting**          | ZERO-SHOT        | Provides a task description and asks for output without any prior training or examples.                                               | N/A                                                         |
| **Few-shot in-context learning** | FEW-SHOT         | Provides a small number of examples (input-output pairs) for the model to learn from.                                                 | Brown et al., 2020b                                         |
| **Chain-of-thought prompting**   | COT              | Provides examples that show how to solve a task step-by-step.                                                                         | Wei et al., 2022                                            |
| **Zero-shot CoT prompting**      | ZERO-COT         | Similar to CoT but uses a simple prompt like "Let's think step by step" instead of providing examples.                                | Kojima et al., 2022                                         |
| **Bag prompting**                | COT-BAG          | Designed for graph-related tasks; appends "Let's construct a graph with the nodes and edges first" to the description.                | Wang et al., 2023                                           |
| **Iterative prompting**          | N/A              | Uses a series of iterative queries to optimize the prompt; noted as performing poorly in this specific paper due to cascading errors. | Zhou et al., 2022b; Pryzant et al., 2023; Yang et al., 2023 |


## Encoding the graph

Encoding is funn!!
![[Pasted image 20260129175015.png]]








