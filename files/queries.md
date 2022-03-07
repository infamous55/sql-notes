# Queries

### SELECT

The `SELECT` clause is used every time we want to retrieve information from the database.

```sql

SELECT * FROM books;

```

`*` means all columns.

### AS

The `AS` keyword is used to rename a column by giving it an alias. The column isn't renamed in the table, only when displaying the result. The renaming takes place at the very end of the statement, we cannot use the created alias inside of a `WHERE` statement, for example.

```sql

SELECT name AS 'Title'
FROM books;

```

### DISTINCT

`DISTINCT` is used to return unique values in the output. It can be used with or without paranthesis.

```sql

SELECT DISTINCT author
FROM books;

```

### WHERE

The `WHERE` clause is used to filter the results using a certain condition.
Comparison operators used with the `WHERE` clause are:

- `=` equal to
- `!=` not equal to
- `>` greater than
- `<` less than
- `>=` greater than or equal to
- `<=` less than or equal to

```sql

SELECT *
FROM books
WHERE rating > 8;

```

### LIKE

The `LIKE` operator can be used inside of a `WHERE` clause to match a specified pattern. The `_` wildcard can be used to match a single unspecified character, while the `%` wildcard can be used to match zero or more unknown characters. `ILIKE` is the same as `LIKE`, but case insensitive.

```sql

SELECT *
FROM movies
WHERE name LIKE 'Se_en';

```

```sql

SELECT *
FROM movies
WHERE name LIKE '%man%';

```

### IS NULL

The comparison operators don't work with `NULL`, instead we use `IS NULL` and `IS NOT NULL`.

```sql

SELECT *
FROM books
WHERE rating IS NOT NULL;

```

### BETWEEN

The `BETWEEN` operator can be used to filter by a range of values. Both bounds are inclusive.

```sql

SELECT *
FROM movies
WHERE year BETWEEN 1980 AND 1990;

```

```sql

SELECT *
FROM movies
WHERE name BETWEEN 'A' AND 'J';

```

### AND

The `AND` operator allows multiple conditions to be combined. Both conditions must be true in order to include a row.

```sql

SELECT *
FROM books
WHERE author = 'Haruki Murakami'
AND release_date > '1999.01.01';

```

### OR

The `OR` operator allows multiple conditions to be combined. At least one of the conditions must be true in order to include a row.

```sql

SELECT *
FROM movies
WHERE release_date > '2014.01.01'
OR genre = 'action';

```

### IN

The `IN` operator is used to check if a value shows up in a list.

```sql

SELECT *
FROM movies
WHERE genre IN ('action', 'horror', 'drama');

```

### ORDER BY

The `ORDER BY` clause can be used to sort the result set by a particular column either alphabetically or numerically. It can be ordered in two ways:

- `DESC` is a keyword used to sort the results in descending order.
- `ASC` is a keyword used to sort the results in ascending order (default).

```sql

SELECT *
FROM contacts
ORDER BY birth_date DESC;

```

### LIMIT

The `LIMIT` clause is used to narrow a result set to the specified number of rows. It always sits at the end of the query, and it is not supported in all SQL databases.

```sql

SELECT *
FROM books
LIMIT 5;

```
