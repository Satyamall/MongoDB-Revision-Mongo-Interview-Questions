
Mongo Interview Questions:

# What is SQL Databases? What are some companies who uses Mongo, what type of applications are these?
=> SQL is the most common language for extracting and organising data that is stored in a relational database. A database is a table that consists of rows and columns. SQL is the language of databases. It facilitates retrieving specific information from databases that are further used for analysis.

**Some Real-World Companies That Use MongoDB:**
- eBay. eBay is a multinational company that provides a platform for the customer to customer sales. ...
- MetLife. MetLife is a leading company in employee benefit programs, annuities, and insurance. ...
- Shutterfly. 
- Aadhar.
- EA.

**Type of applications are:** 
MongoDB is the most commonly used database in the development industry as a Document database. In document databases, the basic concept of table and row in compare with SQL database has been changed. Here row has been replaced by the term document which is much more flexible and model-based data structure.

# What is NoSQL Databases? What are some companies who uses Mongo, what type of applications are these?
=> NoSQL databases (aka "not only SQL") are non-tabular databases and store data differently than relational tables. NoSQL databases come in a variety of types based on their data model. The main types are document, key-value, wide-column, and graph.

**Some Real-World Companies That Use MongoDB:**
- eBay. eBay is a multinational company that provides a platform for the customer to customer sales. ...
- MetLife. MetLife is a leading company in employee benefit programs, annuities, and insurance. ...
- Shutterfly. 
- Aadhar.
- EA.

**Type of applications are:** 
MongoDB is the most commonly used database in the development industry as a Document database. In document databases, the basic concept of table and row in compare with SQL database has been changed. Here row has been replaced by the term document which is much more flexible and model-based data structure.

# What is the difference between SQL and NoSQL databases?
=>              SQL           |    	        NoSQL
RELATIONAL DATABASE MANAGEMENT SYSTEM (RDBMS)  | Non-relational or distributed database system.
These databases have fixed or static or predefined schema	|   They have dynamic schema
These databases are not suited for hierarchical data storage. | 	These databases are best suited for hierarchical data storage.
These databases are best suited for complex queries  |   	These databases are not so good for complex queries
Vertically Scalable	           |     Horizontally scalable
Follows ACID property	       |     Follows CAP(consistency, availability, partition tolerance)

# What are some features of MongoDB?
=> Let’s take a look at MongoDB’s top five technical features:

- 1. **Ad-hoc queries for optimized, real-time analytics:** 
   When designing the schema of a database, it is impossible to know in advance all the queries that will be performed by end users. An ad hoc query is a short-lived command whose value depends on a variable. Each time an ad hoc query is executed, the result may be different, depending on the variables in question.

- 2. **Indexing appropriately for better query executions:**
   In our experience, the number one issue that many technical support teams fail to address with their users is indexing. Done right, indexes are intended to improve search speed and performance. A failure to properly define appropriate indices can and usually will lead to a myriad of accessibility issues, such as problems with query execution and load balancing.

- 3. **Replication for better data availability and stability:**
   When your data only resides in a single database, it is exposed to multiple potential points of failure, such as a server crash, service interruptions, or even good old hardware failure. Any of these events would make accessing your data nearly impossible.

- 4. **Sharding:**
   When dealing with particularly large datasets, sharding—the process of splitting larger datasets across multiple distributed collections, or “shards”—helps the database distribute and better execute what might otherwise be problematic and cumbersome queries. Without sharding, scaling a growing web application with millions of daily users is nearly impossible.

- 5. **Load balancing:**
   At the end of the day, optimal load balancing remains one of the holy grails of large-scale database management for growing enterprise applications. Properly distributing millions of client requests to hundreds or thousands of servers can lead to a noticeable (and much appreciated) difference in performance.

# What are aggregate queries?
=> An aggregate query is a method of deriving group and subgroup data by analysis of a set of individual data entries. The term is frequently used by database developers and database administrators.

# What are pipelines in aggregation?
=> An aggregation pipeline consists of one or more stages that process documents:  <a href="https://www.mongodb.com/docs/manual/core/aggregation-pipeline/#:~:text=An%20aggregation%20pipeline%20consists%20of,passed%20to%20the%20next%20stage.">Link</a>
- Each stage performs an operation on the input documents. For example, a stage can filter documents, group documents, and calculate values. 
- The documents that are output from a stage are passed to the next stage.
- An aggregation pipeline can return results for groups of documents. For example, return the total, average, maximum, and minimum values.

