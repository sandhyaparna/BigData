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
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/image.png)
* Relationship: Two nodes can be connected with a relationship. In the above image ACTED_IN, REVIEWED, PRODUCED, WROTE and DIRECTED are all relationships connecting the corresponding types of nodes. </br>
In writing a cypher query, relationships are enclosed in square brackets - like [w:WORKS_FOR] where w is a variable and WORKS_FOR is the type of relationship it is referring to. </br>
Two nodes can be connected with more than one relationships. </br>
* MATCH (p:Person)-[d:DIRECTED]-(m:Movie) where m.released > 2010 RETURN p,d,m. Expected Result: The above query will return all Person nodes who directed a movie that was released after 2010.
* Query to get all the people who acted in a movie that was released after 2010. </br>
MATCH (p:Person)-[d:ACTED_IN]-(m:Movie) where m.released > 2010 RETURN p,d,m


Labels
* Labels is a name or identifer of a Node or a Relationship. In the image below Movie and Person are Node labels and ACTED_IN, REVIEWED, etc are Relationship labels.
* In writing a cypher query, Labels are prefixed with a colon - like :Person or :ACTED_IN. You can assign the node label to a variable by prefixing the syntax with the variable name. Like (p:Person) means p variable denoted Person labeled nodes.
* Labels are used when you want to perform operations only on a specific types of Nodes. Like
* MATCH (p:Person) RETURN p limit 20. will return only Person Nodes (limiting to 20 items) while

* MATCH (n) RETURN n limit 20. will return all kinds of nodes (limiting to 20 items).


Properties
* Properties are name-value pairs that are used to add attributes to nodes and relationships.
* To return specific properties of a node you can write -
* MATCH (m:Movie) return m.title, m.released. Returns movie title and released year
* Wrtie a query to get name and born properties of the Person node.: MATCH (p:Person) return p.name, p.born


Create a Node
Create clause can be used to create a new node or a relationship.
*  Create a new Person node with property name having value John Doe. Create (p:Person {name: 'John Doe'}) RETURN p

* Create a new Person node with a property name having the value of your name. Create (p:Person {name: '<Your Name>'}) RETURN p


Finding Nodes with Match and Where Clause
* Match clause is used to find nodes that match a particular pattern. This is the primary way of getting data from a Neo4j database.
* In most cases, a Match is used along with certain conditions to narrow down the result.
* Match (p:Person {name: 'Tom Hanks'}) RETURN p
* This is one way of doing it. Although you can only do basic string match based filtering this way (without using WHERE clause).
* Another way would be to use a WHERE clause which allows for more complex filtering including >, <, Starts With, Ends With, etc
* MATCH (p:Person) where p.name = "Tom Hanks" RETURN p
* Find the movie with title "Cloud Atlas". MATCH (m:Movie {title: "Cloud Atlas"}) return m
* Get all the movies that were released between 2010 and 2015. MATCH (m:Movie) where m.released > 2010 and m.released < 2015 RETURN m

Merge Clause
* The Merge clause is used to either
  * match the existing nodes and bind them or
  * create new node(s) and bind them
* It is a combination of Match and Create and additionally allows to specify additional actions if the data was matched or created.
* MERGE (p:Person {name: 'John Doe'}) </br>
ON MATCH SET p.lastLoggedInAt = timestamp() </br>
ON CREATE SET p.createdAt = timestamp() </br>
Return p </br>
* The above statement will create the Person node if it does not exist. If the node already exists, then it will set the property lastLoggedInAt to the current timestamp. If node did not exist and was newly created instead, then it will set the createdAt property to the current timestamp.
* Write a query using Merge to create a movie node with title "Greyhound". If the node does not exist then set its released property to 2020 and lastUpdatedAt property to the current time stamp. If the node already exists, then only set lastUpdatedAt to the current time stamp. Return the movie node. </br>
MERGE (m:movie {title: 'Greyhound'}) </br>
ON MATCH SET m.lastUpdatedAt = timestamp() </br>
ON CREATE SET m.released = "2020", m.lastUpdatedAt = timestamp() </br> </br>
Return m </br>



























