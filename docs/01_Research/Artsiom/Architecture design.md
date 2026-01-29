## Definitions

**RDF** - logic model (relationships) 
- 
**OWL** - puts logic logic constraints (rules)

`.ttl` (turtle) files - has RDF triples and OWL rules 
- build from triples: subject -> predicate -> object (e.g. Alice knows Bob)
- Tools: [protégé](https://protege.stanford.edu/),  RDF4J, SPARQL databases
- `owl:Class`, `owl:ObjectProperty`, 
`.aml`

### Possible pipelines
-> Intent matching -> SPARQL -> RDF accessor 
-> NL (Rule-based, trained parser, LLM gen) 
-> RAG - loses semantic?

Use **triple store/ RDF engine**: 
- GraphDB (build in OWL reasoning)
- Apache Jena Fuseki - reasoning setup is manual]
-  
***Expose SPARQL endpoint***

- **TTL parsing** - RDFLib
- **SPARQL** - GraphDB / Jena
- **vector DB** - ???

Use **RDFLib** ??
for embeddings: RDF -> text + metadata
embed via: `???`
store embeddings via: `???`
embed user question (via same model)
-> retreive related concepts 
?? use them now to build SRAPQL
get SPARQL results
Retrieve supporting text: about found suff (query results and concepts)
(basically take extracted results, form questions, and query them back to vecto_db)
- ontology defines structure by relation types, that helps define queries using templates
Getting all of these, assemble explanation context
Feed into LLM


What do we embed for RAG from TTL?
- class, props desctioptions
- entity labels & synonums
- Also external documentation


Questions:
- use SPARQL +RDF & OWL or Cypher + Neo4j?
	- What tool captures our data structure the best?
- Neo4j does not have inheritance
- what tool to use for 

Possible architectures:
Has to be highly modular to enable testing (docker?) - microservice?

![[Drawing 2026-01-29 12.14.37.excalidraw]]


