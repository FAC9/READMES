# Choosing tables structure and joining

## Best practices in table structures (e.g. normalization)

## What is a primary key and why is it useful?

## How do you join separate tables?

Joining allows you to relate data in one table to the data in other tables.

#### Inner join

Suppose you want to get data from two tables named A (containing customer data) and B (containing payment data). Table B has the `customer_id` field that relates to the primary key (`customer_id`) of the table A.

The INNER JOIN clause returns rows in table A that have the corresponding rows in the table B.

<img src="img/inner-join.png" style="width: 250px;"/>

__Example:__

Table A

| customer_id    | first_name     | last_name      |
| :------------- | :------------- | :------------- |
| usr0001        | Mary           | Smith          |
| usr0002        | Patricia       | Johnson        |
| usr0003        | Peter          | Menard         |

Table B

| payment_id     | amount         | customer_id    |
| :------------- | :------------- | :------------- |
| p078           | 50             | usr0002        |
| p079           | 10             | usr0001        |
| p090           | 25             | usr0001        |
| p091           | 100            | usr0004        |

To join table A to table B:  
- SELECT clause: specify the columns in both tables from which you want to select data  
- FROM clause: specify the main table  
- INNER JOIN clause: specify the table that the main table joins, the ON keyword and the condition for joining  

``` sql
SELECT * FROM A  
INNER JOIN B ON A.customer_id = B.customer_id;  
```

Result:

| customer_id    | first_name     | last_name      | payment_id     | amount         |
| :------------- | :------------- | :------------- | :------------- | :------------- |
| usr0001        | Mary           | Smith          | p079           | 10             |
| usr0001        | Mary           | Smith          | p090           | 25             |
| usr0002        | Patricia       | Johnson        | p078           | 50             |

#### Left join

The LEFT JOIN clause returns the rows in table A that may or may not have corresponding rows in the table B.

<img src="img/left-join.png" style="width: 250px;"/>

``` sql
SELECT * FROM A  
LEFT [OUTER] JOIN B ON A.customer_id = B.customer_id;  
```

Result:

| customer_id    | first_name     | last_name      | payment_id     | amount         |
| :------------- | :------------- | :------------- | :------------- | :------------- |
| usr0001        | Mary           | Smith          | p079           | 10             |
| usr0001        | Mary           | Smith          | p090           | 25             |
| usr0002        | Patricia       | Johnson        | p078           | 50             |
| usr0003        | Peter          | Menard         | (null)         | (null)         |

#### Full outer join

The OUTER JOIN clause returns the rows in table A that may or may not have corresponding rows in the table B, as well as all rows in table B that do not have corresponding rows in table A.

<img src="img/outer-join.png" style="width: 250px;"/>

``` sql
SELECT * FROM A    
FULL [OUTER] JOIN B ON A.customer_id = B.customer_id;  
```

Result:

| customer_id    | first_name     | last_name      | payment_id     | amount         |
| :------------- | :------------- | :------------- | :------------- | :------------- |
| usr0001        | Mary           | Smith          | p079           | 10             |
| usr0001        | Mary           | Smith          | p090           | 25             |
| usr0002        | Patricia       | Johnson        | p078           | 50             |
| usr0003        | Peter          | Menard         | (null)         | (null)         |
| (null)         | (null)         | (null)         | p091           | 100            |

#### Other types of joins

To return all rows in table A that do not have corresponding rows in table B:

<img src="img/example4.png" style="width: 250px;"/>

``` sql
SELECT * FROM A  
LEFT JOIN B ON A.customer_id = B.customer_id
WHERE B.customer_id IS null;
```
To return all rows unique to Table A and all rows unique to Table B:

<img src="img/example5.png" style="width: 250px;"/>

``` sql
SELECT  
 *
FROM  
 A  
FULL JOIN B ON A.customer_id = B.customer_id
WHERE A.customer_id IS null
OR B.customer_id IS null
```

## Differences between inner / outer joins

## Give a practical example of a database with at least 2 tables.

## Resources

- [A Visual Explanation of SQL Joins](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)
- [PostgreSQL Tutorial](http://www.postgresqltutorial.com/), section 4
