# **_Gmit Timetabling Neo4j Database_**

**Student Name:** Matthew Lally </br>
**Student ID:** G00322757 </br>
**Module:** Graph Theory </br>
**Lecturer:** Ian McLoughlin </br>

## **_Introduction_**
This project is a  part of a Graph Thoery Module based in GMIT (Galway-Mayo Institute of Technology). I have to design and build a
graph database using Neo4J and Cypher. Today Neo4J is the worlds most popular graph database managment system, it uses a language called Cypher as its query language. 

The database im implementing is supposed to contain data that shows how to  design and prototype a Neo4j  database for use
in a timetabling system for a third level institute like GMIT. At a minimum , the database should store information about student groups, classrooms, lecturers, and work hours – just like the currently used timetabling system at GMIT. 

## **_Graph Databases_**
A graph database is a database that uses graph structures for semantic queries with nodes, edges and properties to represent and store data. A key concept of the system is the graph (or edge or relationship), which directly relates data items in the store.

## **_What is Neo4j and Cypher_**
Sponsored by Neo Technology, Neo4j is an open-source NoSQL graph database implemented in Java and Scala. With development starting in 2003, it has been publicly available since 2007. The source code and issue tracking are available on GitHub, with support readily available on Stack Overflow and the Neo4j Google group. Neo4j is used today by hundreds of thousands of companies and organizations in almost all industries. Use cases include matchmaking, network management, software analytics, scientific research, routing, organizational and project management, recommendations, social networks, and more.


Some particular features make Neo4j very popular among users, developers, and DBAs:

- Materializing of relationships at creation time, resulting in no penalties for complex runtime queries
- Constant time traversals for relationships in the graph both in depth and in breadth due to efficient representation of nodes and relationships
- All relationships in Neo4j are equally important and fast, making it possible to materialize and use new relationships later on to “shortcut” and speed up the domain data when new needs arise
- Compact storage and memory caching for graphs, resulting in efficient scale-up and billions of nodes in one database on moderate hardware
- Written on top of the JVM

Cypher is a declarative graph query language that allows for expressive and efficient querying and updating of the graph store. Cypher is a relatively simple but still very powerful language. Very complicated database queries can easily be expressed through Cypher.
Cypher is inspired by SQL , it allows us to state what we want to select, insert, update or delete from our graph data without requiring us to describe exactly how to do it.

Neo4j and and Cypher is essentially the equvililant to MySQL and SQL. The main difference being that MySQL is a relational database management system and SQL (Structured Query Language) is MySQL's supporting language.

## **_Creating the database_**
Before creating the database , I had to sit down and think what information would be needed in the database. I would need information on the student groups, the lecturers, classrooms and the hours when the lectures would run. I also had to consider that a student group could not be in the two different rooms at the same time and that a lecturer could not be in two different rooms at the same time. For the purposes of my project I looked at the first three years of the Software Development course in GMIT. I first created nodes for the days of the week, I did this by adding the following command
> CREATE (: Day { day:'Monday'});

Next I had to go on too the http://timetable.gmit.ie/ and extract the data I need for the rooms the lectures for each module were taking place in. I did this by viewing the page source on each courses timetable. I started off by getting the data for all the First Year software development modules and worked my way down to third year.
To Create a room I used the following command :
> CREATE (: Room { Number:'997'});

The next thing I did was to again go on to http://timetable.gmit.ie/ and extract the names for the modules each year of the software development course. To do this I used two different commands in cypher. I used the following command to create the years of the course
> CREATE (: Year { year: 'Year One'});

To create a command for the modules I did used the following command : 
> CREATE(: FirstYearModule { module:'SOFTWARE DESIGN & PROG DEV 1 '});

Next I had to create the lecturers. To do find the information on the lecturers I logged onto https://learnonline.gmit.ie/ and using the search course option entered in the names of each module and got the lecturer name. The command I then used to create each lecturer was 
> CREATE (: Lecturer {name :'Ian McLoughlin'} );

## **_Adding the relationships_**
At first I was not entirely sure how to create relationships using cypher. A quick google search however gave me this stackoverflow answer : http://stackoverflow.com/questions/20456002/adding-relationship-to-existing-nodes-with-cypher . I will be using commands similar to this for most of the relationships I will be creating.  The first relationship I decided to add was a relationship between a module and the year it takes place . An example of what I did to create a relationship between the years and the modules in first year is  
> match (mod: FirstYearModule), (y: Year{year:'Year One'})
create (mod)-[:In]->(y)

The next relationship I had to create was a relationship between a lecturer and the module they teach. To do this for my lecturer Ian McLoughlin and the class he teaches graph theory I did the following :
> match (l: Lecturer { name:'Ian McLoughlin'}), (m: ThirdYearModule{ module:'GRAPH THEORY'})
create (l)-[:Teaches]->(m)



 






