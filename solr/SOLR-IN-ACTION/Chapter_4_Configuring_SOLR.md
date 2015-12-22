
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
| shard | Sets the shard ID for this core; see chapters 12 and 13 for more information about sharding. | 
| collection | Name of the SOLRCloud collection this core belongs to. |
| loadOnStartup | If true, this core is loaded during the SOLR initialization process and a new searcher is opened for the core. 
|transient| Indicates that this core can be unloaded automatically transientCacheSize threshold is reached (advanced option) 

#### Overview of solrconfig.xml

The solrconfig.xml contains index-management settings. 

**Common XML data-structure and type elements**

| name | Description | example |
|------|-------------|---------|
| <arr> | Names, ordered array of objects | <arr name="last-components"> <str>spellcheck</ str> </ arr > |