# How do you do aggregate queries?
=> db.collection.aggregate(pipeline, options)
Example: 
```js
db.orders.aggregate([
                     { $match: { status: "A" } },
                     { $group: { _id: "$cust_id", total: { $sum: "$amount" } } },
                     { $sort: { total: -1 } }
                   ],
                   {
                       cursor: { batchSize: 0 }
                   }
                   )
```

# How can you group by a particular value in MongoDB?
=> $group:  Groups input documents by the specified _id expression and for each distinct grouping, outputs a document. The _id field of each output document contains the unique group by value.

Syntax:
```js
{
  $group:
    {
      _id: <expression>, // Group By Expression
      <field1>: { <accumulator1> : <expression1> },
      ...
    }
 }
```
Example:
```js
db.foo.aggregate([
  {
    $sort:{ x : 1, y : 1 }
  },
  {
    $group: {
      _id: { x : "$x" },
      y: { $first : "$y" }
    }
  }
])
```

# How can you paginate on MongoDB?
=> Below is the syntax of MongoDB pagination.

1) MongoDB pagination by using limit method
```js
db.collection_name.find ().limit (number);
```
2) MongoDB pagination by using skip method
```js
db.collection_name.find ().skip (number);
```
3) MongoDB pagination using the ID field
```js
db.collection_name.find ( {'_id': { 'Projection_operator': field_name } } )
```
4) MongoDB pagination using slice operator
```js
db.collection_name.find ( { }, { field_name: {$slice: [number1, number2] } } )
```
5) MongoDB pagination using ranged queries –
```js
db.collection_name.find ().min ( { _id:0 } ).max ( { _id:3 } )
```
6) MongoDB pagination using create an index
```js
db.collection_name.createIndex ( {field_name: -1} )
```
Example:
```js
db.collection_name.find()
             .skip( pageNumber > 0 ? ( ( pageNumber - 1 ) * nPerPage ) : 0 )
             .limit( nPerPage )
             );
```

# How can you sort in MongoDB?
=> $sort or cursor.sort(sort)
Sorts all input documents and returns them to the pipeline in sorted order.

The $sort stage has the following prototype form:
```js
{ $sort: { <field1>: <sort order>, <field2>: <sort order> ... }}
``
$sort takes a document that specifies the field(s) to sort by and the respective sort order. <sort order> can have one of the following values:

Value  |       Description
1      |      Sort ascending.
-1     |       Sort descending.

Example: 
```js
db.users.find({ }).sort( { age : -1, posts: 1 } )

// or 

db.restaurants.aggregate(
   [
     { $sort : { borough : 1, _id: 1 } }
   ]
)
```

# What is indexing in MongoDB? Why do we need to use indexing? What are pros and cons for indexing?
=> Indexes are special data structures that stores some information related to the documents such that it becomes easy for MongoDB to find the right data file. The indexes are order by the value of the field specified in the index.
```js
db.collection.createIndex( <key and index type specification>, <options> )

// Example:

db.collection.createIndex( { name: -1 } )

db.products.createIndex(
  { item: 1, quantity: -1 } ,
  { name: "query for inventory" }
)
```

Indexes support the efficient execution of queries in MongoDB. Without indexes, MongoDB must perform a collection scan, i.e. scan every document in a collection, to select those documents that match the query statement.

**Pros and cons of indexing:**
The biggest advantage of indexing is that it speeds up your find, update and delete queries. Quite naturally because it is easier to search for the elements based on the indexed field.

The disadvantages of indexing is that 1. It takes up memory (obviously). 2.It slows down write queries.
The write queries will obviously be slowed down because every time you make a write query you need to update the indexed field list in the collection as well and sort it again based on that field.

# Write the query for indexing a field in MongoDB?
=> 
```js
db.collection.createIndex( <key and index type specification>, <options> )

// or

db.collection.find( { } )

// Example:

db.collection.createIndex( { name: -1 } )

