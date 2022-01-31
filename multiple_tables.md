# Multiple tables

### PRIMARY KEY
A *primary key* is a column (or a set of columns) used to uniquely identify each entry in a table. A primary key cannot be `NULL` and cannot repeat itself.

### FOREIGN KEY
A *foreign key* is another table's primary key referenced inside the current working table.

### INNER JOIN
The `JOIN` clause allows us to get data from multiple tables based on common column values. `INNER JOIN` is the default `JOIN`, and it only returns the rows in which the condition specified in `ON` is true.

```sql

SELECT *
FROM orders
INNER JOIN customers
ON orders.customer_id = customers.customer_id;

```

### FULL OUTER JOIN
The `FULL OUTER JOIN` command returns all the data from multiple tables. `NULL` values are used to fill up the rows. The `WHERE` statement can be used to get only records specific to one of the tables. The `LEFT JOIN` and `RIGHT JOIN` commands are part of a subcategory called outer joins.

```sql

SELECT *
FROM registrations
FULL OUTER JOIN logins
ON registrations.name = logins.name;

```

```sql

SELECT * FROM customer
FULL OUTER JOIN payment
ON customer.customer_id = payment.customer_id
WHERE customer.customer_id IS NULL
OR payment.customer_id IS NULL;

```

### LEFT JOIN
The `LEFT JOIN` command keeps the rows from the first table, regardless of whether there is a matching row in the second table. `NULL` values are used to fill up the rows in the second table if the condition was not satisfied. We can get entries that are exclusive to the left table by using a `WHERE` statement.

```sql

SELECT *
FROM newspaper
LEFT JOIN online
ON newspaper.id = online.id
WHERE online.id IS NULL;

```

```sql

SELECT * FROM registrations
LEFT OUTER JOIN logins
ON registrations.name = logins.name;

```

### CROSS JOIN
The `CROSS JOIN` statement matches all rows from the first table with all the rows from the second table. It creates all the possible combinations of records in two tables.

```sql

SELECT month,
COUNT(*)
FROM newspaper
CROSS JOIN months
WHERE start_month <= month AND end_month >= month
GROUP BY month;

```

### UNION
The `UNION` statement combines the results of consecutive `SELECT` clauses.

```sql

SELECT * FROM newspaper
UNION
SELECT * FROM online;

```

### WITH
The `WITH` statement creates a temporary working table from the result of a query using an alias.

```sql

WITH temporary_movies AS (
	SELECT *
	FROM movies
)
SELECT *
FROM temporary_movies
WHERE year BETWEEN 2000 AND 2020;

```