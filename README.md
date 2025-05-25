# SQL Basics Guide

## Table of Contents
1. [What is SQL?](#what-is-sql)
2. [Database Fundamentals](#database-fundamentals)
3. [Basic SQL Syntax](#basic-sql-syntax)
4. [Data Types](#data-types)
5. [Creating Tables](#creating-tables)
6. [Inserting Data](#inserting-data)
7. [Querying Data (SELECT)](#querying-data-select)
8. [Filtering Data (WHERE)](#filtering-data-where)
9. [Sorting Data (ORDER BY)](#sorting-data-order-by)
10. [Grouping Data (GROUP BY)](#grouping-data-group-by)
11. [Joining Tables](#joining-tables)
12. [Updating Data](#updating-data)
13. [Deleting Data](#deleting-data)
14. [Common Functions](#common-functions)
15. [Best Practices](#best-practices)

## What is SQL?

**SQL (Structured Query Language)** is a standard programming language designed for managing and manipulating relational databases. It allows you to:
- Create and modify database structures
- Insert, update, and delete data
- Query and retrieve data
- Control access to data

SQL is used by virtually all relational database management systems (RDBMS) including MySQL, PostgreSQL, SQLite, SQL Server, and Oracle.

## Database Fundamentals

### Key Concepts
- **Database**: A collection of organized data
- **Table**: A structured set of data organized in rows and columns
- **Row (Record)**: A single entry in a table
- **Column (Field)**: A data attribute in a table
- **Primary Key**: A unique identifier for each row
- **Foreign Key**: A field that links to the primary key of another table

### Example Database Structure
```
Users Table:
+----+----------+-------------------+-----+
| id | username | email             | age |
+----+----------+-------------------+-----+
| 1  | john_doe | john@example.com  | 25  |
| 2  | jane_sm  | jane@example.com  | 30  |
+----+----------+-------------------+-----+
```

## Basic SQL Syntax

SQL statements are typically written in uppercase for keywords, though most systems are case-insensitive:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

**Key Rules:**
- Statements end with semicolons (`;`)
- String values are enclosed in single quotes (`'`)
- Comments use `--` for single line or `/* */` for multi-line

## Data Types

### Common SQL Data Types

| Data Type | Description | Example |
|-----------|-------------|---------|
| `INT` / `INTEGER` | Whole numbers | `25`, `-100` |
| `VARCHAR(n)` | Variable-length strings | `'Hello World'` |
| `CHAR(n)` | Fixed-length strings | `'ABC'` |
| `TEXT` | Large text fields | Long paragraphs |
| `DECIMAL(p,s)` | Precise decimal numbers | `99.99` |
| `FLOAT` / `REAL` | Floating-point numbers | `3.14159` |
| `DATE` | Date values | `'2024-01-15'` |
| `DATETIME` / `TIMESTAMP` | Date and time | `'2024-01-15 14:30:00'` |
| `BOOLEAN` | True/false values | `TRUE`, `FALSE` |

## Creating Tables

### Basic CREATE TABLE Syntax
```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...
);
```

### Example: Creating a Users Table
```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL,
    age INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Common Constraints
- `PRIMARY KEY`: Unique identifier for each row
- `NOT NULL`: Column cannot be empty
- `UNIQUE`: All values in column must be different
- `DEFAULT`: Sets a default value
- `AUTO_INCREMENT`: Automatically increments numeric values
- `FOREIGN KEY`: Links to another table's primary key

## Inserting Data

### INSERT INTO Syntax
```sql
-- Insert specific columns
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);

-- Insert all columns (in order)
INSERT INTO table_name
VALUES (value1, value2, value3, value4);
```

### Examples
```sql
-- Single record
INSERT INTO users (username, email, age)
VALUES ('john_doe', 'john@example.com', 25);

-- Multiple records
INSERT INTO users (username, email, age)
VALUES 
    ('jane_smith', 'jane@example.com', 30),
    ('bob_wilson', 'bob@example.com', 28),
    ('alice_jones', 'alice@example.com', 35);
```

## Querying Data (SELECT)

### Basic SELECT Syntax
```sql
SELECT column1, column2, ...
FROM table_name;
```

### Examples
```sql
-- Select all columns
SELECT * FROM users;

-- Select specific columns
SELECT username, email FROM users;

-- Using aliases
SELECT username AS name, email AS contact
FROM users;

-- Select with calculations
SELECT username, age, age + 10 AS age_plus_ten
FROM users;
```

## Filtering Data (WHERE)

### WHERE Clause
```sql
SELECT columns
FROM table_name
WHERE condition;
```

### Comparison Operators
| Operator | Description | Example |
|----------|-------------|---------|
| `=` | Equal | `age = 25` |
| `!=` or `<>` | Not equal | `age != 25` |
| `>` | Greater than | `age > 25` |
| `<` | Less than | `age < 25` |
| `>=` | Greater than or equal | `age >= 25` |
| `<=` | Less than or equal | `age <= 25` |

### Logical Operators
```sql
-- AND
SELECT * FROM users 
WHERE age > 25 AND age < 35;

-- OR
SELECT * FROM users 
WHERE username = 'john_doe' OR username = 'jane_smith';

-- NOT
SELECT * FROM users 
WHERE NOT age = 25;

-- IN
SELECT * FROM users 
WHERE age IN (25, 30, 35);

-- BETWEEN
SELECT * FROM users 
WHERE age BETWEEN 25 AND 35;

-- LIKE (pattern matching)
SELECT * FROM users 
WHERE username LIKE 'john%';  -- Starts with 'john'

SELECT * FROM users 
WHERE email LIKE '%@gmail.com';  -- Ends with '@gmail.com'

-- IS NULL / IS NOT NULL
SELECT * FROM users 
WHERE age IS NOT NULL;
```

## Sorting Data (ORDER BY)

### ORDER BY Syntax
```sql
SELECT columns
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC];
```

### Examples
```sql
-- Sort by age (ascending - default)
SELECT * FROM users ORDER BY age;

-- Sort by age (descending)
SELECT * FROM users ORDER BY age DESC;

-- Sort by multiple columns
SELECT * FROM users 
ORDER BY age DESC, username ASC;
```

## Grouping Data (GROUP BY)

### GROUP BY with Aggregate Functions
```sql
SELECT column, aggregate_function(column)
FROM table_name
GROUP BY column;
```

### Common Aggregate Functions
- `COUNT()`: Count rows
- `SUM()`: Sum numeric values
- `AVG()`: Average of numeric values
- `MIN()`: Minimum value
- `MAX()`: Maximum value

### Examples
```sql
-- Count users by age
SELECT age, COUNT(*) as user_count
FROM users
GROUP BY age;

-- Average age
SELECT AVG(age) as average_age
FROM users;

-- Using HAVING (filter groups)
SELECT age, COUNT(*) as user_count
FROM users
GROUP BY age
HAVING COUNT(*) > 1;
```

## Joining Tables

### Types of Joins

#### INNER JOIN
Returns records that have matching values in both tables:
```sql
SELECT users.username, orders.order_date
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```

#### LEFT JOIN
Returns all records from the left table and matched records from the right:
```sql
SELECT users.username, orders.order_date
FROM users
LEFT JOIN orders ON users.id = orders.user_id;
```

#### RIGHT JOIN
Returns all records from the right table and matched records from the left:
```sql
SELECT users.username, orders.order_date
FROM users
RIGHT JOIN orders ON users.id = orders.user_id;
```

#### FULL OUTER JOIN
Returns all records when there's a match in either table:
```sql
SELECT users.username, orders.order_date
FROM users
FULL OUTER JOIN orders ON users.id = orders.user_id;
```

### Example with Sample Data
```sql
-- Assuming we have these tables:
-- users: id, username, email
-- orders: id, user_id, product, order_date

-- Get all users and their orders
SELECT u.username, o.product, o.order_date
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
ORDER BY u.username;
```

## Updating Data

### UPDATE Syntax
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

### Examples
```sql
-- Update single record
UPDATE users
SET age = 26
WHERE username = 'john_doe';

-- Update multiple columns
UPDATE users
SET email = 'newemail@example.com', age = 27
WHERE id = 1;

-- Update multiple records
UPDATE users
SET age = age + 1
WHERE age < 30;
```

**⚠️ Important**: Always use WHERE clause with UPDATE to avoid updating all records!

## Deleting Data

### DELETE Syntax
```sql
DELETE FROM table_name
WHERE condition;
```

### Examples
```sql
-- Delete specific record
DELETE FROM users
WHERE username = 'john_doe';

-- Delete multiple records
DELETE FROM users
WHERE age < 18;

-- Delete all records (use with caution!)
DELETE FROM users;
```

**⚠️ Important**: Always use WHERE clause with DELETE to avoid deleting all records!

## Common Functions

### String Functions
```sql
-- Concatenation
SELECT CONCAT(username, ' - ', email) as user_info FROM users;

-- Length
SELECT username, LENGTH(username) as name_length FROM users;

-- Uppercase/Lowercase
SELECT UPPER(username), LOWER(email) FROM users;

-- Substring
SELECT SUBSTRING(email, 1, 5) as email_prefix FROM users;
```

### Date Functions
```sql
-- Current date/time
SELECT NOW(), CURRENT_DATE, CURRENT_TIME;

-- Date formatting
SELECT DATE_FORMAT(created_at, '%Y-%m-%d') as formatted_date FROM users;

-- Date arithmetic
SELECT username, DATEDIFF(NOW(), created_at) as days_since_creation 
FROM users;
```

### Numeric Functions
```sql
-- Rounding
SELECT ROUND(AVG(age), 2) as average_age FROM users;

-- Absolute value
SELECT ABS(-25) as absolute_value;

-- Power
SELECT POWER(age, 2) as age_squared FROM users;
```

## Best Practices

### 1. Use Consistent Naming Conventions
```sql
-- Good: snake_case
CREATE TABLE user_profiles (
    user_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);
```

### 2. Always Use WHERE with UPDATE/DELETE
```sql
-- Good
UPDATE users SET age = 30 WHERE id = 1;

-- Dangerous
UPDATE users SET age = 30;  -- Updates ALL records!
```

### 3. Use Proper Indexing
```sql
-- Create indexes on frequently queried columns
CREATE INDEX idx_username ON users(username);
CREATE INDEX idx_email ON users(email);
```

### 4. Use Transactions for Related Operations
```sql
START TRANSACTION;
    INSERT INTO users (username, email) VALUES ('new_user', 'new@example.com');
    INSERT INTO user_profiles (user_id, first_name) VALUES (LAST_INSERT_ID(), 'New');
COMMIT;
```

### 5. Validate Data with Constraints
```sql
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) CHECK (price > 0),
    category_id INT,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

### 6. Use Meaningful Column Names
```sql
-- Good
SELECT user_id, order_date, total_amount FROM orders;

-- Poor
SELECT u, od, ta FROM orders;
```

### 7. Comment Complex Queries
```sql
-- Get users who have placed orders in the last 30 days
-- along with their total order count and average order value
SELECT 
    u.username,
    COUNT(o.id) as total_orders,
    AVG(o.total_amount) as avg_order_value
FROM users u
INNER JOIN orders o ON u.id = o.user_id
WHERE o.order_date >= DATE_SUB(NOW(), INTERVAL 30 DAY)
GROUP BY u.id, u.username
HAVING COUNT(o.id) > 1
ORDER BY avg_order_value DESC;
```

## Quick Reference Commands

```sql
-- Database operations
CREATE DATABASE database_name;
USE database_name;
DROP DATABASE database_name;

-- Table operations
DESCRIBE table_name;  -- Show table structure
SHOW TABLES;          -- List all tables
DROP TABLE table_name; -- Delete table

-- Data operations
SELECT * FROM table_name LIMIT 10;  -- Limit results
SELECT DISTINCT column FROM table_name;  -- Unique values
```

---

This guide covers the fundamental concepts of SQL. Practice these concepts with real databases to strengthen your understanding. Remember that SQL syntax can vary slightly between different database systems, but these core concepts remain consistent across all platforms.
