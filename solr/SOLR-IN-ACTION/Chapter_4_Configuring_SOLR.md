
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