# What is Database ?

- Collection of organized data that can be easily accessed, managed and updated.

- it stores data electronically
- Data is organized in tables (rows and columns)
- You can query the data using a language (usually SQL) to read, insert, update and delete the data.
- the database system ensures consistency, reliability and security of the data. 

# What is RDBMS ?

- Stands for Relational Databse Management System

- Relational -> Database is organized into tables which are related to each other
- Database -> collection of structured data 
- Management system -> software that allows you to create, read update and delete data (using SQL)
- An RDBMS is a software that helps you store data in tables, relate them to each other and perform operations on them using SQL.

### Key features

1. Data is stored in tables (relations)
2. Each table has rows and columns 
3. Relationship b/w the tables
4. Eg: you have students table, you have courses table, you can link them with an enrollments table
5. Examples of RDBMS: PostgreSQL, MySQL, SQLite, Oracle Database, SQL Server

### Postgre SQL

- open source
- Most featured-rich & powerful
- supports complex queries and joins
- ACID compliant, highly extensible
- support for NOoSQL features 
- used for enterprise-grade apps

# PGAdmin

- A databse is like a big container that stores all your data.
- Inside 1 PostgreSQL server you can create multiple databases.
- Each database is isolated - data in one database is not mixed with another.

# Schema

- Inside a db, you can organize objects using schemas
- Think of a schema as a folder - it helps organize your tables, views, functions, etc
- By default, every postgre sql database has a schema called public

# Table

- The main place where data is stored.
- each table has columns(defines type of data like name, age, salary) and rows (each record like one person/one product/one order)

# Create Database

```bash
CREATE DATABASE new_db;
```

- to connect with this database in pgadmin click on new_db and top right click on Query tool to open the tool inside that database

# Create table 

```bash
CREATE TABLE students (
	student_id INT,
	name char(50),
	age INT,
	grade char(1)
);
```

# Insert inot the tables (specific values)

```bash
INSERT INTO students (name, age, grade) VALUES ('Akash', 21, 'A'), ('Anjali', 22, 'B');
```

# Read Data from the table

```bash 
SELECT * FROM students;
```

# To read only specific fields 

```bash
SELECT name FROM students;
```

# To get the record which has age as 22

```bash
SELECT name FROM students WHERE age = 22;
```

# To update the data in table

```bash
UPDATE students
SET age = 90
WHERE name = 'Aman';
```

# To Delete a row 

```bash
DELETE FROM students WHERE name = 'Anjali';
```

# Data Types

- Numeric Data Types
- Character/String Data Types
- Boolean Type (TRUE, FALSE, NULL)
- Date and Time Types

### Numeric Example

```bash
CREATE TABLE numbers (
	id SERIAL,
	age SMALLINT,
	price NUMERIC(4, 2),
	rating REAL
);

INSERT INTO numbers (age, price, rating)
values (23, 23.67, 12.567);

SELECT * FROM numbers;
```

- serial -> starts from 1 automtically incremented

### Character Example

```bash
CREATE TABLE strings (
	code char(5),
	email varchar(100),
	bio text
);

INSERT INTO strings
values ('23vb4', 'aman@gmail.com', 'hola, this is a very lonnnng text' );

SELECT * FROM strings;
```

# Constraints 

- PRIMARY KEY - Uniquely Identifies each row - id SERIAL PRIMARY KEY
- NOT NULL - Column must have a value - name TEXT NOT NULL
- UNIQUE - No duplicate values allowed - email TEXT UNIQUE
- DEFAULT - Provides default value if none - created_at TIMESTAMP DEFAULT now()
- CHECK - Validates values - age INT CHECK (age > 18)
- FOREIGN KEY - Links one table to another - user_id INT REFERENCES users(id)

```bash
CREATE TABLE random (
	id INT PRIMARY KEY,
	name VARCHAR(100) NOT NULL,
	email TEXT UNIQUE NOT NULL,
	created_at DATE DEFAULT now(),
	age INT CHECK (age>=18)
);

INSERT INTO random (id, name, email, age)
values (1, 'Aman', 'aman@gmail.com', 20);

INSERT INTO random (id, name, email, age)
values (2, 'Ayan', 'ayan@gmail.com', 55);

SELECT * FROM random;
```

# Clauses

- Mainly used for querying data and are kind of building blocks.

- SELECT - Choose which column to display
- FROM - Specify the table
- WHERE - Filter rows based on condition
- GROUP BY - Group rows for aggregation
- HAVING - Filter aggregated groups (used after GROUP BY)
- ORDER BY - Sort result in asc/desc order
- LIMIT - Limit no of rows
- AS - rename columns / tables temporarily(aliasing)
- DISTINCT - Return only unique values

# Clause with operators

