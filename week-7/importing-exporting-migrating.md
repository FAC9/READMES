# Importing, exporting and migrating databases

## How to import databases from an existing project

## How to export databases

## Migrations in Postgres

### Things to consider

- You have a live site with live users, and ideally you want to avoid downtime
- User data is very sensitive and not to be messed with


### Example: cat lovers database

In our example, we have a really basic database with just one table. It stores a list of cat lovers and the names of their cats. This works OK for the organisation updating the cat lovers database for a few years, until some of the members start adopting new cats. The single-table database structure just isn't sufficient any more.

It's time to scale.

See below a visual representation of the cat lovers table, and then the schema for the new database:

![image-1](./images/Database_schema1.png)

Getting from catLovers database 1.0 to the proposed version would include a few steps. And of course it's important that none of the users' data goes missing or gets changed in the process.

We might do something like this:

- Create a new "cats" table with all the required columns. The original database table stays as it is.
- From this point on, when new members join the cat lovers club, their data is only recorded in the new format
- But wait! Now we have two different data structures, so it's hard to keep track of which cats already exist. We need to copy data from the first database table to the new "cats" table.

We'll write some SQL for that:

```
INSERT INTO cats (name, color, catLoverId) VALUES
  SELECT cat_name, cat_color, id FROM catLovers
```
- Now all your data is in one place, but you've got some extra columns left in your cat_lovers table which you don't really need any more. In practice, these columns aren't causing you any problems, so you might want to leave them in place for an interim period so that you can be 500% sure that none of your data has been lost in migration.
- Later on, we might want to delete the old data for good. After all, some of those cats might have changed color by now. We can do this with SQL:

```
ALTER TABLE cat_lovers
  DROP COLUMN (cat_name, cat_color)
```

- Our lovely two-columned database now looks more like this:

![image_2](./images/Database_schema2.png)






## Resources

- Put links here

This [post on StackOverflow](http://dba.stackexchange.com/questions/10913/best-practices-for-schema-changes-and-data-migrations-to-a-live-database-without) talks about how to minimize impact of database migrations and is fairly easy to understand:

Emily links
- http://blog.honeybadger.io/zero-downtime-migrations-of-large-databases-using-rails-postgres-and-redis/
- https://github.com/theoephraim/node-pg-migrate
- https://devcenter.heroku.com/articles/heroku-postgres-import-export
- https://kostasbariotis.com/data-migration-with-nodejs/ <<== best one so far!
- https://www.wlaurance.com/2014/04/Using-PostgreSQL-and-Node/ <<== also seems nice
- http://dba.stackexchange.com/questions/10913/best-practices-for-schema-changes-and-data-migrations-to-a-live-database-without

Steve links
- https://www.postgresql.org/docs/9.1/static/backup-dump.html
- https://www.postgresql.org/docs/8.1/static/app-pgdump.html
- https://www.postgresql.org/docs/8.1/static/backup.html
