# Choosing tables structure and joining

## Best practices in table structures (e.g. normalization)

## What is a primary key and why is it useful?

## How do you join separate tables?

## Differences between inner / outer joins

This difference between inner and outer joins is commonly demonstrated using ~~buttocks~~ Venn Diagrams.
Why buck years of tradition?

![Venn Diagram of Inner and Outer link]('/images/inout.png')

IMAGINE TWO CIRCLES. THEY ARE PARTIALLY OVERLAPPING. THERE ARE THREE AREAS TO THIS DIAGRAM. THESE ARE THE INSIDE, THE OUTSIDE LEFT, THE OUTSIDE RIGHT. Lets call them I, L, and R.

These two circles are secretly tables, the area within them represents the data that they contain.

Essentially Inner join will make a new table with the shared values of the joined values. It makes a new table which includes the data in I

Outer Join can be used in three different ways.
It can return L + I, R + I, or   L + R + I

http://stackoverflow.com/questions/38549/what-is-the-difference-between-inner-join-and-outer-join

![Complete Join Diagram]('/images/vens.png')


## Give a practical example of a database with at least 2 tables.

This example database shows a possible database used by an online store.

![erd]('/images/sql-model.jpg')
