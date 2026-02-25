# SQL JOINS -- Complete Detailed Guide (Beginner to Advanced)

Author: Meghana\
Purpose: Practical understanding of all types of SQL JOINS with clear
examples

------------------------------------------------------------------------

# 1. What is a JOIN?

A JOIN is used to combine rows from two or more tables based on a
related column.

In simple words: If data is stored in multiple tables, JOIN helps us
bring it together.

Normalization splits data into multiple tables. JOIN helps retrieve it
back.

------------------------------------------------------------------------

# 2. Creating Sample Tables

We will create two tables: • students\
• courses

------------------------------------------------------------------------

## Create Students Table

``` sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50),
    city VARCHAR(50)
);
```

------------------------------------------------------------------------

## Create Courses Table

``` sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    student_id INT,
    course_name VARCHAR(50),
    instructor VARCHAR(50)
);
```

------------------------------------------------------------------------

# 3. Insert Sample Data

``` sql
INSERT INTO students VALUES
(1, 'Meghana', 'Bangalore'),
(2, 'Rahul', 'Delhi'),
(3, 'Priya', 'Mumbai'),
(4, 'Arjun', 'Chennai');
```

``` sql
INSERT INTO courses VALUES
(101, 1, 'SQL', 'Ravi'),
(102, 1, 'Python', 'Anu'),
(103, 2, 'SQL', 'Ravi'),
(104, 5, 'Java', 'Kiran');
```

------------------------------------------------------------------------

# 4. INNER JOIN

Returns only matching rows.

``` sql
SELECT s.student_name, c.course_name
FROM students s
INNER JOIN courses c
ON s.student_id = c.student_id;
```

------------------------------------------------------------------------

# 5. LEFT JOIN

Returns all rows from left table and matching rows from right.

``` sql
SELECT s.student_name, c.course_name
FROM students s
LEFT JOIN courses c
ON s.student_id = c.student_id;
```

------------------------------------------------------------------------

# 6. RIGHT JOIN

Returns all rows from right table and matching rows from left.

``` sql
SELECT s.student_name, c.course_name
FROM students s
RIGHT JOIN courses c
ON s.student_id = c.student_id;
```

------------------------------------------------------------------------

# 7. FULL JOIN

Returns all rows from both tables.

``` sql
SELECT s.student_name, c.course_name
FROM students s
FULL JOIN courses c
ON s.student_id = c.student_id;
```

------------------------------------------------------------------------

# 8. CROSS JOIN

Returns Cartesian product.

``` sql
SELECT s.student_name, c.course_name
FROM students s
CROSS JOIN courses c;
```

------------------------------------------------------------------------

# 9. SELF JOIN

``` sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    manager_id INT
);
```

``` sql
INSERT INTO employees VALUES
(1, 'Amit', NULL),
(2, 'Neha', 1),
(3, 'Rohan', 1),
(4, 'Simran', 2);
```

``` sql
SELECT e.emp_name AS Employee,
       m.emp_name AS Manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;
```

------------------------------------------------------------------------

# 10. JOIN with Aggregation

``` sql
SELECT s.student_name,
       COUNT(c.course_id) AS total_courses
FROM students s
LEFT JOIN courses c
ON s.student_id = c.student_id
GROUP BY s.student_name;
```

------------------------------------------------------------------------

# 11. Summary

  Join Type    What It Returns
  ------------ ---------------------------
  INNER JOIN   Only matching rows
  LEFT JOIN    All left + matching right
  RIGHT JOIN   All right + matching left
  FULL JOIN    All rows from both
  CROSS JOIN   All combinations
  SELF JOIN    Table joined with itself

------------------------------------------------------------------------

END OF DOCUMENT
