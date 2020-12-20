### What is Cypher?
Cypher is a graph query language that is used to query the Neo4j Database. Just like you use SQL to query a MySQL database, you would use Cypher to query the Neo4j Database.
* Return everything in the database </br>
Match (n) Return n
* Write a query to retrieve all the movies released after the year 2005. </br>
Match (m:Movie) where m.released > 2005 RETURN m
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/Cypher1.png)
* Write a query to retrieve 5 movies released after the year 2005. </br>
Match (m:Movie) where m.released > 2005 RETURN m limit 5
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/Cypher2.PNG)
* Write a query to return the count of movies released after the year 2005. (Hint: you can use the count(m) function to return the count) </br>
Match (m:Movie) where m.released > 2005 RETURN count(m)

### Nodes and Relationships
* Nodes and Relationships are the basic building blocks of a graph database.
* Nodes: Nodes represent entities. A node in graph database is similar to a row in a relational database. In the picture below we can see 2 kinds of nodes - Person and Movie. In writing a cypher query, a node is enclosed between a parenthesis — like (p:Person) where p is a variable and Person is the type of node it is referring to.
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/Realtionship1.PNG)
* Relationship: Two nodes can be connected with a relationship. In the above image ACTED_IN, REVIEWED, PRODUCED, WROTE and DIRECTED are all relationships connecting the corresponding types of nodes. </br>
In writing a cypher query, relationships are enclosed in square brackets - like [w:WORKS_FOR] where w is a variable and WORKS_FOR is the type of relationship it is referring to. </br>
Two nodes can be connected with more than one relationships. </br>
* MATCH (p:Person)-[d:DIRECTED]-(m:Movie) where m.released > 2010 RETURN p,d,m. </br>
Expected Result: The above query will return all Person nodes who directed a movie that was released after 2010.
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/Realtionship2.PNG)
* Query to get all the people who acted in a movie that was released after 2010. </br>
MATCH (p:Person)-[d:ACTED_IN]-(m:Movie) where m.released > 2010 RETURN p,d,m
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/Realtionship3.PNG)

### Labels
* Labels is a name or identifer of a Node or a Relationship. In the image below Movie and Person are Node labels and ACTED_IN, REVIEWED, etc are Relationship labels.
* In writing a cypher query, Labels are prefixed with a colon - like :Person or :ACTED_IN. You can assign the node label to a variable by prefixing the syntax with the variable name. Like (p:Person) means p variable denoted Person labeled nodes.
* Labels are used when you want to perform operations only on a specific types of Nodes </br>
MATCH (p:Person) RETURN p limit 20 </br>
will return only Person Nodes (limiting to 20 items)  </br>
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/Labels2.png)
* MATCH (n) RETURN n limit 20 </br>
will return all kinds of nodes (limiting to 20 items).
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/Labels1.png)

### Properties
* Properties are name-value pairs that are used to add attributes to nodes and relationships.
* To return specific properties of a node you can write - </br>
MATCH (m:Movie) return m.title, m.released.  </br>
Will return Movie nodes but with only the title and released properties.  </br>
* Wrtie a query to get name and born properties of the Person node  </br>
MATCH (p:Person) return p.name, p.born
* To get properties of Movie node  </br>
Match (m:Movie)  WITH DISTINCT keys(m) AS keys  </br>
UNWIND keys AS keyslisting WITH DISTINCT keyslisting AS allfields  </br>
RETURN allfields;  </br>

### Create a Node
Create clause can be used to create a new node or a relationship.
*  Create a new Person node with property name having value John Doe. </br>
Create (p:Person {name: 'John Doe'}) RETURN p
* Create a new Person node with a property name having the value of your name.  </br>
Create (p:Person {name: '<Your Name>'}) RETURN p

### Finding Nodes with Match and Where Clause
* Match clause is used to find nodes that match a particular pattern. This is the primary way of getting data from a Neo4j database.
* In most cases, a Match is used along with certain conditions to narrow down the result. </br>
Match (p:Person {name: 'Tom Hanks'}) RETURN p </br>
This is one way of doing it. Although you can only do basic string match based filtering this way (without using WHERE clause) </br>
Another way would be to use a WHERE clause which allows for more complex filtering including >, <, Starts With, Ends With, etc  </br>
MATCH (p:Person) where p.name = "Tom Hanks" RETURN p
* Find the movie with title "Cloud Atlas" </br>
MATCH (m:Movie {title: "Cloud Atlas"}) return m
* Get all the movies that were released between 2010 and 2015 </br>
MATCH (m:Movie) where m.released > 2010 and m.released < 2015 RETURN m

