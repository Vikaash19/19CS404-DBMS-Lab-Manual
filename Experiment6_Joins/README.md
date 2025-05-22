# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
```
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.
Sample table: salesman
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
Sample table: customer
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
For example:
Result
Salesman         cust_name        city
---------------  ---------------  ---------------
Bob Emily        Brad Davis       New York
Nail Knite       Fabian Johns     Paris
Pit Alex         Brad Guzan       London
Pit Alex         Julian Green     London
Mc Lyon          Fabian Johns     Paris
```

```sql
SELECT s.name AS Salesman, c.cust_name, s.city
FROM salesman s
JOIN customer c
  ON s.city = c.city;
```

**Output:**

![image](https://github.com/user-attachments/assets/7269de0d-d281-49c8-bdda-ac0d1b21de71)


**Question 2**
```
Write the SQL query that achieves the selection of all columns from the "patients" table and the specialization from the "doctors" table (aliased as "doctor_specialization"), with an inner join on the "doctor_id" column.
PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT
DOCTORS TABLE:
name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)
For example:
Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id   doctor_specialization
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------  ---------------------
1                Alice            Williams         1980-05-12       2024-01-10                      1           Cardiology
2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2           Orthopedics
3                Charlie          Davis            1972-11-30       2024-03-10                      3           Pediatrics
```

```sql
select p.*,d.specialization AS doctor_specialization
from patients p
inner join doctors d on p.doctor_id=d.doctor_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/91b3245e-3bc9-45c6-93b1-30036c7c8d9c)


**Question 3**
```
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 
Sample table: orders
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:
Result
ord_no           ord_date         purch_amt        Customer Name    grade       Salesman    commission
---------------  ---------------  ---------------  ---------------  ----------  ----------  ----------
70001            2012-10-05       150.5            Graham Zusi      200         Nail Knite  0.13
70009            2012-09-10       270.65           Brad Guzan       100         Pit Alex    0.11
70002            2012-10-05       65.26            Nick Rimando     100         Bob Emily   0.15
70004            2012-08-17       110.5            Geoff Cameron    100         Lauson Hen  0.12
70007            2012-09-10       948.5            Graham Zusi      200         Nail Knite  0.13
70005            2012-07-27       2400.6           Brad Davis       200         Bob Emily   0.15
70008            2012-09-10       5760.0           Nick Rimando     100         Bob Emily   0.15
70010            2012-10-10       1983.43          Fabian Johns     300         Mc Lyon     0.14
70003            2012-10-10       2480.4           Geoff Cameron    100         Lauson Hen  0.12
70012            2012-06-27       250.45           Julian Green     300         Nail Knite  0.13
70011            2012-08-17       75.29            Jozy Altidore    200         Paul Adam   0.13
70013            2012-04-25       3045.6           Nick Rimando     100         Bob Emily   0.15
```

```sql
select o.ord_no,o.ord_date,o.purch_amt,c.cust_name AS "Customer Name",c.grade,s.name AS "Salesman",s.commission
from orders o
join customer c on o.customer_id=c.customer_id
join salesman s on o.salesman_id=s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/1d236535-3b41-48b9-a678-4ca92c024859)


**Question 4**
```
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  
Sample table: customer
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:
Result
Customer Name    city             Salesman         city             commission
---------------  ---------------  ---------------  ---------------  ----------
Nick Rimando     Chennai          Bob Emily        New York         0.15
Graham Zusi      California       Nail Knite       Paris            0.13
Julian Green     London           Nail Knite       Paris            0.13
Jozy Altidore    Moscow           Paul Adam        Rome             0.13
```

```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.city AS "city",
    s.commission
FROM 
    customer c
JOIN 
    salesman s ON c.salesman_id = s.salesman_id
WHERE 
    c.city <> s.city
    AND s.commission > 0.12;
```

**Output:**

