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

This is used when the content of a source field needs to be added and indexed on some other destination field (usually as a melting pot for very general searches) The idea behind it is that we want to be able to search in all the fields of a document at the same time (The source will be defined byu the wildcard *) the 