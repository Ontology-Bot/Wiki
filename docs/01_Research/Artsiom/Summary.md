## Helpful links
free opensource ontology builder [protégé](https://protege.stanford.edu/)
  
Official tutorial from neo4j RAG  
[https://neo4j.com/blog/developer/rag-tutorial/](https://neo4j.com/blog/developer/rag-tutorial/)  
[https://neo4j.com/labs/neosemantics/](https://neo4j.com/labs/neosemantics/)
## Very short summary of papers

### before 2021 approaches (before LLMs):

- User -> intent/entity extraction -> NL module -> Query generation-> format -> User
- Regex extraction -> keywords -> (same)  
### after 2021+ approaches

- Generate query using LLM
- RAG (?)

## Details

### E-commerce Chatbot (2018) [[Ontology_based_Chatbot_For_E_commerce_We.pdf]]
![[Pasted image 20260129110716.png|300]]
- Wit.ai for dialog management (obtaining intent)
- Protégé online tool to create ontology
- entities are created from mentioning products, and their props
- used external platform for ontology dev

### E-learning Chatbot (2021) 
[[SM2676.pdf]]

- architecture:
![[Pasted image 20260129131149.png|400]]
![[Pasted image 20260129131211.png|400]]
- 932 chatbot questions dataset! - split on train & test
- The **Subword Semantic Hashing** method is used to provide the features input to classify an intent and get keywords (claims its the best)
- did train the intent classifier - used a bunch of them and selected the best by tests
- Retrieves relevant knowledge using keywords(enhanced by synonyms)
- the knowledge base needs to have communication scripts to interact with the user naturally

![[Pasted image 20260129131111.png|400]]

### Industry 4.0 Chatbot (2024)
[[2408.00800v2.pdf]]


- uses LLMs to generate SPARQL queries
	- feeds TBox for this (terminology = vocabulary + constraints of the domain
- Good results!
- traceability of answers
- Enhancing ODPs with **rdfs:comment** annotations is critical, as these provide additional context about the classes, object properties, and data properties
- flow
![[Pasted image 20260129132608.png|350]]

- assessment
![[Pasted image 20260129150134.png|300]]

![[Pasted image 20260129150617.png|250]]
### Generative approach for SPARQL queries
[[ieee_access_sgpt.pdf]]

"Most approaches are template-based"
Adopt BLEU and F1 score to measure accuracy 

Do not really understand this paper

![[Pasted image 20260129152201.png|400]]


### KBot IEEE
[[KBot_A_Knowledge_Graph_Based_ChatBot_for_Natural_Language_Understanding_Over_Linked_Data.pdf]]

