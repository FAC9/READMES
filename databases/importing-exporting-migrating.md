# Importing, exporting and migrating databases

## How to import databases from an existing project

The two methods to do this are:
- GUI database client tool
- The command-Line

##### GUI tools:
- SQL Server Management Studio
- Toad for SQL Server
- Database fishing tool
- Apex SQL Studio
- SQuirreL SQL

#### Walk through to import a sql file into your database.

1. Create a database / decide which database you want to import into:<br>
<br> ![](https://github.com/FAC9/READMES/blob/master/week-7/images/1.%20Create%20database.png)

2. As you can see the database is empty:<br>
<br> ![](https://github.com/FAC9/READMES/blob/master/week-7/images/2.%20The%20database%20is%20empty.png)

3. Get the sql file that you want to import:<br>
<br> ![](https://github.com/FAC9/READMES/blob/master/week-7/images/3.%20beg:borrow:steal%20sql%20file.png)

4. Type the command into Bash, NOT in postgresql command line:<br>
<br> ![](https://github.com/FAC9/READMES/blob/master/week-7/images/4%20Command%20to%20import%20database.png)

5. The database has been imported (here is the proof):<br>
<br> ![](https://github.com/FAC9/READMES/blob/master/week-7/images/5.%20Full%20database!.png)

## Migrations in Postgres

### What is a database schema?

A database schema defines how a database is structured. It defines the tables that exist and their names, how those tables are configured, the fields that those tables contain, and the data format for those fields. A schema describes how real-world (or conceptual) entities are modeled by the database.

The schema doesn’t contain any data in itself. It is simply a description of how data added to a database must be structured.

If you start working on a project with an existing database, the first thing you should do is ask for a schema diagram. The diagram will show all of the tables in the database and the foreign keys they use to relate. It should look like this:

![schema-image](http://www.codeproject.com/KB/database/UnitTestDbAppsWithNDbUnit/NDbUnitXPath.jpg)

### What is migration?

Migration is the processing of transferring data from one schema to another - often within the same database. (It may also refer to the process of moving data between two different databases with the same schema, although this tends to be a simpler task - just export from one then import into the other.)

### When might you need to migrate a database?

As a company expands or develops, the real-world or conceptual entities it deals with may change or become more complicated. When this happens, you might need to update your database schema to reflect the changes in the real-world entities that you're dealing with – but all of the data created under the old schema will need to be ‘migrated’ into the new format in order to preserve your previous records. See _Example: cat lovers database_ below.

### The steps of migrating a database

There are many approaches to database migration. One of the most commonly used patterns is __ETL (export, transform, load)__, although others exist.

To migrate data using the ETL pattern, you would first __identify which tables are affected by the migration__. Databases can be huge, so you only want to be working with the data that is specifically affected by the change of schema.

Making changes directly into a live database is a _very bad idea_ – a single typo or poorly written query can destroy millions of records. So when you’ve selected the affected data, you should __export__ it to a safe area, separate from your live data.

When you’ve exported your data, you then need to __transform__ the data from the old schema into the new schema. This should be done using scripts – firstly because this reduces the possibility of human error, and secondly because the transformation can then be applied to your databases in other environments (for example, your production, test and development environments). See _Example: cat lovers database_ for an example script.

When the data has been transformed and validated, you can then __load__ the transformed data back into the database.    

### Things to consider

- If you have a live site with live users, ideally you want to avoid downtime.
- User data is very sensitive and not to be messed with.

### Example: cat lovers database 🐱

In our example, we have a really basic database with just one table. It stores a list of cat lovers and the names of their cats. This works OK for the organisation updating the cat lovers database for a few years, until some of the members start adopting new cats. The single-table database structure just isn't sufficient any more.

It's time to scale.

🐈🐈 🐈 🐈🐈🐈

See below a visual representation of the cat lovers table, and then the schema for the new version of the database, to which we've added a new table and a few extra columns:

![image-1](./images/Database_schema1.png)

Even though our project is a very small one, getting from catLovers-database-1.0 to the proposed schema would include a few steps. And of course it's important that none of the users' data goes missing or gets accidentally changed in the process 🙀.

We might do something like this:

- Create a new "cats" table with all the required columns. The original database table stays as it is.
- From this point on, when new members join the cat lovers club, their data is only recorded in the new format
- But wait! Now we have two different data structures, so it's hard to keep track of which cats already exist. We need to copy data from the first database table to the new "cats" table.

We'll write some SQL for that:

```
INSERT INTO cats (name, color, catLoverId) VALUES
  SELECT cat_name, cat_color, id FROM catLovers;
```
- Now all our data is in one place but we've got some extra columns left in our cat_lovers table which we don't really need any more. In practice, these columns aren't causing us any problems, so we'll leave them in place for an interim period so that we can be 500% sure that none of our data has got lost in migration.
- Later on, we might want to delete the old data for good. After all, some of those cats might have changed colour by now and we wouldn't want to be storing inaccurate data. We can do this with SQL:

```
ALTER TABLE cat_lovers
  DROP COLUMN (cat_name, cat_color);
```

- Our lovely two-columned database now looks more like this:

![image_2](./images/Database_schema2.png)
😻

## Resources

The [Wikipedia entry on ETL](https://en.wikipedia.org/wiki/Extract,_transform,_load) explains a little more about the pattern, its history and its uses.

This [post on StackOverflow](http://dba.stackexchange.com/questions/10913/best-practices-for-schema-changes-and-data-migrations-to-a-live-database-without) informed the cats example and talks about how to minimize impact of database migrations

Here's an [article](https://kostasbariotis.com/data-migration-with-nodejs/) that talks about migration in a node.js context
