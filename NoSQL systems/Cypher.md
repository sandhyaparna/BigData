Table:
{ 
  "identity": 9,
  "labels": [
    "Movie"
  ],
  "properties": {
"title": "The Matrix Reloaded",
"tagline": "Free your mind",
"released": 2003
  }
}
{
  "identity": 10,
  "labels": [
    "Movie"
  ],
  "properties": {
"title": "The Matrix Revolutions",
"tagline": "Everything that has a beginning has an end",
"released": 2003
  }
{
  "identity": 154,
  "labels": [
    "Movie"
  ],
  "properties": {
"title": "Something's Gotta Give",
"released": 2003
  }
}
{
  "identity": 161,
  "labels": [
    "Movie"
  ],
  "properties": {
"title": "The Polar Express",
"tagline": "This Holiday Season… Believe",
"released": 2004
  }
}
{
  "identity": 92,
  "labels": [
    "Movie"
  ],
  "properties": {
"title": "RescueDawn",
"tagline": "Based on the extraordinary true story of one man's fight for freedom",
"released": 2006
  }
}


What is Cypher?
Cypher is a graph query language that is used to query the Neo4j Database. Just like you use SQL to query a MySQL database, you would use Cypher to query the Neo4j Database.
* Write a query to retrieve all the movies released after the year 2005. </br>
Match (m:Movie) where m.released > 2005 RETURN m
* Write a query to return the count of movies released after the year 2005. (Hint: you can use the count(m) function to return the count) </br>
Match (m:Movie) where m.released > 2005 RETURN count(m)

Nodes and Relationships
* Nodes and Relationships are the basic building blocks of a graph database.
* Nodes: Nodes represent entities. A node in graph database is similar to a row in a relational database. In the picture below we can see 2 kinds of nodes - Person and Movie. In writing a cypher query, a node is enclosed between a parenthesis — like (p:Person) where p is a variable and Person is the type of node it is referring to.
![](


* Relationship: Two nodes can be connected with a relationship. In the above image ACTED_IN, REVIEWED, PRODUCED, WROTE and DIRECTED are all relationships connecting the corresponding types of nodes.

In writing a cypher query, relationships are enclosed in square brackets - like [w:WORKS_FOR] where w is a variable and WORKS_FOR is the type of relationship it is referring to.

Two nodes can be connected with more than one relationships.

MATCH (p:Person)-[d:DIRECTED]-(m:Movie) where m.released > 2010 RETURN p,d,m
Hint: You can click on the query above to populate it in the editor.
Expected Result: The above query will return all Person nodes who directed a movie that was released after 2010.

movies after 2010
Try

Query to get all the people who acted in a movie that was released after 2010.

MATCH (p:Person)-[d:ACTED_IN]-(m:Movie) where m.released > 2010 RETURN p,d,m













