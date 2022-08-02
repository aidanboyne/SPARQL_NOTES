SPARQL
===

#### Helpful Resources
- _Learning Sparql, 2nd Edition_ by Bob DuCharme: [Download](https://oiipdf.com/learning-sparql-2nd-edition)
  - Very thorough introduction to the language. Would reccommend reading and referring back to but don't get too caught up in the examples.
- [_SPARQL Working Group_](https://www.w3.org/TR/2013/REC-sparql11-overview-20130321/): Documentation of SPARQL by its creators
- Learning Repo on GraphDB
  - I've created a small repository with toy data corresponding to the examples that you can use. Files used to create the repo are under the **Learning_repo** folder in this github repository.

---

SPARQL is the query language for RDF, a directed and labeled graph format for representing data.The power of SQARQL and RDF comes from incorporation of standardized ontologies, allowing disparate datasources to be connected via shared terminology. Data is primarily represented in **triples** consisting of a subject, predicate and object.

`dis:00001 rdfs:label "Alzheimer's Disease"`

Is an example of a triple with subject `dis:00001`, predicate `rdfs:label`, and object `"Alzheimer's Disease"`. Although "Alzheimer's Disease" is a string, it is usually preferable to use Universal Resource Identifers in all positions of the triple for interoperability. 
