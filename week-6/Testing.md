## If not mocking the database, how do you ensure you don't fill your database with test insertions?
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


## Resources
- [An overview of database testing](http://www.softwaretestinghelp.com/database-testing-process/)
- [Strategies for unit-testing database-driven applications](http://stackoverflow.com/questions/145131/whats-the-best-strategy-for-unit-testing-database-driven-applications)
- [Testing: when to connect the database](http://softwareengineering.stackexchange.com/questions/206539/unit-tests-and-databases-at-which-point-do-i-actually-connect-to-the-database)
- [Wikipedia entry on mock objects](https://en.wikipedia.org/wiki/Mock_object)
- [Martin Fowler on classical testing vs mocking](http://martinfowler.com/articles/mocksArentStubs.html)
- [Node Postgres Test](https://www.npmjs.com/package/pgtest)
