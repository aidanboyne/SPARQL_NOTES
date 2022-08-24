SPARQL
===

#### Helpful Resources
- _Learning Sparql, 2nd Edition_ by Bob DuCharme: [Download](https://oiipdf.com/learning-sparql-2nd-edition)
  - Very thorough introduction to the language. Would reccommend reading and referring back to but don't get too caught up in the examples.
- [_SPARQL Working Group_](https://www.w3.org/TR/2013/REC-sparql11-overview-20130321/): Documentation of SPARQL by its creators
- [Learning Repo](https://github.com/aidanboyne/SPARQL_NOTES/blob/89a9e2205003ad47f6412d1c825d26697b4e2d9a/Learning_repo/info.md) on GraphDB
  - I've created a small repository with toy data that you can use. Files used to create the repo are under the **Learning_repo** folder in this github repository.
  - There are also several questions and example answers for the main KG that you can try to figure out and compare with solutions the team has written.
- VS Code has SPARQL support and is nice for sketching out ideas. GraphDB's editor is great for exploration but can be a bit slow to actually write long queries in.
- For a totally fresh start to query grammar, check [here](https://github.com/aidanboyne/SPARQL_NOTES/blob/57896da77396fadc0b7ccff643dfe291a2dab167/Example_Queries/Grammar_Basics.md).
- For info on property paths, see the W3 website or [here] (https://github.com/aidanboyne/SPARQL_NOTES/blob/9adabe3dde6b53db77f5b478eadd3adaa3e37f2e/Learning_repo/Property_Paths.md)
- If it looks like your query should work and you can't figure out what is wrong, check your spelling! Usually spelling/capitalizaiton errors in variables are the culprit.

---

SPARQL is the query language for RDF, a directed and labeled graph format for representing data.The power of SQARQL and RDF comes from incorporation of standardized ontologies, allowing disparate datasources to be connected via shared terminology. Data is primarily represented in **triples** consisting of a subject, predicate and object.

`dis:00001 rdfs:label "Alzheimer's Disease"`

Is an example of a triple with subject `dis:00001`, predicate `rdfs:label`, and object `"Alzheimer's Disease"`. Although "Alzheimer's Disease" is a string, it is usually preferable to use Universal Resource Identifers (URIs) in all positions of the triple for interoperability and you _cannot_ use strings (or any other type of literal such as integer, boolean, float...) as subject or preposition - SPARQL processors will throw an error message.

Note that a full URI looks something like `<http://www.w3.org/2000/01/rdf-schema#label>`. The `rdfs:` prefix takes the place of `<http://www.w3.org/2000/01/rdf-schema#>` to improve readability. To use these in a query, add `PREFIX abbv:partial_uri` to the top of your code. For example, the following two queries ask for identical informaiton (the full name of all men in a hypothetical database), yet it's a lot easier to understand the second query.

```
SELECT ?Name 
WHERE {
  ?ID <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://learning/ns/addressbook#man> ;
      <http://learning/ns/addressbook#firstName> ?firstName ;
      <http://learning/ns/addressbook#lastName> ?lastName .
  BIND ( CONCAT(?firstName, " ", ?lastname) AS ?Name)
}
```

Versus

```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX person: <http://learning/ns/addressbook#>

SELECT ?Name 
WHERE {
  ?ID rdf:type person:man ;
      person:firstName ?firstName ;
      person:lastName ?lastName .
  BIND ( CONCAT(?firstName, " ", ?lastname) AS ?Name)
}
```

Also, notice that SPARQL includes bulit in functions for working with strings such as `CONCAT` and variable assignment `BIND`. There are a ton of helpful functions out there and most of them are covered in _Learning SPARQL_.

