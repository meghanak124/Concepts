# SQL
- SQL, or Structured Query Language, used to communicate with databse
- language designed to allow users to query, manipulate, and transform data from a relational database.
- popular SQL databases : SQLite, MySQL, Postgres, Oracle and Microsoft SQL Server.
# Relational Databases
- represents a collection of related 2D tables
- Each of the tables are similar to an Excel spreadsheet, 
- fixed number of named columns (the attributes or properties of the table)
- any number of rows of data.

![](https://media.geeksforgeeks.org/wp-content/uploads/20250728165405585326/acid_properties.webp)

## Basic Terminology 
- table
- data
- record
- fields
- columns
## ER Diagrams
- Entity-Relation diagrams
- **Entity** : objects that we can feel - rectangle
- **Attributes** : property - Oval
- **Relation** : relationship - rhombus
![](https://media.geeksforgeeks.org/wp-content/uploads/20230428115454/Introduction-to-ER-Model-2-768.webp)

**verbal requirements**(gets all requirements from client) --------------> **conceptual diagram**(estimates cost, architecture, design) -------------->  **approved/rejected**(clients reviews and decides)

![](https://www.simplilearn.com/ice9/free_resources_article_thumb/ERDiagramsInDBMS_1.png)


# QUERIES :
### 1. SELECT
```SQL
- SELECT column, another_column, …
FROM mytable;
- SELECT * 
FROM mytable;
```


### 2. Queries with constraints :
```SQL
SELECT column, another_column, …
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

| Header 1 | Header 2 | Header 3 |
|---|---|---|
| =, !=, <, <=, >, >= |	Standard numerical operators  |	col_name != 4
| BETWEEN … AND …	| Number is within range of two values (inclusive)	| col_name BETWEEN 1.5 AND 10.5
| NOT BETWEEN … AND …	| Number is not within range of two values (inclusive)	| col_name NOT BETWEEN 1 AND 10
| IN (…)	| Number exists in a list	| col_name IN (2, 4, 6)
NOT IN (…) | Number does not exist in a list |	col_name NOT IN (1, 3, 5) |
| =	| Case sensitive exact string comparison (notice the single equals)	| col_name = "abc"
| != or <> |	Case sensitive exact string inequality comparison |	col_name != "abcd"
| LIKE |	Case insensitive exact string comparison	| col_name LIKE "ABC"
| NOT LIKE |	Case insensitive exact string inequality comparison |	col_name NOT LIKE "ABCD"
| %	| Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE)	| col_name LIKE "%AT%"(matches "AT", "ATTIC", "CAT" or even "BATS")
| _	| Used anywhere in a string to match a single character (only with LIKE or NOT LIKE)| 	col_name LIKE "AN_"(matches "AND", but not "AN")
| IN (…)	| String exists in a list |	col_name IN ("A", "B", "C")
| NOT IN (…) |	String does not exist in a list	| col_name NOT IN ("D", "E", "F") |

### 3. Filtering and sorting Query results

**i. DISTINCT :**
```SQL
SELECT DISTINCT column, another_column, …
FROM mytable
WHERE condition(s);
```
**ii. ORDER BY :**
```SQL
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```
**iii. LIMIT and OFFSET :**
- LIMIT will reduce the number of rows to return
- OFFSET will specify where to begin counting the number rows from.
```SQL
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

### 4. Multi-table queries with JOINs

**i. Database Normalization :**
- minimizes duplicate data in any single table, and allows for data in the database to grow independently of each other.

| Normal Form | Description |
|---|---|
**First Normal Form (1NF)** | A relation is in first normal form if every attribute in that relation is single-valued attribute. |
**Second Normal Form (2NF)** | A relation that is in First Normal Form and every non-primary-key attribute is fully functionally dependent on the primary key, then the relation is in Second Normal Form (2NF).
| **Third Normal Form (3NF)** | A relation is in the third normal form if there is no transitive dependency for non-prime attributes and it is already in Second Normal Form (2NF). <br><br> A relation is in 3NF if at least one of the following holds for every non-trivial functional dependency X → Y: <br> 1. X is a super key. <br> 2. Y is a prime attribute (each element of Y is part of some candidate key). |
| **Boyce-Codd Normal Form (BCNF)** | For BCNF, the relation should satisfy the following conditions: <br><br> 1. The relation should be in Third Normal Form (3NF). <br> 2. X should be a super key for every functional dependency (FD) X → Y in a given relation. |
| **Fourth Normal Form (4NF)** | A relation R is in 4NF if and only if the following conditions are satisfied: <br><br> 1. It should be in Boyce-Codd Normal Form (BCNF). <br> 2. The table should not have any multi-valued dependency. |
| **Fifth Normal Form (5NF)** | A relation R is in 5NF if and only if it satisfies the following conditions: <br><br> 1. R should already be in 4NF. <br> 2. It cannot be further non-loss decomposed (join dependency). |

**ii. Multi-table queries with JOINs :**
- INNER JOIN is a process that matches rows from the first table and the second table which have the same key to create a result row with the combined columns from both tables
```SQL
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```
**iii. OUTER JOINs :**
- two tables have asymmetric data, then we would have to use a LEFT JOIN, RIGHT JOIN or FULL JOIN instead to ensure that the data you need is not left out of the results.
```SQL
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```
- When joining table A to table B, a LEFT JOIN simply includes rows from A regardless of whether a matching row is found in B. The RIGHT JOIN is the same, but reversed.
### 5. NULLs - Datatype appropriate default values
- reduce NULL values in databases as they require more attention when constructing queries
- An alternative to NULL values is to have data-type appropriate default values, like 0 for numerical data, empty strings for text data, etc.
- you can test a column for NULL values in a WHERE clause by using either the IS NULL or IS NOT NULL constraint.
```SQL
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR …;
```
### 6. Queries with expressions
- to write more complex logic on column values in a query.
- uses **mathematical and string functions** along with basic arithmetic to transform values when the query is executed
```SQL
SELECT particle_speed / 2.0 AS half_particle_speed
FROM physics_data
WHERE ABS(particle_position) * 10.0 > 500;
```
#### **Mathematical Functions**

| Function | Description | Example | Output |
|---------------------|------------|----------|--------|
| + | Addition | SELECT 10 + 5; | 15 |
| - | Subtraction | SELECT 10 - 5; | 5 |
| * | Multiplication | SELECT 10 * 5; | 50 |
| / | Division | SELECT 10 / 5; | 2 |
| % | Modulus | SELECT 10 % 3; | 1 |
| ABS() | Absolute value | SELECT ABS(-20); | 20 |
| ROUND() | Round number | SELECT ROUND(45.678, 2); | 45.68 |
| CEIL() / CEILING() | Round up | SELECT CEIL(4.2); | 5 |
| FLOOR() | Round down | SELECT FLOOR(4.9); | 4 |
| POWER() | Exponent | SELECT POWER(2, 3); | 8 |
| SQRT() | Square root | SELECT SQRT(25); | 5 |
| MOD() | Remainder | SELECT MOD(10, 3); | 1 |
| RAND() | Random number (0–1) | SELECT RAND(); | 0.x |
| SUM() | Total of column | SELECT SUM(rating) FROM movies; | Depends on data |
| AVG() | Average value | SELECT AVG(rating) FROM movies; | Depends on data |
| MIN() | Smallest value | SELECT MIN(rating) FROM movies; | Depends on data |
| MAX() | Largest value | SELECT MAX(rating) FROM movies; | Depends on data |
| COUNT() | Count rows | SELECT COUNT(*) FROM movies; | Depends on data |


#### **String Functions**

| Function | Description | Example | Output |
|----------|------------|----------|--------|
| CONCAT() | Join strings | SELECT CONCAT('Hello',' World'); | Hello World |
| LENGTH() | Count characters | SELECT LENGTH('Meghana'); | 7 |
| UPPER() | Convert to uppercase | SELECT UPPER('hello'); | HELLO |
| LOWER() | Convert to lowercase | SELECT LOWER('HELLO'); | hello |
| TRIM() | Remove spaces | SELECT TRIM('  hello  '); | hello |
| SUBSTRING() | Extract part of string | SELECT SUBSTRING('Meghana',1,4); | Megh |
| REPLACE() | Replace text | SELECT REPLACE('Hello World','World','SQL'); | Hello SQL |
| LEFT() | Left characters | SELECT LEFT('Meghana',3); | Meg |
| RIGHT() | Right characters | SELECT RIGHT('Meghana',2); | na |
| INSTR() | Find position | SELECT INSTR('Meghana','g'); | 3 |
| LPAD() | Pad left | SELECT LPAD('123',5,'0'); | 00123 |
| RPAD() | Pad right | SELECT RPAD('123',5,'0'); | 12300 |

- **AS keyword :** 
- gives a descriptive alias using the AS keyword.
- regular columns and even tables can also have aliases to make them easier to refer in the output
```SQL
SELECT column AS better_column_name, …
FROM a_long_widgets_table_name AS mywidgets
INNER JOIN widget_sales
  ON mywidgets.id = widget_sales.widget_id;
  ```
### 7. Queries with aggregates
**i. GROUP BY :**
- GROUP BY is used to group rows that have the same values in specified columns.
```SQL
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression
GROUP BY column;

--OR

SELECT group_by_column, AGG_FUNC(column_expression) AS aggregate_result_alias, …
FROM mytable
WHERE condition
GROUP BY column
HAVING group_condition;
```
### 8. ORDER OF EXECUTION 
i. FROM and JOINs

ii. WHERE

iii. GROUP BY

iv. HAVING

v. SELECT

vi. DISTINCT

vii. ORDER BY

viii. LIMIT / OFFSET

### 9. INSERTING NEW DATA
- **the database schema is what describes the structure of each table, and the datatypes that each column of the table can contain.**
```SQL
INSERT INTO mytable
(column, another_column, …)
VALUES (value_or_expr, another_value_or_expr, …),
      (value_or_expr_2, another_value_or_expr_2, …),
      …;
```
### 10. UPDATING ROWS
- Similar to the INSERT statement, you have to specify exactly which table, columns, and rows to update
```SQL
UPDATE mytable
SET column = value_or_expr, 
    other_column = another_value_or_expr, 
    …
WHERE condition;
```

### 11. DELETING ROWS
- describes the table to act on, and the rows of the table to delete through the WHERE clause.
- leaving out the WHERE constraint, then all rows are removed,
```SQL
DELETE FROM mytable
WHERE condition;
```

### 12. CREATING TABLES
```SQL
CREATE TABLE IF NOT EXISTS mytable (
    column DataType TableConstraint DEFAULT default_value,
    another_column DataType TableConstraint DEFAULT default_value,
    …
);
```
| Data type |	Description|
|----------|------------|
INTEGER, BOOLEAN	| whole integer values or boolean value is represented as an integer value of just 0 or 1.
FLOAT, DOUBLE, REAL| precise numerical data like fractional values. 
CHARACTER(num_chars), VARCHAR(num_chars), TEXT	| CHAR : Fixed length text (adds extra spaces if shorter). Best for data with same length.VARCHAR : Variable length text (stores only actual characters). Best for names, emails, addresses.
DATE, DATETIME	| stores date and time stamps to keep track of time series and event data.
BLOB	| SQL can store binary data in blobs right in the database. These values are often opaque to the database, so you usually have to store them with the right metadata to requery them.

### KEYS

| Constraint            | Description |
|-----------------------|------------|
| PRIMARY KEY           | Column values must be unique and identify each row. |
| AUTOINCREMENT         | Automatically increases integer value for each new row (not supported in all DBs). |
| UNIQUE                | Column values must be unique, but it is not necessarily the main identifier. |
| NOT NULL              | Column cannot store NULL (empty) values. |
| CHECK (expression)    | Ensures inserted values satisfy a condition (e.g., positive number). |
| FOREIGN KEY           | Ensures values match a valid value in another table column (maintains relationship between tables). |

### 13. ALTERING TABLES
```SQL
--Adding columns
ALTER TABLE mytable
ADD column_name DataType OptionalTableConstraint 
    DEFAULT default_value;

--Removing columns
ALTER TABLE mytable
DROP column_to_be_deleted;

--Renaming the table
ALTER TABLE mytable
RENAME TO new_table_name;
```

### 14. DROPPING TABLES
- differs from the DELETE statement
```SQL
DROP TABLE IF EXISTS mytable;
```
- with a FOREIGN KEY dependency) then you will have to either update all dependent tables first to remove the dependent rows or to remove those tables entirely.