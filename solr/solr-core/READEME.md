Solr Core
===========================

Solr exposes various components as services, in order to provide a different kind of functionality. These components are managed with the **RequestHandler** components. 

####Query Handler 

This is a standard handler implicitl;y mapped on the paht /select unless we decide to explicitly use another name. We have already seen this handler in action. 

####Update Handler 

This is explicitly mapped to the path /update. This is used to receive new data to indexed. The data to be indexed in Solr are generally called documents and it's important to distinguish them from the original data we want to search over. A Solr docuemtn is indeed a flat, unstructed sequence of the indexed metadata we want to use to represent a specific resource in our search domain. 

####Admin Handler

This is explicitly mapped to the path /admin. This is essential for using the admin web interface and having access to statistics, debug, and so on. Somewhat related to this definition is the definition of the default query to use the admin interface. 



schema.xml
==========================

####Types

This is used for defining a list of different data types for values. We can define strings, numeric types, or new types as we like. It's very common to have two or three different data types for handling text values shaped for different purposes, but for the moment we need to focus on the main concepts. 

####Fields

Theese are an essential part of this file. every field should declare a unique name and associate it with one of the types defined previously. It is important to understand that not every instance of a SOLR document must have a value for every field when mandatory a field can be marked as required. This approach is very flexible. We only index the actual data values without introducing dummy empty fields. 

####copyfield:

This is used when the content of a source field needs to be added and indexed on some other destination field (usually as a melting pot for very general searches) The idea behind it is that we want to be able to search in all the fields of a document at the same time (The source will be defined byu the wildcard *) . The Most simple way to do this is by copying the values into a default field where we will perform the actual searches. this field will also have its own type and analysis defined. 

####dynamicfield

By using this type we can start indexing some data without having to define the name of the field. The name will be defined by the wildcard and it's possible to use prefixes. and postfixes so that the actual name of a field is accepted at the runtime, while the type should be defined. For examplewhen writing <dynamicField name='*_s' type='string' />  We can post new documents containing string values such as firstName_s='Alfredo' and surname_s='Serafini'. This is an ideal case for prototypes, as wecan work with the Solr APi without defining a final schema  for our data. 

####uniqueKey: 

this is used to give a unquie identity to a specific SOLR docuemnt. It is a concept similar to a primary key for a DBMS. 

####defaultSearchField: 

This field is used when there is no request for a specific field. the best configuration for this is generally the field containing all the full-text tokens. 

####defaultOperator

- This is used to choose a default behavior when handling multiple tokens in the search. 
- A query that uses "and" between the various words used for a search is intuitively narrowed to a small set of docuemnts. 
- In most cases you will use the "or" Operator instead. It is less restrictive and more natural for commom queires. 
- The "and" approach is generally usefull, for example, when working with navigation filters or conductiing and advanced search on large datasets. 

Field Attributes
================


####MultiValued

If the value of this attribute is true, a solr Document can contain more than one instance of value for the field. The default value is false. 

####indexed: 

If it is true, the field is used in index. Generally we will use only indexed fields, but it can be interesting to have them not idexed in certain instances for exampole, if we want to save a value without it searches. 

####stored

This is used to permeanently save the original data value for a field, whether indexed or not. Moreover during the indexing pahse, a field is analyzed as defined by its type in the schema.xml  file to update the index; however, it it not explicitly saved unless we decide to store it. 








