db.products.createIndex(
  { item: 1, quantity: -1 } ,
  { name: "query for inventory" }
)
```

# What is the improvement in performance in MongoDB?
=> More importantly, always remember that appropriate data modeling, indexing, embedding, and referencing are basic considerations. Assuming you know the query patterns of your application well, you’ll find that you can get solid performance and a lot of extra mileage out of the distributed and replicated nature of MongoDB.

If all else fails...did we mention that MongoDB Atlas also has a built-in Performance Advisor? It can make your life a whole lot easier if you’re not sure where to start.

# What is the data structure used for indexing?
=> B-trees are the most commonly used data structures for indexes as they are time-efficient for lookups, deletions, and insertions. All these operations can be done in logarithmic time. Data that is stored inside of a B-tree can be sorted. Indexes that use hash tables are generally referred to as hash index.

# Are values sorted in indexes?
=> When an index has a key with multiple data types, the index is sorted according to the BSON type sort order. If an index key contains an array, the document is sorted according to the type of the first array element.

# What are Replica Sets in MongoDB?
=> A replica set in MongoDB is a group of mongod processes that maintain the same data set. Replica sets provide redundancy and high availability, and are the basis for all production deployments. This section introduces replication in MongoDB as well as the components and architecture of replica sets.
<a href="https://www.mongodb.com/docs/manual/replication/#:~:text=A%20replica%20set%20in%20MongoDB,and%20architecture%20of%20replica%20sets.">Full Details</a>

# Explain the structure of ObjectID in MongoDB.
=> ObjectId(<value>)
Returns a new ObjectId. The 12-byte ObjectId consists of:
- A 4-byte timestamp, representing the ObjectId's creation, measured in seconds since the Unix epoch.
- A 5-byte random value generated once per process. This random value is unique to the machine and process.
- A 3-byte incrementing counter, initialized to a random value.

While the BSON format itself is little-endian, the timestamp and counter values are big-endian, the most significant bytes appear first in the byte sequence.

If an integer value is used to create an ObjectId, the integer replaces the timestamp.

ObjectId() can accept one of the following inputs:

hexadecimal: Optional. A 24 character hexadecimal string value for the new ObjectId.
integer: Optional. The integer value, in seconds, is added to the Unix epoch to create the new timestamp.

Example:
Generate a New ObjectId
To generate a new ObjectId, use ObjectId() with no argument:
```js
x = ObjectId()
```
In this example, the value of x is:
```js
ObjectId("507f1f77bcf86cd799439011")
```
```js
ObjectId("507f191e810c19729de860ea").str
// output
507f191e810c19729de860ea
```
Generate a new ObjectId using an integer.
```js
newObjectId = ObjectId(32)
```
The ObjectId resembles:
```js
ObjectId("00000020f51bb4362eee2a4d")
```
The first four bytes of the ObjectId are the number of seconds since the Unix epoch. In this example 32 seconds, represented in hexadecimal as 00000020, are added. A five byte random element and a three byte counter make up the rest of the ObjectId.

# By default, which index is created by MongoDB for every collection?
=> Default _id Index 
MongoDB creates a unique index on the _id field during the creation of a collection. The _id index prevents clients from inserting two documents with the same value for the _id field.

# In which format MongoDB represents document structure?
=> In MongoDB, data is stored as documents. These documents are stored in MongoDB in JSON (JavaScript Object Notation) format.

# What is the limitation of a document in MongoDB?
=> The maximum BSON document size is 16 megabytes. The maximum document size helps ensure that a single document cannot use excessive amount of RAM or, during transmission, excessive amount of bandwidth. To store documents larger than the maximum size, MongoDB provides the GridFS API.

# What is the difference between MongoDB and Redis database?
=> MongoDB is a document-oriented, disk-based database optimized for operational simplicity, schema-free design and very large data volumes. Redis is an in-memory, persistent data structure store that enables developers to perform common operations with minimal complexity and maximum performance.

MongoDB is written in C++, Go, JavaScript, Python languages. MongoDB offers high speed, high availability, and high scalability. Redis is written in ANSI and C languages. Redis offers memory efficiency, fast operating speed, high availability and provides some features like tunability, replication, clustering, etc.

# How can you add references between multiple collections?
=> MongoDB applications use one of two methods for relating documents:
- Manual references where you save the _id field of one document in another document as a reference. Your application runs a second query to return the related data. These references are simple and sufficient for most use cases.
Example:
```js
original_id = ObjectId()

db.places.insertOne({
    "_id": original_id,
    "name": "Broadway Center",
    "url": "bc.example.net"
})

