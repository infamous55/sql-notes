# Conditional expressions and procedures

### CASE
The `CASE` statement allows us to only execute SQL statements when certain conditions are met. It has a general form which is similar to a sequence of IF/ELSE statements in a programming language like C++ or JavaScript, and it can also be used as a `CASE` expression. The latter evaluates an expression and then check for equality.

```sql

-- general CASE statement

SELECT name,
CASE 
	WHEN genre == 'romance' THEN 'Chill'
	WHEN genre == 'comedy' THEN 'Chill'
	ELSE 'Intense'
END AS 'Mood'
FROM movies;

-- CASE expression

SELECT rental_rate,
SUM(CASE rental_rate
	WHEN 0.99 THEN 1
	ELSE 0
END) AS bargains,
SUM(CASE rental_rate
	WHEN 2.99 THEN 1
	ELSE 0
) AS regular,
SUM(CASE rental_rate
	WHEN 4.99 THEN 1
	ELSE 0
) AS premium
FROM films;

```

### COALESCE
The `COALESCE` function accepts an unlimited number of arguments and returns the first argument that is not null.

```sql

SELECT COALESCE(1, 2)

-- returns 1

SELECT COALESCE(NULL, 2)

-- returns 2

```

The `COALESCE` function becomes useful when querying a table that has `NULL` values and wanting to substitute those with another value.

```sql

SELECT item, (price - COALESCE(discount, 0))
AS final_price FROM items;

```

### CAST
The `CAST` operator allows to convert a value from one data type into another. It can be used with a single instance, as well as with an entire column.

```sql

-- general SQL syntax

SELECT CAST('5' AS INTEGER);

-- PostgreSQL shorthand

SELECT '5'::INTEGER;

-- using CAST with an entire column

SELECT CAST(inventory_id AS VARCHAR) FROM rental;

```

### NULLIF
The `NULLIF` function takes two arguments and returns `NULL` if they are equal, otherwise it returns the first argument.

```sql

SELECT NULLIF(10, 10);

-- returns NULL

SELECT NULLIF(10, 12);

-- returns 10

SELECT (
	SUM(CASE WHEN department = 'A' THEN 1 ELSE 0 END) /
	NULLIF(SUM(CASE WHEN department = 'B' THEN 1 ELSE 0 END), 0)
) AS department_ratio
FROM depts;

-- returns NULL if there is no entry for dept B

```

### Views
A view is a database object that is of a stored query. A view can be accessed as a virtual table in PostgreSQL. It doesn't duplicate data, it simply stores the query, and it can be updated and deleted as well.

View creation:

```sql

CREATE VIEW customer_info AS
SELECT first_name, last_name, address FROM customer
INNER JOIN address
ON customer.address_id = address.address_id;

```

Updating a view:

```sql

CREATE OR REPLACE VIEW customer_info AS
SELECT first_name, last_name, address, district FROM customer
INNER JOIN address
ON customer.address_id = address.address_id;

```

Dropping a view:

```sql

DROP VIEW IF EXISTS customer_info;

DROP VIEW customer_info;

```

Renaming a view:

```sql

ALTER VIEW customer_info RENAME TO c_info;

```

### Import and export
PgAdmin's import functionality uses the `COPY` statement under the hood. Not every file can be imported, it must match certain conditions. The path must be correct, and the table must be already created, pgAdmin doesn't create it on import. There is no official PosgreSQL or pgAdmin way to create tables from Excel or .csv files, but there are community made tools. A table can also be exported as a file.

Useful resources:
- [How to import and export data using CSV files in PostgreSQL](https://www.enterprisedb.com/postgres-tutorials/how-import-and-export-data-using-csv-files-postgresql)
- [Can I automatically create a table in PostgreSQL from a csv file with headers?](https://stackoverflow.com/questions/21018256/can-i-automatically-create-a-table-in-postgresql-from-a-csv-file-with-headers)
- [How to import CSV file data into a PostgreSQL table?](https://stackoverflow.com/questions/2987433/how-to-import-csv-file-data-into-a-postgresql-table)