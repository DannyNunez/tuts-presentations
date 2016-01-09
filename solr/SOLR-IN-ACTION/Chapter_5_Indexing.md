Goals of Chapter 5

- Designing your schema for indexing documents
- Defining fields and fields types in schema.xml 
- Using Field types for structured data
- Handling update requests, commits and automatic updates. 
- Managing index settings in solrconfig.xml

Each document in a SOLR index is made up of fields, and each field has a specific type that determines how it 's stored, searched and analyzed. 

You should only index fields that will be searched by users. 

 Overview of the SOLR indexing process
 
 1 Convert a Document from its native format in a format supported by SOLR such as JSON and XML. 
 2 Add the document to SOLR using one of several well-defined interfaces, typically HTTP POST.
 3 Configure SOLR to apply transformations to the text in the document during indexing. 
 
 
####SCHEMA.XML

The schema.xml defines the fields and fields types for your documents. For the simple applications , the fields to search and their types may be obvious. In general, though, it helps to do some up-front planning about your schema. 


####Key Design considerations

- What is a document in your index? 
- How is each document uniquely identified?
- What fields in your documents can be searched by users?
- Which fields should be displayed to users in the search results?

#####Unique Key

SOLR doesn't require a unique identifier, but if one is supplied, SOLR uses it to avoid duplicating documents in your index. 

#####Indexed Fields

Determine the indexed fields by selecting fields that users of the search engine would miss if they would not included in the search option filters. 

In addition to enabling searching, you will also need to mark your field as indexed in you need to sort, facet, group by, provide query suggestions for , or execute function queries on values within a fields. 

#####Stored Fields

Sorted Fields are fields that are not indexed but are useful for display purposes. 

#####XML Elements

- The \<fields> element , containing \<field> and \<dynamicField> elements used to define the basic structure of your documents

- Miscellaneous elements, such as \<uniqueKey> and \<copyField>, which are listed after the \<fields> element

- Field types under the \<types> element that determins how dates, numbers and text fields are handled in solr

#####Defining Fields in schema.xml 

The \<fields> section in the schema.xml defines the \<field> elements for all fields in your document. 

SOLR uses the field definitions from the schema.xml file to figure out what kind of analysis needs to be inverted search index.

#####Required field Attributes

Each field has a unique name that's used when constructing queries. 

```
<field name="screen_name" type="string" indexed="true" stored="true"/>
```

