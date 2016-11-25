## If not mocking the database, how do you ensure you don't fill your database with test insertions?
## Research and figure out how to use a mocking library.
## What are some advantages and disadvantages of mocking?
### Advantages of mocking
- using a mock database can be a good way to unit-test the business logic as any modules and data needed for the test can be faked, but it doesn't seem like anyone thinks mock databases are a good way to test the object relational mapping or the database iteslf.

### Disadvantages of mocking
- the copy has to be very carefully maintained so it doesn't get out of date with the production version of the data and schema, and this is complicated and time-consuming
- there are security and privacy implications to mock databases
- once the db gets big, taking a copy of it and putting it into your dev environment can be a big deal

## What exactly needs testing about the database?
