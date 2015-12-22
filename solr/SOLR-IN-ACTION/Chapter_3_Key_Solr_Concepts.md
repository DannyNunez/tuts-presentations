
## Terms , Phrases, and Boolean Logic

**Required Terms**

There are two identical ways to write this query using the default query parser in SOLR.

- +new+house
- new AND house

the + symbol is a unary operator that means that the part of the query immediately following it is required to exist in any documents matched. 

The **AND** keyword is a binary operator that means that the part of the query immediately preceding and the part of the query immediately following it are both required. 


**Optional Terms** 

In contrast to the **AND** operator, Solr also supports the OR binary operator, which means that either the part of the query preceding or the part of the query following it is required to exits in any documents matched. By default, Solr is also configured to treat any part of the query without explicit operator as an optional parameter, making the following identical. 

- new house 
- new OR house

**Negated Term**

In addition to making parts of a query optional or required, it is also required, it is also possible to require that they not exist in any matched documents through either of the following equivalent queries. 

- new house -rental
- new house NOT rental

**Solr's default operator**

While the default configuration in SOLR  assumes that a term or phrase by itself is an optional term, this is a configurable on a per query basis using the q.op URL parameter with many of SOLR's query handlers. 

- /select/?q=new house&q.op=OR **versus** /select?q=new house&q.op=AND

Note that if you change the default operator from **OR** to **AND**,  this will switch to requiring all terms specified without an explicit Boolean operator. 

**Phrases**

Solr does not only support searching single terms; it can also search for phrases, ensuring that multiple terms appear together in order; 

- "new home" OR "new house"
- "3 bedrooms" AND "walk in closet" AND "granite countertops"

**Grouped Expressions**

In addtion to the preceding query expressions, one final basic Boolean construct that SOLR supports is the grouping of terms, phrases and other query expressions. The Solr query syntax can represent arbitrarly complex queries through grouping terms using parentheses and in the following examples. 

- New AND(house OR (home NOT improvement NOT depot NOT grown))
- (+(buying purchasing -renting) +(home house residence –(+property -bedroom)))

**Fuzzy Matching**

Fuzzy matching is defined as the ability to perform inexact matches on terms in the search index.

**Wildcard Searching**

One of the most common forms of fuzzy matching in SOLR is the use of wildcards. Suppose you want to find any documents that start with the letters **offic**. One way to do this is to create a query that enumerates all of the possible variations. 
 
 Because all of the variations you could match already exist in the solr index, you can use the asterisk(*) wildcard character to perform wildcard searches. 
 
 - Query: offi* Matches office, officer, official, and so on 
 
 In addtion to matching the end of a term, a wildcard character can be used inside of the search term as well, such as if you wanted to match both officer and offer: 
 
 - Query: off*r Matches offer, officer, officiator, and so on 
 
 The asterisk wildcard(*) matches zero or more characters in a term. If you want to match only a single character, you can make use of the question mark(?) for this purpose:
 
 - Query:off?r Matches offer, but not officer
 
**Range Searching**

Solr provide the ability to search for terms that fall between known values, this can be useful when you want to search for a particular subset of document falling within a range. For example, if you only wanted to match documents created in sux months between FE 2, 2012 and Augusr 2, 2012 you could perform the following search. 

- Query: created:[2012-02-01T00:00.0Z TO 2012-08-02T00:00.0Z]

**Proximity Searching**

- Query: "chief officer" ~1
  - Meaning: child and officer must be a maximum of one position away
  - Examples: "chief executive officer" , "chief financial officer"
- Query: "chief officer"~2
  - Meaning: chief and officer must be a maximum of two edit distances away. o Examples: "chief business development officer", "officer chief"
- Query: "chief officer"~N
  - Meaning: Finds chief within N positions of officer.
  
**Term Frequency**

Term frequency (tf) is a measure of how often a particular term appears in a matching document, and ot's am indication of how well a document matches the term. 

**Inverse document Frequency** 

Inverse document frequency (idf), a measure of how ***rare*** a search term is, is calculated by finding the document frequency ( how may total documents the search term appears within ).

Term frequency and inverse document frequency, when multiplied together in the relevancy calculation, provide a nice counterbalance. The term frequency elevates terms that appear multiple times within a document, whereas the inverse document frequency penalizes those terms that appear commonly across many documents. Therefore, common words in the English language such as the, an, and of ultimately yield low scores, even though they may appear many times in any given document.
 
**Boosting**

It is not necessary to leave all aspects of your relevancy calculations up to Solr. If you have domain knowledge about your content—you know that certain fields or terms are more (or less) important than others—you can supply boosts at either indexing time or query time to ensure that the weights of those fields or terms are adjusted accordingly.

Query-time boosting, the most flexible and easiest to understand form of boosting, uses the following syntax:

 - Query: title:(solr in action)^2.5 description:(solr in action)
 
This example provides a boost of 2.5 to the search phrase in the title field, while providing the default boost of 1.0 to the description field. Unless otherwise specified, all terms receive a default boost of 1.0 (which means multiplying the calculated score by 1, or leaving it as originally calculated). 

Query boosts can also be used to penalize certian terms if a boost of less than 1.0 is used:

- Query: title:(solr in action) description:(solr in action)^0.2

Query time boosts can be applied to any part of the query: 

- Query: title:(solr^2 in^.01 action^1.5)^3 OR "solr in action"^2.5


###Normalization Factors###

The default SOLR relevancy formula calculates three kinds of normalization(norms): field norms, query norms, and the coordinates factor. 

The field normalization factor (field norm) is a combination of factors describing the importanct of a particular field on a per-document basis. Field norms are calculated at index time and are more represented as an additional byte per field in the SOLR index. This byte packs a lot of information:

- The boost se on the document when indexed
- The boost set on the field when indexed
- The length normalization factor that penalizes longer documents and helps short documents.

####The Coord Factor####

One final normalization factor taking into account in the default SOLR relevancy calculation is the coord factor. its role is to measure how much of the query each document matches. 


####PRecision and Recall####

The information retrieval concepts of Precision (a measure of accuracy) and Recall (a measure of thoroughness) are simple to explain, but are also important to understand when building any search application or understanding why the results being returned are not meeting your business requirements. We’ll provide a brief summary here of each of these key concepts.

**Precision**
The precision of a search result set is a measurement attempting to answer the question, “Were the documents that came back the ones I was looking for?"