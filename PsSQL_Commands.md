# PostGres SQL

- open SQL Shell (psql)
- enter password

```bash
\l  # list of availabe databases
```

- create database

```bash
CREATE DATABASE new_db;
```
- to connect with this database

```bash
\c new_db;
```

- You are now connected to database "new_db" as user "postgres".

# Insert inot the tables (specific values)

```bash
INSERT INTO students (name, age, grade) VALUES ('Akash', 21, 'A'), ('Anjali', 22, 'B');
```

### All fields

```bash
 INSERT INTO students values (3, 'Aman', 30, 'C');
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