### Merge Clause
* The Merge clause is used to either
  * match the existing nodes and bind them or
  * create new node(s) and bind them
* It is a combination of Match and Create and additionally allows to specify additional actions if the data was matched or created.
* MERGE (p:Person {name: 'John Doe'}) </br>
ON MATCH SET p.lastLoggedInAt = timestamp() </br>
ON CREATE SET p.createdAt = timestamp() </br>
Return p </br>
The above statement will create the Person node if it does not exist. If the node already exists, then it will set the property lastLoggedInAt to the current timestamp. If node did not exist and was newly created instead, then it will set the createdAt property to the current timestamp.
* Write a query using Merge to create a movie node with title "Greyhound". If the node does not exist then set its released property to 2020 and lastUpdatedAt property to the current time stamp. If the node already exists, then only set lastUpdatedAt to the current time stamp. Return the movie node. </br>
MERGE (m:movie {title: 'Greyhound'}) </br>
ON MATCH SET m.lastUpdatedAt = timestamp() </br>
ON CREATE SET m.released = "2020", m.lastUpdatedAt = timestamp() </br>
Return m </br>

### Create a Relationship
* A Relationship connects 2 nodes.
* MATCH (p:Person), (m:Movie) </br>
WHERE p.name = "Tom Hanks" and m.title = "Cloud Atlas" </br>
CREATE (p)-[w:WATCHED]->(m) </br>
RETURN type(w) </br>
The above statement will create a relationship :WATCHED between the existing Person and Movie nodes and return the type of relationship (i.e WATCHED).
* Create a relationship :WATCHED between the node you created for yourself previously in step 6 and the movie Cloud Atlas and then return the type of created relationship </br>
MATCH (p:Person), (m:Movie) </br>
WHERE p.name = "<Your Name>" and m.title = "Cloud Atlas" </br>
CREATE (p)-[w:WATCHED]->(m) </br>
RETURN type(w) </br>

### Relationship Types
* In Neo4j, there can be 2 kinds of relationships - incoming and outgoing.
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/RealtionshipTypes1.PNG) </br>
In the above picture, the Tom Hanks node is said to have an outgoing relationship while Forrest Gump node is said to have an incoming relationship.
* Relationships always have a direction. However, you only have to pay attention to the direction where it is useful.
* To denote an outgoing or an incoming relationship in cypher, we use → or ←.
* MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) RETURN p,r,m </br>
In the above query Person has an outgoing relationship and movie has an incoming relationship.
* Although, in the case of the movies dataset, the direction of the relationship is not that important and even without denoting the direction in the query, it will return the same result. So the query - </br>
MATCH (p:Person)-[:ACTED_IN]-(m:Movie) RETURN p,r,m </br>
will return the same reuslt as the above one. </br>
* Write a query to find the nodes Person and Movie which are connected by REVIEWED relationship and is outgoing from the Person node and incoming to the Movie node. </br>
MATCH (p:Person)-[r:REVIEWED]-(m:Movie) return p,r,m </br>
![](https://github.com/sandhyaparna/NoSQL-BigData/blob/master/NoSQL%20systems/Images/RealtionshipTypes2.png)

### Advcance Cypher queries
* Finding who directed Cloud Atlas movie </br>
MATCH (m:Movie {title: 'Cloud Atlas'})<-[d:DIRECTED]-(p:Person) return p.name
* Finding all people who have co-acted with Tom Hanks in any movie </br>
MATCH (tom:Person {name: "Tom Hanks"})-[:ACTED_IN]->(:Movie)<-[:ACTED_IN]-(p:Person) return p.name
* Finding all people related to the movie Cloud Atlas in any way </br>
MATCH (p:Person)-[relatedTo]-(m:Movie {title: "Cloud Atlas"}) return p.name, type(relatedTo) </br>
In the above query we only used the variable relatedTo which will try to find all the relationships between any Person node and the movie node "Cloud Atlas"
* Finding Movies and Actors that are 3 hops away from Kevin Bacon. </br>
MATCH (p:Person {name: 'Kevin Bacon'})-[*1..3]-(hollywood) return DISTINCT p, hollywood </br>
Note: in the above query, hollywood refers to any node in the database (in this case Person and Movie nodes)

https://neo4j.com/docs/cypher-manual/4.0/











