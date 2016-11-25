## If not mocking the database, how do you ensure you don't fill your database with test insertions?

To test a real database, you need a way to create a test table at the start of each test, then test your database calls, and finally drop your table after each test.

If you want to work with similar table data in your tests, you can use SQLs VIEW method:
```sql
CREATE VIEW my_view AS
SELECT column_name(s)
FROM original_table
WHERE condition
```
Views act like temporary tables in memory. You can perform the same actions as you would a real table. After working with your view table, you can drop it...
```sql
DROP VIEW my_view
```

Otherwise, you can simply create a table in the same way, and drop it after testing.

To integrate this approach in a real testing framework, you would perform the following tasks-
1. (Before Test) Create test database from desired testing table.
2. Perform actions (e.g add/delete/modify data).
3. Use SELECT queries on this test table, and asserts to test that data is manipulated.
4. (After Test) Drop test table.

Many testing frameworks allow beforeEach and AfterEach as a testing method, so steps **1** and **4** would be performed before and after each test.

We all love Tape, but does it have before each and after each methods? No.
But [redtape](https://www.npmjs.com/package/redtape) does. It is built on tape testing framework, so essentially you can perform the following;

```javascript
var redtape = require('redtape'),
    fs = require('fs');

var test = redtape({
  beforeEach: function (cb) {
    // CREATE VIRTUAL TABLE
  },
  // DO SOME TABLE STUFF. TEST IT
  afterEach: function (cb) {
    // DROP VIRTUAL TABLE
  }
});
```

## Research and figure out how to use a mocking library.
## What are some advantages and disadvantages of mocking?
## What exactly needs testing about the database?
