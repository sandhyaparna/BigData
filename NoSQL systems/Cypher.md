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
![](https://lh3.googleusercontent.com/ujrT8nIydCGuy42v1VLFa3AWSx4dOs4qdUCACGiU-wJ5LekFb4TRHcQOOjSOuQ_M8dba=s85)





What is Cypher?
Cypher is a graph query language that is used to query the Neo4j Database. Just like you use SQL to query a MySQL database, you would use Cypher to query the Neo4j Database.
A simple cypher query can look something like this
Match (m:Movie) where m.released > 2000 RETURN m limit 5















