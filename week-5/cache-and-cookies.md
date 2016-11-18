# Cache and cookies


## Databases

### what is a database?

A database is a collection of information that is organized so that it can easily be accessed, managed, and updated.

## Web SQL

### SQL
- SQL is a standard language for accessing databases.
- SQL stands for Structured Query Language
- SQL lets you access and manipulate databases

#### Using SQL in Your Web Site
To build a web site that shows data from a database, you will need:

- An RDBMS database program (i.e. MS Access, SQL Server, MySQL)
- To use a server-side scripting language, like PHP or ASP
- To use SQL to get the data you want
- To use HTML / CSS

#### RDBMS
RDBMS stands for Relational Database Management System.

RDBMS is the basis for SQL, and for all modern database systems such as MS SQL Server, IBM DB2, Oracle, MySQL, and Microsoft Access.

The data in RDBMS is stored in database objects called tables.

A table is a collection of related data entries and it consists of columns and rows.

### Web SQL

The Web SQL Database specification is no longer being maintained and support may be dropped in future versions.

### SQL important commands
- SELECT - extracts data from a database
  The SELECT statement is used to select data from a database.
  SELECT column_name,column_name
  FROM table_name;
  OR
  SELECT * FROM table_name;
- UPDATE - updates data in a database
  UPDATE table_name
  SET column1=value1,column2=value2,...
  WHERE some_column=some_value;
- DELETE - deletes data from a database
  DELETE FROM table_name
  WHERE some_column=some_value;
- INSERT INTO - inserts new data into a database
  SELECT * FROM Users WHERE UserId = 105 or 1=1
- CREATE DATABASE - creates a new database
  CREATE DATABASE dbname;
- CREATE TABLE - creates a new table
  CREATE TABLE table_name
  (
  column_name1 data_type(size),
  column_name2 data_type(size),
  column_name3 data_type(size),
  ....
  );
- DROP TABLE - deletes a table
  DROP TABLE table_name
- CREATE INDEX - creates an index (search key), Creates an index on a table. Duplicate values are  allowed:
  CREATE INDEX index_name
  ON table_name (column_name)
  OR in order to create a unique index
  CREATE UNIQUE INDEX index_name
  ON table_name (column_name)
- DROP INDEX - deletes an index
  DROP INDEX index_name ON table_name

##### Structure of a query:
SELECT [ALL | DISTINCT] {[table.]* | expr [alias], exp [alias], }
FROM table [alias], table [alias],
[WHERE condition]
[GROUP BY expr, expr, [HAVING condition]]
[{INTERSECT | EXCEPT | UNION | UNION ALL } SELECT ]
[ORDER BY expr [ASC | DESC ], expr [ASC | DESC], ];

#### Example
``` JavaScript
if (window.openDatabase) {
    //Create the database the parameters are 1. the database name 2.version number 3. a description 4. the size of the database (in bytes) 1024 x 1024 = 1MB
    var mydb = openDatabase("cars_db", "0.1", "A Database of Cars I Like", 1024 * 1024);

    //create the cars table using SQL for the database using a transaction
    mydb.transaction(function (t) {
        t.executeSql("CREATE TABLE IF NOT EXISTS cars (id INTEGER PRIMARY KEY ASC, make TEXT, model TEXT)");
    });

} else {
    alert("WebSQL is not supported by your browser!");
}
```

## IndexedDB

#### Intro
IndexedDB is a transactional database system, like an SQL-based RDBMS. However, unlike SQL-based RDBMSes, which use fixed-column tables, IndexedDB is a JavaScript-based object-oriented database. IndexedDB lets you store and retrieve objects that are indexed with a key; any objects supported by the structured clone algorithm can be stored. You need to specify the database schema, open a connection to your database, and then retrieve and update data within a series of transactions.

#### Basic IndexedDB Pattern
- Open a database.
- Create an object store in the database.
- Start a transaction and make a request to do some database operation, like adding or retrieving data.
- Wait for the operation to complete by listening to the right kind of DOM event.
- Do something with the results (which can be found on the request object).

##### Open a database

``` JavaScript
  // Let us open our database
  var request = window.indexedDB.open("MyTestDatabase", 3);
```
 The call to the open() function returns an IDBOpenDBRequest object with a result (success) or error value that you handle as an event.
 The first parameter is the name of the database.
 The second parameter is version optional. The version to open the database with.
 If the version is not provided and the database does not exist, then it will be created with version 1.

##### Generating handlers
``` JavaScript
  request.onerror = function(event) {
    // Do something with request.errorCode!
  };
  request.onsuccess = function(event) {
    // Do something with request.result!
  };
```