![image](https://github.com/user-attachments/assets/7189bcbb-f6dc-43ed-9f1f-1b8407432089)


**Question 5**
```
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  
Sample table: customer
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:
Result
cust_name        city             grade            Salesman         city
---------------  ---------------  ---------------  ---------------  ----------
Brad Guzan       London           100              Pit Alex         London
Nick Rimando     Chennai          100              Bob Emily        New York
Jozy Altidore    Moscow           200              Paul Adam        Rome
Fabian Johns     Paris            300              Mc Lyon          Paris
Graham Zusi      California       200              Nail Knite       Paris
Brad Davis       New York         200              Bob Emily        New York
Julian Green     London           300              Nail Knite       Paris
Geoff Cameron    Berlin           100              Lauson Hen       San Jose
```

```sql
SELECT 
    c.cust_name,
    c.city AS "city",
    c.grade,
    s.name AS "Salesman",
    s.city AS "city"
FROM 
    customer c
JOIN 
    salesman s ON c.salesman_id = s.salesman_id
ORDER BY 
    c.customer_id ASC;
```

**Output:**

![image](https://github.com/user-attachments/assets/1ca74080-cc49-40a8-947e-384d60398d41)


**Question 6**
```
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:
ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

APPOINTMENTS TABLE:
ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date

For example:
Result
date_of_birth    appointment_id   patient_id       doctor_id        appointment_date
---------------  ---------------  ---------------  ---------------  -------------------
1980-05-12       1                1                1                2024-01-05 10:00:00
```

```sql
select p.date_of_birth,a.appointment_id,a.patient_id,a.doctor_id,a.appointment_date
from patients p
inner join APPOINTMENTS a ON p.patient_id=a.patient_id
where p.first_name="Alice";
```

**Output:**

![image](https://github.com/user-attachments/assets/d5879e70-bab2-4a3c-822a-aaf704f88b9c)


**Question 7**
```
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman_id values that have more than one associated customer.
Customer Table:
```

![image](https://github.com/user-attachments/assets/8c040502-063a-4d9c-8832-44d6bd863065)

```
Salesmen Table:
```

![image](https://github.com/user-attachments/assets/a9ca7126-875f-4240-8431-15906acdfe74)

```
For example:
Result
name             cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
Bob Emily        Nick Rimando     Chennai          100              5001
Bob Emily        Brad Davis       New York         200              5001
Nail Knite       Graham Zusi      California       200              5002
Nail Knite       Julian Green     London           300              5002
```

```sql
SELECT 
    s.name,
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM 
    salesman s
LEFT JOIN 
    customer c ON s.salesman_id = c.salesman_id
WHERE 
    c.salesman_id IN (
        SELECT salesman_id
        FROM customer
        GROUP BY salesman_id
        HAVING COUNT(*) > 1
    )
order by c.grade;
```

**Output:**

![image](https://github.com/user-attachments/assets/39dffd63-eda4-452c-a65d-bec97d0684fb)


**Question 8**
```
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.
Sample table: orders
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer
customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
For example:
Result
cust_name        city             ord_no           ord_date         Order Amount
---------------  ---------------  ---------------  ---------------  ------------
Nick Rimando     Chennai          70013            2012-04-25       3045.6
Julian Green     London           70012            2012-06-27       250.45
Brad Davis       New York         70005            2012-07-27       2400.6
Geoff Cameron    Berlin           70004            2012-08-17       110.5
Jozy Altidore    Moscow           70011            2012-08-17       75.29
Nick Rimando     Chennai          70008            2012-09-10       5760.0
Graham Zusi      California       70007            2012-09-10       948.5
Brad Guzan       London           70009            2012-09-10       270.65
Nick Rimando     Chennai          70002            2012-10-05       65.26
Graham Zusi      California       70001            2012-10-05       150.5
Fabian Johns     Paris            70010            2012-10-10       1983.43
Geoff Cameron    Berlin           70003            2012-10-10       2480.4
```

```sql
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount"
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
ORDER BY 
    o.ord_date ASC;
```

**Output:**

![image](https://github.com/user-attachments/assets/4ddbc7e5-7f7b-499d-87eb-967176949975)


**Question 9**
```
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n"), with an inner join on the "department_id" column and a condition filtering for nurses in the 'Pediatrics' department.
NURSES TABLE:
ATTRIBUTES - nurse_id, first_name, last_name, department_id

DEPARTMENTS TABLE:
ATTRIBUTES - department_id, department_name

For example:
Result
nurse_id         first_name       last_name        department_id
---------------  ---------------  ---------------  ---------------
3                Sophia           Clark            3
```

```sql
SELECT 
    n.*
FROM 
    nurses n
INNER JOIN 
    departments d ON n.department_id = d.department_id
WHERE 
    d.department_name = 'Pediatrics';
```

**Output:**

![image](https://github.com/user-attachments/assets/295588f2-686c-474e-ab71-b7cac01d57b2)


**Question 10**
```
Write the SQL query that achieves the selection of the "cust_name" and "city" columns from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column and a condition filtering for customers in the city 'London'.
For example:
Result
cust_name        city             ord_no           ord_date         purch_amt
---------------  ---------------  ---------------  ---------------  ----------
Brad Guzan       London           70009            2012-09-10       270.65
Julian Green     London           70012            2012-06-27       250.45
```

```sql
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
WHERE 
    c.city = 'London';
```

**Output:**

![image](https://github.com/user-attachments/assets/fecb7580-f28d-4478-8c44-5484443a26b1)



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
![image](https://github.com/user-attachments/assets/477add74-4e46-4782-98d2-01d36e625800)
