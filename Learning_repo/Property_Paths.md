# Property Paths

Used to define how the SPARQL processor should move between nodes, treating them as part of a directed graph.
Traditional queries (i.e. matching triple patterns) are of length one and begin/end with either URIs or variables. Similarly, property
paths must begin and end with URIs or variables, but cannot contain any variables within the path definition. If you are familiar with regex,
the operators are pretty much the same, only the use context is different.

Outside of reducing the amount of writing required for queries, property paths also allow you to match nodes based on their 
connectivity in the context of the graph rather than via an explicit connection between one another. Another perk is that
property paths allow you to unite datasets using different predicate terminology more easily than using `UNION` statements. 
When working with property paths, keep in mind the operations can apply both to URIs _and_ to path elements (makes more sense with the examples).

[W3C documentation](https://www.w3.org/TR/sparql11-query/#propertypaths). Also see pgs. 64-68 in _Learning SPARQL_.

### Operators

| Operator   | Description | 
| ---------- | ----------- |
| ^          | Inverse path from object to subject      |
| a/b        | Sequence path moving from a to b      | 
| \|         | "OR" Tries to find triples matching either possible pattern      |
| *          | Zero or more: finds paths of any length connecting subjet and object  |
| +          | One or more: finds paths of length 1+ that connect subject and object (subject is not directly object) |
| ?          |  Zero or one: extends traditional query to allow self reference     |
| !          |  Negation. Can be combined with (groups) and inverse to give tighter control than `MINUS` |
| (_group_)  |  Grouping of terms to control order of operations or provide additional readability |

### Examples

Some of the operators seem trivial on their own, but they are often quite useful in conjunction with the other operators. The examples below
are presented using property paths and (when possible) explicitly written:

1. Find Bob's (person:13948) job in disparate datasources
```
{ person:13948 (person:job|workDB:career|jobOntology:profession) ?job }

#Explicitly

{ {person:13948 person:job ?job} UNION {person:13948 workDB:career ?job} UNION {person:13948 jobOntology:profession ?job} }
```

2. Find the name of everyone Bob knows, everyone they know, and so on...

```
{ person:13948 foaf:knows+/foaf:name ?name }

#Explicitly

{ person:13948 foaf:knows ?foafID .
  ?foafID foaf:name ?name ;
          foaf:knows ?foafID2 .
  ?foafID2 foaf:name ?name2 ;
          foaf:knows ?foafID3 .
  #and so on indefinitley
 }
 
 ```
 
 Already it is clear that operators allow you to ask questions that would otherwise be infeasible or very ugly. Here are some other interesting tricks you can use:
 
 3. Find the class of an object and all subclasses, if they exist
 ```
 { ?item wdt:P31/wdt:P279* ?class. }
 
 #Explicitly
 
 {
   { ?item wdt:P31 ?class .}
    UNION
   { ?item wdt:P31 [wdt:P279 ?class] . }
    UNION
   { ?item wdt:P31 [wdt:P279 [wdt:P279 ?class]]. }
    #and so on indefinitley
 }
 ```
 
