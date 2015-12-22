## Find or Query Data with Mongo Shell

**Overview**

You can use the find() method to issue a query to retrieve data from a collection in MongoDB. All queries in MongoDB have the scope of a single collection. 

Queries can return all documents in a collection or only the documents that match a specified filter or criteria. 
You can specify the filter or criteria in a document and pass as a parameter to the find() method.

The find() method returns query results in a cursor, which is iterable object that yields documents.

###Query for All Documents in a Collection

To return all documents in a collection, call the find() method without a criteria document. For example the following operation queries for all documents in the restaurants collection. 

```mongodb 
db.restaurants.find();
```

The result set contains all documents in the restaurants collection. 

###Specify Equality Conditions

The query condition for an equality match on a field has the following form:

```mongodb 
db.restaurants.find({<field1>: <value1>, <field2>: <value2>});
```

If the <field> is a top level field and not field in an embedded document or an array, you can either enclose the field name in quotes or omit the quotes. 

If the <field> is an embedded document or an array, use dot notation to access the field. With the dot notation, you must enclose the dotted name in quotes. 

**Dot Notation**

MongoDB uses the dot notation to access the elements of an array and to access the fields of an embedded document. 

To access an element of an array by the zero based index position, concatenate the array name with the dot (.) and the zero-based index position, and enclose in quotes. 

```MongoDB
'<array>.<index>'
```

###Query by a Top Level Field

The following operation finds documents whose borough field equals "Manhattan".

```
db.resturants.find({"borough":"Manhattan"});
```

###Query by a Field in an Embedded Document

To specify a condition on a field within an embedded document, use the dot notation. Dot notation requires quotes around the whole dotted field name. The following species an equality condition on the zip code field in the address embedded document.

**Exact Match on the Embedded Document**

To specify an equality match on the whole embedded document, use the query document { <field> : <value> } where <value> is the document to match. Equality matches on an embedded document requires an exact match of the specified <value>, including the field order. 

*In the following example, the query matches all documents where the value of the field producer is an embedded document that contains only the field company with the value 'ABC123' and the field address with the value '123 Street', in the exact order:*

```
db.inventory.find(
    {
      producer:
        {
          company: 'ABC123',
          address: '123 Street'
        }
    }
)
```

**Equality Match on Fields within an Embedded Document**

Use the dot notation to match by specific fields in an embedded document. Equality matches for a specific fields in an embedded document will select documents in the collection where the embedded document contains the specified fields with the specified values. The embedded document can contain additional fields.
 
In the following example, the query uses the dot notation to match all documents where the value of the field producer ian an embedded document that contains a field company with the value 'ABC123' and may contain other fields.  

```
db.inventory.find( { 'producer.company': 'ABC123' } )
```

