### SPARQL Query Grammar

Multiple predicates for same subject are separated by **semicolons**. <br>
Multiple objects for same subject and predicate are separated by **commas**. <br>
Each triple about a subject is terminated with a **period**. <br>

```
SELECT ?s1 ?s2 ?s3 
WHERE
{
  ?s1 p1 o1;
      p2 o2;
      p3 o31, o32, o33.
  ?s2 p4 o41, o42.
  ?s3 p5 o5;
      p6 o6.
}
```

Brackets can be used to create an anonymous linking variable when you don't intend on using the link. For example

`person:Juliet action:loves person:someone . 
 person:someone action:kills person:Tybalt .`
 
Is interpreted identically to 

`person:Juliet action:loves [ action:kills person:Tybalt ].`
