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

Each field must define a type attribute that identifies the \<fieldType> to use for that field. 

Each field must define is it is indexed or stored. 

Indexed fields can be searched and sorted upon and stored fields can be returned in search results for display purposes. 

There are no nested fields in SOLR. All fields are siblings in schema.xml

Document in SOLR need to be denormalized into a flat structure. 

#####Joins in SOLR

SOLR joins are like subqueries in SQL than joins. A typical use case is to find the parent documents of child documents that match your search criteria.  

#####Multivalued Fields

In SOLR, fields that can have more that one calue per document are called multivalued fields. 

```
<field name="link" type="string" indexed="true" stored="true" multiValued="true"/>
```

Adding a document with multiple values for one field example
```
<add>
<doc>
<field name="link">google.com</field>
<field name="link">bing.com</field>
</doc>
</add>
```

#####Dynamic Fields

In SOLR, dynamic fields allow you to apply the same definition to any fields in your documents whose names match either a prefix or suffix pattern, such as s_* or *_s 

Dynamic fields use a special naming scheme to apply the same definition to any field that match this kind of glob-style pattern. 

Dynamic fields help address common problems that occur when building search applications.

- Modeling documents with many fields
- Supporting documents from diverse sources
- Adding new document sources

Dynamic fields can be a handy feature on the indexing side, there no real magic on the query side. When querying for docuemnts that were indexed with dynamic fields, you must use the full field name in the query. 

you can not formulate queries to find a match in all string fields by quering with a prefix or suffix pattern. 

#####Copy Fields

If you want to find matches in more than one field, dynamic or static, SOLR provides a clever way to do that with copy fields. 

In SOLR, copy fields allow you to populate one field from one or more other fields. 

Copy fields support two use cases that are common in most search applications. 

- Populate a single catch-all field with contents of multiple fields. 
- Apply different text analysis to the same field content to create a new searchable field. 

The catch-all field shouldn't be stored as it's populated from another field. 

The Destination field must be multivalued if any source fields are multivalued. 

```
<field name="catch_all" type="text_en" indexed="true" stored="false" multiValued="true"/>
```

**Using the \<copyField> directive to populate the catch_all field**

```
<schema>
    <fields>
    <field name="catch_all" type="text_en" indexed="true" stored="false" multiValued="true"/>
    </fields>
    <copyField source="screen_name" dest="catch_all" />
    <copyField source="text" dest="catch_all" />
    <copyField source="link" dest="catch_all" />
    <types>
    </types>
</schema>
```

