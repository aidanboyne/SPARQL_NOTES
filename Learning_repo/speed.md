# SPARQL FASTER

SPARQL can be very tempermental. Queries that look practically identical may take radically different times to return the same result.
Here is a list of principles to make your queries faster. Of course, there are probably even faster ways out there, but sticking to this
has cut down my time staring at a loading screen by quite a bit :)


- Use `BIND` instead of `VALUES` wherever possible
  - `VALUES` is a powerful keyword, allowing you to assign multiple variables at the same time or create higher dimensional tables of results. 
     HOWEVER, this comes at a cost and I suspect (at least for GraphDB) that `VALUES` causes the engine to return all results matching the query bound variables,
     then runs an additional query to match the specified variables. `BIND` on the otherhand is highly optimizable by the engine and inserts the 
     variables into the query on the first pass, reducing the search space quite significantly.
  - `FILTER` = FAST. Mostly. At least faster than not using a filter 


If you are crazy, you could try to learn _SPARQL ALGEBRA_ to understand queries from the view of the engine. 
