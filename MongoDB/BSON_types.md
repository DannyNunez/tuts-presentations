BSON is a binary serialization format used to store documents and make remote procedure calls in MongoDB. the BSON specification is located at [http://bsonspec.org/](http://bsonspec.org/) . 

BSON supports the following data types as values in documents. Each data type has a corresponding number and string alias that can be used with the $type operator to query documents by BSON type. 

| Type  | Number | Alia | Notes
| ----- | ------------------ |
| Double | 1 | "double" |
| String | 2 | "string" |
| Object | 3 | "object" |
| Array  | 4 | "array" |
| Binary data  | 5 | "binData" | 
| Undefined  | 6 | "undefined" | Deprecated
| Object id  | 7 | "objectId" | 
| Boolean  | 8 | "bool" | 
| Date  | 9 | "date" | 
| Null  | 10 | "null" | 
| Regular Expression | 11 | "regex" |
| DBPointer | 12 | "dbPointer" |
| JavaScript | 13 | "javascript" | 
| Symbol | 14 | "symbol" |
| JavaScript(with scope)| 15 | "javascriptWithScope" | 
| 32-bit integer | 16 | "int" |   

