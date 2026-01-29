[[noy01.pdf]]

Can we reuse existing ontologies?

"there is no single correct ontology for any domain"
"ontology design is a creative process"
**"can be assessed only by usage"**

If the ontology we are designing **will be used to assist in natural language processing** of articles
in our domain, it may be **important to include synonyms** and part-of-speech information
for concepts in the ontology

One of the ways **to determine the scope of the ontology** is to **sketch a list of questions** that a
knowledge base based on **the ontology should be able to answer**, competency questions
They will serve as tests later
- Does the ontology contain enough information to answer these types of questions? 
- Do the answers require a particular level of detail or representation of a particular area? 

**Class** describes a concept (e.g class wine - alll possible wines)
**Subclass** = more speciefic (wine -> sparkling wine)

Concepts in the ontology should be close to objects (physical or logical)
and relationships in your domain of interest. These are most likely to be
**nouns** (objects) or **verbs** (relationships) in sentences that describe your
domain

In practical terms, developing an ontology includes:
- defining classes in the ontology,
- arranging the classes in a taxonomic (subclass–superclass) hierarchy,
- defining slots (aka props) and describing allowed values for these slots,
- filling in the values for slots (aka props) for instances


Iterative development: (**Ontology development is necessarily an iterative process**.)
- Determine the domain and scope of the ontology
- Define the classes and the class hierarchy
- Enumerate important terms in the ontology
- Define the properties of classes—slots
- Define the facets of the slots - cardinality, value type, range(allowed classes)
- ...