db.people.insertOne({
    "name": "Erin",
    "places_id": original_id,
    "url":  "bc.example.net/Erin"
})
```
- DBRefs are references from one document to another using the value of the first document's _id field, collection name, and, optionally, its database name, as well as any other fields. DBRefs allow you to more easily reference documents stored in multiple collections or databases.
Example:
```js
{
  "_id" : ObjectId("5126bbf64aed4daf9e2ab771"),
  // .. application fields
  "creator" : {
                  "$ref" : "creators",
                  "$id" : ObjectId("5126bc054aed4daf9e2ab772"),
                  "$db" : "users",
                  "extraField" : "anything"
               }
}
```

# What are lookup in aggregation for MongoDB?
=> The $lookup operator is an aggregation operator or an aggregation stage, which is used to join a document from one collection to a document of another collection of the same database based on some queries. Both the collections should belong to the same databases.
Syntax:
```js
{
   $lookup:
     {
       from: <collection to join>,
       localField: <field from the input documents>,
       foreignField: <field from the documents of the "from" collection>,
       as: <output array field>
     }
}
```

# What are graph lookups?
=> MongoDB has added a new feature in its version 3.4 $graphLookup, Its is an extended version of $lookup and has enhanced capabilities which are used to perform a recursive search on a collection in an array with multiple values/fields.

$graphLookup. Performs a recursive search on a collection, with options for restricting the search by recursion depth and query filter. The $graphLookup search process is summarized below: Input documents flow into the $graphLookup stage of an aggregation operation.
Syntax:
```js
{
   $graphLookup: {
      from: <collection>,
      startWith: <expression>,
      connectFromField: <string>,
      connectToField: <string>,
      as: <string>,
      maxDepth: <number>,
      depthField: <string>,
      restrictSearchWithMatch: <document>
   }
}
```

# What is the alternative for lookups in MongoDB?
=> .populate()


# How can you do one to many relation in MongoDB?
=> In this one-to-many relationship between patron and address data, the patron has multiple address entities.
```js
// patron document
{
   _id: "joe",
   name: "Joe Bookreader"
}

// address documents
{
   patron_id: "joe", // reference to patron document
   street: "123 Fake Street",
   city: "Faketon",
   state: "MA",
   zip: "12345"
}

{
   patron_id: "joe",
   street: "1 Some Other Street",
   city: "Boston",
   state: "MA",
   zip: "12345"
}
```
If your application frequently retrieves the address data with the name information, then your application needs to issue multiple queries to resolve the references. A more optimal schema would be to embed the address data entities in the patron data, as in the following document:
```js
{
   "_id": "joe",
   "name": "Joe Bookreader",
   "addresses": [
                {
                  "street": "123 Fake Street",
                  "city": "Faketon",
                  "state": "MA",
                  "zip": "12345"
                },
                {
                  "street": "1 Some Other Street",
                  "city": "Boston",
                  "state": "MA",
                  "zip": "12345"
                }
              ]
 }
```

# How can you do many to many relation in MongoDB?
=>  I have modeled many-to-many relationships in relational databases using a junction table. A junction table is just the table that stores the keys from the two parent tables to form the relationship. See the example below, where there is a many-to-may relationship between the person table and the group table. The person_group table is the junction table.
Example:
```js
db.person.insert({
  "_id": ObjectId("4e54ed9f48dc5922c0094a43"),
  "firstName": "Joe",
  "lastName": "Mongo",
  "groups": [
    ObjectId("4e54ed9f48dc5922c0094a42"),
    ObjectId("4e54ed9f48dc5922c0094a41")
  ]
});

db.person.insert({
  "_id": ObjectId("4e54ed9f48dc5922c0094a40"),
  "firstName": "Sally",
  "lastName": "Mongo",
  "groups": [
    ObjectId("4e54ed9f48dc5922c0094a42")
  ]
});
```
This is how some group documents would look in mongoDB.
```js
db.groups.insert({
  "_id": ObjectId("4e54ed9f48dc5922c0094a42"),
  "groupName": "mongoDB User",
  "persons": [
    ObjectId("4e54ed9f48dc5922c0094a43"),
    ObjectId("4e54ed9f48dc5922c0094a40")
  ]
});

db.groups.insert({
  "_id": ObjectId("4e54ed9f48dc5922c0094a41"),
  "groupName": "mongoDB Administrator",
  "persons": [
    ObjectId("4e54ed9f48dc5922c0094a43")
  ]
});
```

# How can you do one to zillion relation in MongoDB?\
=> 
```js
//city
  {
  _id: 1,
  name: 'NYC',
  area: 30,
  people: [{
      _id: 1,
      name: 'name',
      gender: 'gender'
        .....
    },
    ....
    8 million people data inside this array
    ....
  ]
}
```