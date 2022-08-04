## Patients, Drugs, and Diseases
---
This (very small) toy dataset includes data on people and their relationships, diseases, and drugs. To start, it can be helpful to explore the data with the following query.

```
SELECT *
WHERE {
  ?s ?p ?o
}

LIMIT 100
```

The `LIMIT` statement is very important when working with larger datasets so that you don't crash the server while exploring the data. Once you have an idea of how the data is structured, try to do the following via SPARQL Queries:
- List all patients and their full name
- Sort patients by their date of birth
- Find which drugs are not perscribed to any patient
- Identify the drugs used to treat Asthma
- Identify the drugs used to treat any neurological disorder
- Find where the patients see their doctor
- Find the symptom Rishab is likley suffering from


### Expanding the data
The triples in the graph can be uploaded directly using Turtle (.ttl) files or by using `INSERT` queries to construct new triples. For example, you could add another patient with a first and last name who has arthritis via the following query;

```
PREFIX sysbio: <http://learning/sysbio#> 
PREFIX  person:   <http://learning/ns/addressbook#> 
PREFIX  dis: <http://learning/diseases#> 
PREFIX  drg:  <http://learning/drugs#> 

INSERT {
person:i3625
   person:firstName "Aisha" ; 
   person:lastName  "Houmeini" ;
   person:dateOfBirth "1960-11-25"^^xsd:date ;
   sysbio:hasDisease dis:00002 ;
}
WHERE{}
```

Note that all examples uploaded to GDB repo are kept here as turtle (.ttl) files. To upload additional triples (such as those found in Bob DuCharme's book), go to GDB and use import RDF data, selecting the files you want.
