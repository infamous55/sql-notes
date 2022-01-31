# Aggregate functions

Calculations performed on multiple rows of a table are called **aggregates**. Aggregate functions happen only in the `SELECT` clause and the `HAVING` clause.

### COUNT
The `COUNT` function allows us to calculate how many rows are in a table. It takes the name of a column as an argument, but it should return the same value for any column that you provide.

```sql

SELECT COUNT(*)
FROM books;

```

### SUM
The `SUM` function adds all the values in a given column.

```sql

SELECT SUM(items_left)
FROM stock;

```

### MAX/ MIN
The `MAX` function returns the maximum value in a particular column. The `MIN` function returns the minimum value in a particular column.

```sql

SELECT MAX(rating)
FROM movies;

```

### AVG
The `AVG` function calculates the average value of a column.

```sql

SELECT AVG(price)
FROM books;

```

### ROUND
The `ROUND` funciton rounds the values of a particular column to a specific number of decimals.

```sql

SELECT ROUND(price, 2)
FROM books;

```

### GROUP BY
The `GROUP BY` statement groups data by identical values in the specified columns. It must be written before the `ORDER BY` and `LIMIT` clauses. Both the `GROUP BY` and `ORDER BY` clauses can reference the selected columns by the order in which they appear in the `SELECT` statement. The columns referenced in the `SELECT` clause must appear in the `GROUP BY` statement or be inside an aggregate function.

```sql

SELECT company, division, SUM(sales)
FROM finance_table
WHERE division IN ('marketing', 'transport')
GROUP BY company, division
ORDER BY SUM(sales)
LIMIT 10;

```

```sql

SELECT COUNT(*) AS 'total_movies',
rating
FROM movies
GROUP BY 2
ORDER BY 1;

```

### HAVING
The `HAVING` clause allows us to filter which groups are included in a `GROUP BY` statement. It works like `WHERE`, but for groups.

```sql

SELECT year,
genre,
COUNT(name)
FROM movies
GROUP BY 1, 2
HAVING COUNT(name) > 10;

```