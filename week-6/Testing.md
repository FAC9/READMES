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

Check out [redtape](https://github.com/eugeneware/redtape) for examples on how to use a tape like testing environment with before each and after each methods.

## Research and figure out how to use a mocking library.
## What are some advantages and disadvantages of mocking?
### Advantages of mocking
- using mock objects and data can be a good way to unit-test, but integration testing is needed to ensure that the system runs as a whole
- if the real database (db) runs very slowly, a mock test of the schema or whole may be preferable
- db can be big and complex; if you are testing whether additions to the db have worked you may unintentionally alter other data, which could be avoided if you use a mock db
- even if db is not that complex, you may have reasons not to want to add something as part of a test and then remove it later (eg if it could prejudice statistics or user behaviour), in which case a mock db could be a better option

### Disadvantages of mocking
- the copy has to be very carefully maintained so it doesn't get out of date with the production version of the data and schema, and this is complicated and time-consuming
- there are security and privacy implications to mock databases
- once the db gets big, taking a copy of it and putting it into your dev environment can be a big deal

## What exactly needs testing about the database?
- Test if any errors are shown while executing queries
- Data Integrity is maintained while creating, updating or deleting data in database
- Check response time of queries and fine tune them if necessary
- Test data retrieved from your database is shown accurately in your web application

  Find out more: http://www.guru99.com/web-application-testing.html
  
