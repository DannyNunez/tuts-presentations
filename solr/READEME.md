Understanding Solr
===========================

- Apache solr was started at CNET in 2004 
- It was initially conceived to be a web application for providing a wide range of full-text search capabilities. 
  by using and extending the power of the well known Apache Lucene Library. 
- The two projects have been merged into a single development effort since 2010, with improved modularity.
- solr is designed to be a standalone web server.
	- exposing full-text and other functionalities via it;s own rest like services.

###What Solr is not

- Solr is not a database.
- It it designed to manage indexes of actual data and not the data itself or the relations between them. 

###What can you use Solr for? 

- data acquisitions
- language processing
- document clustering
- full text search
- auto suggestion
- advanced filtering
- geocoded search
- highlighting in text
- faceted search 

Aspects of Solr
================

- Advanced Full Text Search
- Suggestions
- Language Analysis
	- solr permits us to configure different types of lanugae analysis even on a per-field basis, with the posiibility to configure them specficall for a certain language. 
	- Intergrations with tools such as Apache UIMA for metadat extraction already exist. 
- Faceted Search: This is a particular type if search based on classification. With Solr, we can perform facated search automatically over our fields to gain information such as how many documents have the value London for the city field. This is useful to contruct some kind of navigation. This is another very familiar pattern in user experience that you probably know from having used it on a e-commerce site such as amazon. 
- It is easy to index data using use POST over HTTP
- Solr can index text and metadata over a collection of rich documents (Such as PDF, WORD or HTML) useing the [APACHE TIKA COMPONENT](http://tika.apache.org/).
- Solr can read data from a database or other external data sources, and configure an internal workflow to directly index them if needed using the [DataImportHandler](http://wiki.apache.org/solr/DataImportHandler)
- solr also exposes its own search services that are REST-Like on standard opne formats such as JSON or XML. 
	- The services are designed to be paginated, and to expose parameters for sorting and filtering results.
	- Other serilalization formats can be used which are designed for specific languages
		- PHP
		- Ruby
		- Java
- Third party integrations for existing application already exist
	- Drupal
	- Wordpress
	- Magento
	- Java API's 
	- Alfresco
	- Broadleaf

How to start Solr
=================
java -jar start.jar & 



What is solr.jar
=================
The solr.jar launcher is a small Java library that starts an embedded Jetty container to run the Solr application. By default, this application will be running on port 8983. 

- Jetty is a lightweight container that has been apdopted for distributing Solr for its simplicity and small memory footprint. 
- Solr is distributed as a standard Java Web Application WAR files are avlaible for running SOLR on Tomcat or JBOSS and others.