# Caching and cookies

See our demo project on COOKIES README [here](https://github.com/limeyb7/cookies-with-hapi-demo/tree/master).

## Client-side storage
>>>>>>> master

### Client-side storage is a minefield

Handling client-side storage well is fundamental to developing performant web apps - especially for developing progressive web apps, which rely heavily on client-side storage to function.

- Cookies: Cookies are supported by virtually every browser in circulation, and are suitable for handling session management, personalisation and tracking. They were never designed to handle general purpose client-side storage, but were often used for this purpose in the absence of any widely supported alternative. Cookies have mostly been superseded for client-side storage by other APIs (see below).
- Web Storage API: The Web Storage API  It is defined in the HTML5 standard, so should be supported by all modern browsers (although legacy browser support is patchy).
- IndexedDB: A JSON-based database API with similar functionality to NoSQL databases. It isn't part of the HTML5 standard, but it *is* recommended by W3C (the World Wide Web Consortium). It is fully supported by all modern browsers except Internet Explorer and Edge, and is partly supported by both of those.
- WebSQL: WebSQL was an attempt to incorporate SQL-style database functionality into the browser, but it was never recommended by W3C and its specification was abandoned in 2010 after Mozilla refused to support it in Firefox.

### Local storage and session storage

localStorage and sessionStorage are both browser APIs for storing data on the client side. They were introduced in the HTML5 specification and are supported by all modern browsers (although support in older browsers is patchy).

The two APIs are almost identical in their interfaces and functionality. The key difference is that sessionStorage is intended to store data for the duration of a single browser session, while localStorage is intended to store data that persists between sessions.

To put it simply, data stored through sessionStorage should be deleted when the browser window is closed. Data stored through localStorage shouldn't.

Both sessionStorage and localStorage are instances of the Storage object, one of the interfaces of the Web Storage API - a relatively recent API which provides browsers with mechanisms for storing key/value pairs.

The Web Storage API can be used in similar situations to HTTP session cookies, but offers several advantages. Unlike cookies, for example, sessionStorage is scoped to an individual window - so different windows can maintain separate state without changes in one 'leaking' into the other.

The API can also be used to store large files to improve website performance. When accessing large files and documents stored on the cloud, for example, copies may be saved in localStorage to improve load times after the initial transfer.

#### When to use sessionStorage

sessionStorage creates a storage area for each origin (normally a web domain) accessed by the browser, which persists until the end of the page session.

It should be used when you need to store data on the client side temporarily. Each browser window creates its own sessionStorage instance, which is cleared when the window is closed.

#### When to use localStorage

localStorage creates a separate storage area for each origin accessed by the browser, which persists until it is explicitly deleted by the user.

It should be used when data needs to be stored between sessions or for the long term, such as recording user preferences about how your website is displayed.

#### Inspecting sessionStorage and localStorage

You can inspect your browser's sessionStorage and localStorage for a domain by opening Chrome's Developer Tools and selecting the Application tab.

#### Using the Web Storage API

The Storage object has the following methods, which can be used on either window.localStorage or window.sessionStorage:

- Storage.key(): takes an integer as an argument, and returns the key with that index
- Storage.getItem(): takes a key name as a string, and returns that key's value
- Storage.setItem(): takes a key name and a value and adds that key to storage or, if it already exists, update its value
- Storage.removeItem(): takes a key name as a string and remove that key from storage
- Storage.clear(): removes all keys from storage (takes no arguments)

## Browser database APIs

#### what is a database?

A database is a collection of information that is organized so that it can easily be accessed, managed, and updated.

### Web SQL

#### SQL
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

#### Web SQL

The Web SQL Database specification is no longer being maintained and support may be dropped in future versions.

#### SQL important commands
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

#### Structure of a query:
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

### IndexedDB

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
