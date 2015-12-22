#Documents

A record in MongoDB is a document, which is a data structure composed of field and value pairs. MongoDB
documents are similar to JSON objects. MongoDB stores documents in BSON a binary representation of JSON The values of fields may include other documents, arrays, and arrays of documents. 


Most user-accessible data structures in MongoDB are documents, including

* All database records
* **Query selectors**, which define what records to select for read,update, and delete operations.
* **Update definitions**, which define what fields to modify during an update. 
* **Index specifications**, which define what fields to index.
* Data output by MongoDB for reporting can configuration, such as the output of the **serverStatus** and the **replica set configuration document**.


###Document Format


```json
{
   "_id" : ObjectId("54c955492b7c8eb21818bd09"),
   "address" : {
      "street" : "2 Avenue",
      "zipcode" : "10075",
      "building" : "1480",
      "coord" : [ -73.9557413, 40.7720266 ],
   },
   "borough" : "Manhattan",
   "cuisine" : "Italian",
   "grades" : [
      {
         "date" : ISODate("2014-10-01T00:00:00Z"),
         "grade" : "A",
         "score" : 11
      },
      {
         "date" : ISODate("2014-01-16T00:00:00Z"),
         "grade" : "B",
         "score" : 17
      }
   ],
   "name" : "Vella",
   "restaurant_id" : "41704620"
}
```

#Collections

MongoDB stores documents in collections. Collections are analogous to tables in relational databases. Unlike a table, however, a collection does not require its documents to have the same schema. 

In MongoDB, documents stored in a collection must have a unique **_id** field that acts as a primary key.

##MongoDB Shell

The Mongo shell is an interactive JavaScript interface to MongoDB and is a component of the MongoDB package. You can use the mongo shell to query and update data as well as perform administrative operations. 
 
## Inserting Documents

You can use the insert() method to add documents to a collection in MongoDB. If you attempt to add documents to collection that does not exist, MongoDB will create the collection for you. 


 

