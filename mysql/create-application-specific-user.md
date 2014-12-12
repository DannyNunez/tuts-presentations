1. Login into mysql as root
```
mysql -u root -p
```
2. Create a new user. 
```
mysql> CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)
```
3. Create a new database.
```
mysql> create database databasename;
Query OK, 1 row affected (0.00 sec)
```
4. Grant Full Privilege on the new database to the user you ject created. 
```
mysql> GRANT ALL ON databasename.* TO 'newuser'@'localhost';
Query OK, 0 rows affected (0.00 sec)
```
5. Flush Privileges 
```
mysql> FLUSH PRIVILEGES; 
Query OK, 0 rows affected (0.00 sec)
```