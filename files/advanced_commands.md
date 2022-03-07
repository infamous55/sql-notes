# Advanced commands

### Working with time and date
Data types in PostgreSQL:
- `TIME` contains only time.
- `DATE` contains only date.
- `TIMESTAMP` contains both time and date.
- `TIMESTAMPTZ` contains time, date, and timezone.

Useful commands:

```sql

SHOW TIMEZONE;

SHOW NOW();

SHOW TIMEOFDAY();

SHOW CURRENT_TIME;

SHOW CURRENT_DATE;

```

The `EXTRACT` statement allows us to obtain a component of a date value.

```sql

SELECT EXTRACT(YEAR FROM payment_date) AS year
FROM payments;

```

The `AGE` function calculates the current age of a given timestamp.

```sql

SELECT AGE(payment_date)
FROM payments;

```

The `TO_CHAR` function converts data into text.

```sql

SELECT TO_CHAR(payment_date, 'dd/mm/yyyy')
FROM payments;

```

### Mathematical functions and operators
A compete list of the mathematical functions and operators available in PostgreSQL can be found [here](https://www.postgresql.org/docs/9.5/functions-math.html).

### String functions and operators
A complete list of the string functions and operators available in PostgreSQL can be found [here](https://www.postgresql.org/docs/9.5/functions-string.html).

Note: The `||` operator is used for string concatenation.

### Subqueries
A subquery is a query nested inside another query. To construct a subquery we put the second query inside brackets and use it as an expression.

```sql

SELECT film_id, title, rental_rate
FROM film
WHERE rental_rate > (
	SELECT AVG(rental_rate)
	FROM film
);

```

The inner query executes first, and then passes the result to the outer query.

### Self-join
A self-join is a query in which a table is joined to itself. Self-joins are useful for comparing values in a column inside the same table. The table is not actually copied, but SQL performs the command as if it were.

```sql

SELECT emp.name, report.name AS rep
FROM employees AS emp
JOIN employees AS report
ON emp.emp_id = report.report_id;

```