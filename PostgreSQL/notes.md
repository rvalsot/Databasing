# Notes

Notes on how to do stuff with PostgreSQL.

__Command Shell commands__

Login
``` shell
# Login into postgres user
$ sudo -i -u postgres

# Login to postgres functionalities
$ psql
```

Administration
``` shell
# Connect to a database
$ \c database_name

# Details about something (current database, tables)
$ \d stuff_name

# List of databases in the system
$ \l

# Quit from current action
$ \q

# Clear the Terminal
$ \! clear
```

## Common SQL commands

General commands for creation, deletion, insertion.

``` sql
-- Creations -----------------------------------------
CREATE DATABASE database_name;
CREATE TABLE table_name (
  COLUMN TYPE MODIFIERS,
);

-- Drops ---------------------------------------------
DROP DATABASE database_name;
DROP TABLE table_name;

-- Insertion -----------------------------------------
-- Insert a record
INSERT INTO table_name (column, column, etc.) VALUES (value, value, etc.);
-- Insert several records on same table
INSERT INTO table_name(column) VALUES (value1), (value2), (value...);

-- Selection -----------------------------------------
-- Select all records from one table
SELECT * FROM table_name;

-- Users ---------------------------------------------
-- Who is the current user
SELECT current_user;

```

Properties for data
``` sql

-- Auto increment
CREATE TABLE table_name(
  ID SERIAL PRIMARY KEY -- ← The 'SERIAL' will auto increment our value
);

-- Foreign Key
CREATE TABLE table_name(
  foreign_key TYPE REFERENCES other_table(ref)
);
```

__Joined Queries__

* __Cross Join__: returns a Cartesian product of rows from tables joined. Every member of `table A` is joined with everyone of `table B`.
* __Inner Join__: joins over a connection done with foreign keys. Returns a combination where identifier and foreign key match some pattern.
* __Outer Join__: Could be `LEFT`, `RIGHT` or `FULL` join that returns all the single elements on one table and the matches they have with the other table.

``` sql

-- Cross Join
SELECT {selection} FROM table_a CROSS JOIN table_b;

-- Inner Join
SELECT table_a.fields, table_b.columns FROM table_a INNER JOIN table_b ON table_a.id = table_b.fk;

-- Inner Join with double base and one transactional
SELECT table_a.fields, table_b.fields FROM table_a INNER JOIN table_t ON table_a.id = table_t.fk INNER JOIN table_b ON table_t.fk = table_b.id;

-- Outer Join -----------------------------------
-- Full
SELECT table_a.fields, table_b.fields FROM table_a FULL OUTER JOIN table_b ON table_a.id = table_b.id;
-- Left
SELECT table_a.fields, table_b.fields FROM table_a LEFT OUTER JOIN table_b ON table_a.id = table_b.id;
-- Right
SELECT table_a.fields, table_b.fields FROM table_a RIGHT OUTER JOIN table_b ON table_a.id = table_b.id;

```

__Clauses__

* `AND`: allows you to join conditionals.
* `IN`: allows you to specify multiple value in a `WHERE` clause.
* `IS NOT NULL`:
* `LIKE`:
* `NOT`: returns the negation of the condition.
* `OR`:
* `WHERE`: helps you to filter the registries that complain with certain rules.

``` sql
-- And
SELECT [selection] FROM table WHERE [condition] AND [condition];

-- In
SELECT [selection] FROM table WHERE [base] IN(value #1, value #2);

-- Not
SELECT [selection] FROM table WHERE [base] NOT [condition];

-- Where
SELECT [selection] FROM table WHERE [condition];

```
