Understanding the SOLR index
=============================

####Document

This is the maoin structure used both for searches and indexes. A document is an in-memory representation of the data values we need to use for our searches. In order for this to wrk, every docuemtn resource consits of a collection of fields, which is the most simple data structure. 

####Field

Thsi has its own name and value and consits of at least one term. So every docuemnt can be seen as niothing more than a list of very simple(field anem and term value)pairs. If a field is designed to be multi-valued, we can save as many values as wen want within the same key. Otherwise if we enter new values the last one will simply overwrite the previous. 

####Term

This is the basic unit for indexing. For simplicity let's imagine a single word, but the word can consist of a string of words, depending on a configuration details. 

####Index

This is the in-memory structure where Lucene(and solr) perform the searches. We can think about a docuemnt to be a single record in the index. From an abstrct logical point of view, we can easily imagine a data structure as shown in the following figure. 

