# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
For products with a profit % less than 30% of selling price, update the selling price to provide a profit margin of 35% over cost price of the product in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

```sql
update Products
set sell_price=cast(1.35*cost_price as int)
where (sell_price-cost_price)/cost_price<sell_price*0.3;
```

**Output:**

![image](https://github.com/user-attachments/assets/d64b03f6-c165-47ea-ad52-21266cb58aee)


**Question 2**
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.

```sql
update purchases
set per_unit_price=25
where purchase_date is '2022-08-15' and product_id is 12;

update purchases
set total_price=per_unit_price*quantity
where purchase_date is '2022-08-15' and product_id is 12;
```

**Output:**

![image](https://github.com/user-attachments/assets/40a1ee03-3288-44dc-9061-f084ed83a826)


**Question 3**
---
Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.
Products Table 
name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lv     INT        
quantity       INT        
supplier_id    INT           
For example:
Test	Result
select changes();
changes()
----------
4

```sql
UPDATE products
SET sell_price=sell_price * 1.15
WHERE quantity < 50 AND supplier_id = 10;
```

**Output:**

![image](https://github.com/user-attachments/assets/60820b04-05d4-4993-aaf0-aeee93ff746c)


**Question 4**
---
Write a SQL query to Delete customers from 'customer' table where 'AGENT_CODE' is either 'A003' or 'A008'.
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:
Test	Result
select distinct(agent_code)from customer;
AGENT_CODE
----------
A003
A008
A011
A006
A005
A010
A002
A004
A009
A007
A012
A001
AGENT_CODE
----------
A011
A006
A005
A010
A002
A004
A009
A007
A012
A001

```sql
DELETE FROM customer
WHERE AGENT_CODE IN('A003','A008');
```

**Output:**

![image](https://github.com/user-attachments/assets/8607ddca-7cbc-4d1e-928a-61dd4f5a6267)


**Question 5**
---
Write a SQL query to Delete All Doctors with a NULL Specialization
Sample table: Doctors
attributes : doctor_id, first_name, last_name, specialization
For example:
Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin       Jones
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics

```sql
DELETE FROM Doctors
WHERE specialization IS NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/d5cff95d-67d8-4cbc-9b40-5b7cb9c747de)


**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_CITY' is not 'New York' and 'OUTSTANDING_AMT' is greater than 5000.
Sample table: Customer
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:
Test	Result
select changes();
changes()
----------
16

```sql
DELETE from Customer
WHERE CUST_CITY <> 'New York' AND OUTSTANDING_AMT > 5000
```

**Output:**

![image](https://github.com/user-attachments/assets/ad43d92b-b3f9-4bdf-bc54-762a9a1e3984)


**Question 7**
---
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.
Sample table: Doctors
attributes : doctor_id, first_name, last_name, specialization

```sql
delete from Doctors
where Specialization IS 'Pediatrics' AND first_name IS 'Michael'
```

**Output:**

![image](https://github.com/user-attachments/assets/9a9ceaaa-f728-45bc-bb53-985719bbe705)


**Question 8**
---
Write a query to find all the employees whose salary is between 50000 to 100000 from employeeposition table.
EmpID
EmpPosition
DateOfJoining
Salary
1
Manager
01/05/2024
500000
2
Executive
02/05/2024
75000
For example:
Result
EmpID       EmpPosition  DateOfJoining  Salary
----------  -----------  -------------  ----------
2           Executive    2024-05-02     75000
3           Manager      2024-05-01     90000
2           Lead         2024-05-02     85000

```sql
SELECT EmpID,EmpPosition,DateOfJoining,Salary 
FROM employeeposition
WHERE Salary BETWEEN 50000 and 100000;
```

**Output:**

![image](https://github.com/user-attachments/assets/327a5163-f1f5-4a1b-8778-faa6033715de)


**Question 9**
---
Write a SQL statement to Find the salesmen with all information who gets the commission within a range of 0.12 and 0.14.
salesman table
cid         name         type        notnull     dflt_value  pk
----------  -----------  ----------  ----------  ----------  ----------
0           salesman_id  numeric(5)    0                       1
1           name         varchar(30)   0                       0
2           city         varchar(15)   0                       0
3           commission   decimal(5,2)  0                       0

For example:
Result
salesman_id  name        city        commission
-----------  ----------  ----------  ----------
5002         Nail Knite  Paris       0.13
5006         Mc Lyon     Paris       0.14
5007         Paul Adam   Rome        0.13
5003         Lauson Hen  San Jose    0.12

```sql
select * from salesman
where commission BETWEEN 0.12 and 0.14;
```

**Output:**

![image](https://github.com/user-attachments/assets/9fd1a1bd-f664-4a45-905c-b5a0266e4f75)

**Question 10**
---
Write a SQL query to round the decimal column to 3 decimal places from the Calculations table.
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
For example:
Result
id          rounded_value
----------  -------------
1           123.457
2           567.891
3           78.234
4           45.78

```sql
select id,ROUND("decimal", 3) AS
rounded_value
from Calculations
```

**Output:**

![image](https://github.com/user-attachments/assets/92ad1ef8-1543-458b-8724-59540c92a1a2)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
![image](https://github.com/user-attachments/assets/44e30a98-5ae1-44a0-8e4b-aac6bed1f1b6)
