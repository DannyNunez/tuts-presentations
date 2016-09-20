
**Create a drop table list for all unnecessary databases**

```
SELECT CONCAT('DROP DATABASE ',schema_name,' ;') AS stmt
  FROM information_schema.schemata
 WHERE schema_name != 'information_schema'
 AND   schema_name != 'mysql'
 AND   schema_name != 'performance_schema'
 ORDER BY schema_name
```

**Create a drop table list for all database by prefix**

```
SELECT CONCAT('DROP DATABASE ',schema_name,' ;') AS stmt
  FROM information_schema.schemata
 WHERE schema_name LIKE 'database\_%' ESCAPE '\\'
 ORDER BY schema_name
```
