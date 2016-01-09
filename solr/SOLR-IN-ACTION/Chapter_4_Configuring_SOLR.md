
Most configuration of SOLR focuses around three main XML files. 

- solr.xml - Defines properties related to administration, logging, sharding, and SolrCloud
- solrconfig.xml - Defines the main settings for a specific SOLR core
- schema.xml - Defines the structure of your index, including fields and field types


#### Core Properties Parameters 

| name | Description |
|------|-------------|
| name | Names the core; required. |
| config | Specifies the name of the configuration file; defaults to solrconfig.xml. |
| dataDir | Specifies the path to a directory containing the index files and update log (tlog); defaults to data under the instance directory. |
| ulogDir | Specifies the path to a directory containing the update log (tlog) |
| schema | Sets the name of the schema document; defaults to schema.xml |
| shard | Sets the shard ID for this core | 
| collection | Name of the SOLRCloud collection this core belongs to. |
| loadOnStartup | If true, this core is loaded during the SOLR initialization process and a new searcher is opened for the core. 
|transient| Indicates that this core can be unloaded automatically transientCacheSize threshold is reached (advanced option) 

#### Overview of solrconfig.xml

The solrconfig.xml contains index-management settings. 

**Common XML data-structure and type elements**

| name | Description | example |
|------|-------------|---------|
| arr  | Names, ordered array of objects | <arr name="last-components"> <str>spellcheck</ str> </ arr > |
| lst  | Named , ordered list of name/value pairs | <lst name="defaults"><str name="omit Header"> true</ str > <str name="wt">json</str></lst> |
| bool | Boolean value-true or false | <bool>true</bool> |
| str  | String value | <str>spellcheck</str> or <str name="wt">json</str> |
| int  | Integer value| <int>512</int>|
| long | long value| <long>123123213213123123</long>|
| float | float value| <float>3.14</float>|
| double | Double value| <double>3.14</double>|


####luceneMatchVersion

SOLR uses the *luceneMatchVersion* to understand which version your index is based on and whether to disable Lucence features that depend on a later version than what is specified. 

```xml
<luceneMatchVersion>4.7</ luceneMatchVersion>
```

####Loading dependency JAR files using the <lib> element 

The lib element allows you to add JAR files to SOLR's runtime classpath so that it can located plugin classes. 

```xml
<lib dir="../../../contrib/langid/lib/" regex=".*\.jar" />
<lib dir="../../../dist/" regex="solr-langid-\d.*\.jar" />
```
- Each <lib> element identifies a directory and a regular expression to match files in the directory. 
- The dir attribute uses relative paths, which are evaluated from the core directory root, commonly referred to as the core instanceDir. 

####JMX

The *jmx* element activates SOLR's MBeans to allow ystem administrators to monitor and manage core SOLR components from popular tools, such as Nagios. 

####Request-handling Overview

Requests to SOLR happen over HTTP. 

If you want to query SOLR, then you send an HTTP GET request. 

If you want to index a document in solr, you use an HTTP Post request. 

####Request Parameter Decoration

- **defaults** - Set default parameters on the request if they are not explicitly provided by the client. 

- **invariants** - Set parameters to fixed values, which override values provided by the client

- **appends** - Additional parameters to be combined with the parameters provided by the client
 
- **first-components** - an optional chain of search components that are executed first to perform pre-processing tasks. 

- **components** - The primary chain of search copmponents that must at least include the query component

- **last-components** - An optional chain of search components that are applied last to perform post-processing tasks. 





