# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
-- Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

```sql
ALTER TABLE employee
ADD first_name varchar(50);

ALTER TABLE employee
ADD last_name varchar(50);
```

**Output:**

![output1](https://github.com/user-attachments/assets/170315d2-f3a1-4081-9995-ffd00c00c5dd)


**Question 2**
---
-- Create a new table named products with the following specifications:
  - product_id as INTEGER and primary key.
  - product_name as TEXT and not NULL.
  - list_price as DECIMAL (10, 2) and not NULL.
  - discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
  - A CHECK constraint at the table level to ensure:
  - list_price is greater than or equal to discount
  - discount is greater than or equal to 0
  - list_price is greater than or equal to 0

```sql
CREATE TABLE products(
    product_id  INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    list_price DECIMAL (10, 2) NOT NULL,
    discount DECIMAL (10, 2) DEFAULT 0 not NULL,
    CHECK (list_price >= discount AND discount >= 0 AND list_price >= 0)
);
```

**Output:**

![output2](https://github.com/user-attachments/assets/d96c5cef-6d3b-4fda-a1df-48ab1874ae47)


**Question 3**
---
-- Create a table named Bonuses with the following constraints:
  - BonusID as INTEGER should be the primary key.
  - EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
  - BonusAmount as REAL should be greater than 0.
  - BonusDate as DATE.
  - Reason as TEXT should not be NULL.

```sql
CREATE TABLE Bonuses(
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount  REAL CHECK (BonusAmount > 0),
    BonusDate DATE ,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

![output3](https://github.com/user-attachments/assets/37d54ceb-d3c1-4413-ae3e-5cfe6e15979e)


**Question 4**
---
-- Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0

```sql
INSERT INTO Student_details(RollNo, Name, Gender, Subject, MARKS)
SELECT RollNo, Name, Gender, Subject, MARKS FROM Archived_students
```

**Output:**

![output4](https://github.com/user-attachments/assets/885af799-1b86-43f1-88f2-fbf34b9a2bff)

**Question 5**
---
-- Create a table named Departments with the following columns:

  - DepartmentID as INTEGER
  - DepartmentName as TEXT

```sql
CREATE TABLE Departments(
    DepartmentID INTEGER,
    DepartmentName TEXT
);
```

**Output:**

![output5](https://github.com/user-attachments/assets/06ba1860-d9a6-4bef-9295-6fd015d2442f)


**Question 6**
---
-- Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies. 

```sql
ALTER TABLE Companies
RENAME COLUMN name TO first_name;

ALTER TABLE Companies
ADD mobilenumber number;

ALTER TABLE Companies
ADD DOB Date;

ALTER TABLE Companies
ADD State varchar(30);
```

**Output:**

![output6](https://github.com/user-attachments/assets/f78eec89-3252-4347-80b6-82ca5d2159c7)

**Question 7**
---
-- Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

```sql
INSERT INTO Products(ProductID, Name, Category, Price, Stock)
VALUES (101, 'Laptop', 'Electronics', 1500, 50);
```

**Output:**

![output7](https://github.com/user-attachments/assets/3740f4fb-e58b-46c6-baf6-a92edfcffd58)

**Question 8**
---
-- Create a new table named item with the following specifications and constraints:
  - item_id as TEXT and as primary key.
  - item_desc as TEXT.
  - rate as INTEGER.
  - icom_id as TEXT with a length of 4.
  - icom_id is a foreign key referencing com_id in the company table.
  - The foreign key should cascade updates and deletes.
  - item_desc and rate should not accept NULL.

```sql
CREATE TABLE item(
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK (LENGTH(icom_id) = 4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
);
```

**Output:**

![output8](https://github.com/user-attachments/assets/bd1e96cd-af7f-46eb-ac02-17fc38e369f4)

**Question 9**
---
-- Create a table named ProjectAssignments with the following constraints:
  - AssignmentID as INTEGER should be the primary key.
  - EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
  - ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
  - AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments(
    AssignmentID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY(ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

![output9](https://github.com/user-attachments/assets/2438eb48-b99e-4d04-bf1e-1a872b95b048)

**Question 10**
---
-- In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021

```sql
INSERT INTO Books(ISBN, Title, Author, Publisher, Year)
VALUES ('978-1234567890', 'Introduction to AI', 'John Doe', NULL, NULL);

INSERT INTO Books(ISBN, Title, Author, Publisher, Year)
VALUES ('978-9876543210', 'Deep Learning', 'Jane Doe', 'TechPress', 2022);

INSERT INTO Books(ISBN, Title, Author, Publisher, Year)
VALUES ('978-1122334455', 'Cybersecurity Essentials', 'Alice Smith', NULL, 2021);
```

**Output:**

![output10](https://github.com/user-attachments/assets/88cdabec-65e7-4511-84b5-623d70e4c19a)

![image](https://github.com/user-attachments/assets/699c69fc-a20a-437a-9237-8880afa987bb)
## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
