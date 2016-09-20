### Documents, Fields and Schema DEsign 

#### Solr Field Types

The field type defines how SOLR should 
interpret data in a field and how the fields can be queried. 
There are many field types included with SOLR by default, 
and they can also be defined locally. 

#### Field Type Definitions and Properties

A Field type definition can include four types of information: 

* The Name of the field Type (mandatory)
* An implementation class name (mandatory)
* If the Field type is TextField, a description of the 
field analysis for the field type.
* Field type properties - depending on the implementation class, 
some properties may be mandatory.

#### Field Type Definitions in schema.xml 

Field types are defined in schema.xml. Each field type is defined between fieldType
elements. They can optionally be grouped with a type element. Here is an example of
a field type definition for a type called text_general. 

```xml 
<fieldType name="text_general" class="solr.TextField" positionIncrementGap="100">
  <analyzer type="index">
    <tokenizer class="solr.StandardTokenizerFactory"/>
    <filter class="solr.StopFilterFactory" ignoreCase="true" words="stopwords.txt"
/>
    <!-- in this example, we will only use synonyms at query time
    <filter class="solr.SynonymFilterFactory" synonyms="index_synonyms.txt"
ignoreCase="true" expand="false"/>
-->
    <filter class="solr.LowerCaseFilterFactory"/>
  </analyzer>
  <analyzer type="query">
    <tokenizer class="solr.StandardTokenizerFactory"/>
    <filter class="solr.StopFilterFactory" ignoreCase="true" words="stopwords.txt"
/>
    <filter class="solr.SynonymFilterFactory" synonyms="synonyms.txt"
ignoreCase="true" expand="true"/>
    <filter class="solr.LowerCaseFilterFactory"/>
  </analyzer>
</fieldType>
```

The First line in the example above contains the field type name, 
text_general and the name of the implementing class, solr.TextField. 
The rest of the definition is about field analysis, described in Understanding
Analyzers, Tokenizers, and Filters. 

The implementing class is responsible for making sure the field is handled correctly.
In the class names in schema.xml, the string solr is shorthand for org.solr.schema

### Filed Type Properties

The field type class determines most of the behavior of a field type, 
but options properties can also be defined. For example the following 
definition of a date field type defines two properties, sortMissingLast
and omitNorms. 

```xml
<fieldType name="date" class="solr.TrieDateField"
           sortMissingLast="true" omitNorms="true"/>
```

The properties that can be specified for a given field type fall into 
three major categories: 

* Properties specific to the field type's class.
* General Properties SOLR supports for any field type.
* Field Default Properties that can be specified on the field type that will be 
inherited by fields that use this type instead of the default behavior. 

General Properties

**name** - The name of the fieldType. This value gets used in field definitions,
in the "Type" attribute. It is strongly recommended 