```bash
SELECT * FROM products where category = 'Home & Kitchen';

SELECT * FROM products where category != 'Home & Kitchen';

SELECT * FROM products where price > 1000;

SELECT * FROM products where price < 1000;

SELECT * FROM products where price < 1000 and category = 'Electronics';

SELECT * FROM products where price BETWEEN 400 and 1000;

SELECT * FROM products where category IN ('Electronics', 'Home & Kitchen', 'Fitness');

SELECT * FROM products WHERE sku_code LIKE 'W%';

SELECT * FROM products WHERE sku_code LIKE '%123%';

SELECT * FROM products WHERE sku_code LIKE '_B%';

SELECT * FROM products WHERE not category = 'Electronics';
```

# Aggregation Functions

- COUNT(), SUM(), AVG(), MIN(), MAX()

```bash
SELECT COUNT(product_id) FROM products;

SELECT SUM(price) FROM products;

SELECT SUM(price) FROM products where category = 'Electronics';

SELECT ROUND(AVG(price),2) FROM products;

SELECT MIN(price) FROM products;

SELECT MAX(price) FROM products;

SELECT name, price from products where price = (SELECT MIN(price) FROM products);

SELECT AVG(price) from products WHERE category = 'Home & Kitchen' OR category = 'Fitness';

SELECT name, stock_quantity from products WHERE is_available = true and stock_quantity > 50 and price != 299;

SELECT MAX(price), category FROM products group by category;

SELECT distinct UPPER(category) FROM products ORDER BY UPPER(category) desc;
```

# String Functions

- manipulate text data like names, categories etc

- Upper lower and length functions

```bash
SELECT UPPER(name) FROM products;

SELECT LOWER(sku_code) FROM products;

SELECT LENGTH(name) FROM products;
```

- substring - used to extract some portion from string.
- substring(text, location, length)

```bash
SELECT name, SUBSTR(sku_code, 1, 2) FROM products;
```

- LEFT() and RIGHT()
- Get n leftmost and rightmost elements

```bash
SELECT left(sku_code, 2) FROM products;
```

- CONCAT()
- joins 2 strings together

```bash
SELECT CONCAT(name, ' ', category) from products;

SELECT CONCAT_WS(':',name, ' ', category) from products;
```

- TRIM() & REPLACE()
- TRIM() - remove all spaces from string
- REPLACE() - will replace anything 

```bash
SELECT REPLACE(sku_code, left(sku_code, 2), 'GG') from products;
```

# Alter table

- add new columns
- remove
- rename
- change data types
- set/remove default values
- add/remove constraints
- rename table

- first create the table 

```bash
CREATE TABLE student (
	student_id SERIAL PRIMARY KEY,
	name VARCHAR(100),
	age BIGINT
);
```

- Add a new column

```bash
ALTER TABLE student
ADD COLUMN email VARCHAR(100); # default null values in this column
```

- remove a column

```bash
ALTER TABLE student
DROP COLUMN email;
```

- to provide email with default value

```bash
ALTER TABLE student
ADD COLUMN email VARCHAR(100) DEFAULT 'not provided';
```

- rename column

```bash
ALTER TABLE student
RENAME COLUMN name TO full_name;
```

- Change data type of a column 

```bash
ALTER TABLE student
ALTER COLUMN age TYPE SMALLINT;
```

- set default value

```bash
ALTER TABLE student
ALTER COLUMN age SET DEFAULT 18;
```

- remove default value

```bash
ALTER TABLE student
ALTER COLUMN age DROP DEFAULT;
```

- add a constraint

```bash
ALTER TABLE student
ADD CONSTRAINT age_check CHECK (age >=0);
```

- drop a constraint

```bash
ALTER TABLE student
DROP CONSTRAINT age_check;
```

- rename table

```bash
ALTER TABLE student
RENAME TO school_students;
```

# Case
- conditional expression that works like an if else switch statements.
- lets you return different values based on different conditions all within a single query

- syntax

```bash
SELECT 
	column1,
	CASE
		WHEN condition1 THEN result1
		WHEN condition2 THEN result2
		....

		ELSE default_result
	END AS new_colum_name
FROM table_name;
```

- example

```bash
select name, price,
	CASE 
		WHEN (price > 1000) THEN 'Expensive'
		WHEN (price BETWEEN 500 AND 1000) THEN 'Moderate'
		ELSE 'Cheap'
	END AS price_tag
FROM products;
```

- this creates a virtual table but you can also alter real data

```bash
ALTER TABLE products
ADD COLUMN price_tag text;

select * from products;

UPDATE products
SET price_tag = 
CASE 
		WHEN (price > 1000) THEN 'Expensive'
		WHEN (price BETWEEN 500 AND 1000) THEN 'Moderate'
		ELSE 'Cheap'
END;

select * from products;
```
 - examples 

```bash
select name, is_available,
	CASE 
		WHEN is_available THEN 'in_stock'
		ELSE 'out of stock'
	END AS stock
FROM products;
```

```bash
select name, stock_quantity,
	CASE 
		WHEN (stock_quantity > 100) THEN 'High Stock'
		WHEN (stock_quantity BETWEEN 30 and 100) THEN 'Medium Stock'
		ELSE 'Low Stock'
	END AS label
FROM products;
```