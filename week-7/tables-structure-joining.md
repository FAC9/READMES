# Choosing tables structure and joining

## Best practices in table structures (e.g. normalisation)
Think of your database like a messy bedroom:
- If you design the storage in your room well when you first move in then it's easier to regularly add to it/ update it/ keep it tidy.
- This helps to prevent costly and time intensive problems later on.
- It's important to ensure your room is regularly cleaned and tidied to keep it in good shape and to clear out clutter/ duplicates of things that take up space but don't serve a purpose.

### TOP TIPS FOR A TIDY/ GOOD DATABASE
- Always have a primary key
- Cut out redundant/useless values
- Avoid duplicates of values - to avoid not all versions being updated if the data is changed.
- Avoid illogical structures (bad for compatibility, scaling and for accessibility)
- Make column names easy to search for. Not too long or too short. Bad example: 'ID' as the letters i and d may appear as part of other column names.
- Don't make untested changes to a production database.

- Beware of using a spreadsheet as the basis for a table! It may not be normalised.
- Avoid creating tables lots of columns e.g. over 20. Think in a similar vein to modularising functions in js.
- Think carefully before utilising lots of different extensions, it could create compatibility issues in the future.
- Back up your database
- Refactor

### Follow Normalisation (aka organisation) practices:
- There are 3 tiers of normalisation: First/Second/Third normal form or 1NF, 2NF and 3NF.
- A database falls into a tier according to its lowest common denominator.

- Don't put more than one value in a cell. Ie. Student: 'Marina', Subjects: 'Maths, English'. In this case you should create 2 separate rows for Marina rather than putting the subjects in the same cell.
- A column must depend upon an entire primary key not just part of a concatenated primary key.
- Split out columns into separate tables when their values do not relate to the other column values.
Ie. Student: 'Shireen', Age:23, Subject: 'Maths', Student: 'Shireen', Age:23, Subject: 'English' repeats the age of Shireen even though it's not related to the subjects. It would be better to remove age to a separate table to stop students' ages being duplicated unnecessarily.
- Create new tables so that columns are reliant on a relevant primary key. Move columns that are dependent on another column to a new table if the column they rely on is not the primary key.
Ie. Zip code should be the primary key for other address columns. Doing this helps avoid duplications and make the data easier to understand/use.

## What is a primary key and why is it useful?

## How do you join separate tables?

## Differences between inner / outer joins

## Give a practical example of a database with at least 2 tables.

## Extra Resources:

- http://www.studytonight.com/dbms/database-normalization.php
- http://agiledata.org/essays/dataNormalization.html
