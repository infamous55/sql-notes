# Data manipulation

### Data types
The main data types in PostgreSQL are:
- Boolean (True or False)
- Character (char, varchar, and text)
- Numeric (integer or floating-point number)
- Temporal (date, time, timestamp, and interval)
- UUID (Universally Unique Identifier)
- Array
- JSON
- Hstore (key-value pair)
- Special types (for network addresses, geometric data, etc.)

When creating databases and tables, we should be careful choosing which data types to use. Make sure to check the [official documentation](https://www.postgresql.org/docs/9.5/datatype.html) to see the constrains of each data type, and search for best practices online. Remember that we can always delete information, but we can't go back in time and add more data.

### CREATE
The `CREATE` statement allows us to create a new table into the database.

```sql

CREATE TABLE posts (
	id INTEGER
	name TEXT
	author TEXT
	release_date DATE
) INHERITS(articles);

```

### Constraints
Column constraints are the rules applied to the values of individual columns:

- `PRIMARY KEY` constraint can be used to uniquely identify the row.
- `FOREIGN KEY` constrains data based on columns of other tables.
- `UNIQUE` columns have a different value for every row.
- `NOT NULL` columns must have a value.
- `DEFAULT` assigns a default value for the column when no value is specified.
- `CHECK` ensures that all values satisfy certain conditions.

There can be only one `PRIMARY KEY` column per table and multiple `UNIQUE` columns.

```sql

CREATE TABLE students (  
	id INTEGER PRIMARY KEY,
	name TEXT UNIQUE,
	grade INTEGER NOT NULL,
	age INTEGER DEFAULT 17,
	absences INTEGER CHECK (absences >= 0)
);

```

Table constrains are rules applied to entire tables:

- `CHECK` ensures that all values inserted into the table satisfy certain conditions.
- `REFERENCES` verifies that all values inserted into a column exist in a column in another table.
- `UNIQUE` forces the values stored in the specified columns to be unique.
- `PRIMARY KEY` allows to define a primary key that consists of multiple columns.

### SERIAL
The `SERIAL` data type creates a sequence object and sets the next value generated by the sequence as the default value for the column. It is often used as a *primary key*. The column with `SERIAL` as the data type won't adjust if an entry is removed.

```sql

CREATE TABLE account (
	user_id SERIAL PRIMARY KEY,
	username VARCHAR(50) UNIQUE NOT NULL,
	password VARCHAR(50) NOT NULL,
	email VARCHAR(200) UNIQUE NOT NULL
);

```

### INSERT
The `INSERT` statement inserts a new row into a table.

```sql

INSERT INTO books (id, name, author, release_date)
VALUES (1, 'Dance, Dance, Dance', 'Haruki Murakami', '1994-01-01');

```

Note: `SERIAL` columns don't need to be provided a value.

### SELECT
The `SELECT` statement fetches data from the database.

```sql

SELECT name FROM books;

SELECT * FROM books;

```

### ALTER TABLE
The `ALTER TABLE` statement is used to modify the columns of an existing table.

```sql

-- adding a column

ALTER TABLE books  
ADD COLUMN rating FLOAT;

-- dropping a column

ALTER TABLE books
DROP COLUMN rating;

-- adding a constraint

ALTER TABLE books
ALTER COLUMN name
SET NOT NULL;

ALTER TABLE stock
ALTER COLUMN number
SET DEFAULT 0;

-- dropping a constraint

ALTER TABLE books
ALTER COLUMN name
DROP NOT NULL;

```

We can change the name of a table or a column like this:

```sql

-- renaming a table

ALTER TABLE information
RENAME TO new_info;

-- renaming a column

ALTER TABLE new_info
RENAME COLUMN persons TO people;

```

### UPDATE
The `UPDATE` statement is used to edit rows in a table.

```sql

UPDATE books  
SET name =??'A Wild Sheep Chase', release_date =??'1982-10-13'  
WHERE id =??1;

```

We can update using another table's values (this is called an "update join").

```sql

UPDATE registrations
SET email = logins.email
FROM logins
WHERE registrations.name = logins.name;

```

The `RETURNING` statement returns the values that were modified.

```sql

UPDATE account
SET last_login = created_on
RETURNING account_id, last_login;

```

### DELETE
The `DELETE` statement deletes one or more rows from a table.

```sql

DELETE FROM books
WHERE author IS NULL;

```

We can delete based on data from another table.

```sql

DELETE FROM books
USING out_of_stock
WHERE books.id = out_of_stock.id;

```

We can delete all the rows from a table.

```sql

DELETE FROM table;

```

Similar to `UPDATE`, we can return the values which were deleted with the `RETURNING` statement.

### DROP
The `DROP` statement allows for the complete removal of a column. The `CASCADE` keyword allows for the removal of all associated dependencies.

```sql

ALTER TABLE new_info
DROP COLUMN IF EXISTS people;

```