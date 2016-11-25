# Importing, exporting and migrating databases

## How to import databases from an existing project

## How to export databases

## Migrations in Postgres

### Things to consider

- You have a live site with live users, and ideally you want to avoid downtime
- User data is very sensitive and not to be messed with

## Resources

- Put links here

This [post on StackOverflow](http://dba.stackexchange.com/questions/10913/best-practices-for-schema-changes-and-data-migrations-to-a-live-database-without) talks about how to minimize impact of database migrations and is fairly easy to understand:





Emily links
http://blog.honeybadger.io/zero-downtime-migrations-of-large-databases-using-rails-postgres-and-redis/

https://github.com/theoephraim/node-pg-migrate

https://devcenter.heroku.com/articles/heroku-postgres-import-export

https://kostasbariotis.com/data-migration-with-nodejs/ <<== best one so far!

https://www.wlaurance.com/2014/04/Using-PostgreSQL-and-Node/ <<== also seems nice

http://dba.stackexchange.com/questions/10913/best-practices-for-schema-changes-and-data-migrations-to-a-live-database-without

- https://www.postgresql.org/docs/9.1/static/backup-dump.html
- https://www.postgresql.org/docs/8.1/static/app-pgdump.html
