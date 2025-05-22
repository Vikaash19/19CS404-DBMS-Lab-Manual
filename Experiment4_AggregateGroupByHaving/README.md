# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
```
Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count. 
Note: Inventory attribute contains amount of fruits
Table: fruits
name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
For example:
Result
total_available_amount
----------------------
160
```

```sql
select  sum(inventory) as total_available_amount
from fruits
where price >0.5;
```

**Output:**

![image](https://github.com/user-attachments/assets/7dc6e06f-a6f8-4cd3-b45d-ca9aaeb6cdb1)


**Question 2**
```
Write a SQL query to find the average length of email addresses (in characters):
Table: customer
name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:
Result
avg_email_length
----------------
15.0
```

```sql
select AVG(length(email)) as avg_email_length
from customer;
```

**Output:**

![image](https://github.com/user-attachments/assets/9359cd37-3713-454d-9184-29c8c697c827)


**Question 3**
```
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.
Sample table: employee
For example:
Result
city        Income
----------  ----------
Alaska      450000
Arizona     1000000
California  5300000
Florida     5350000
Georgia     250000
```

```sql
select city,sum(income) as Income
from employee
group by city
having sum(income)>200000;
```

**Output:**

![image](https://github.com/user-attachments/assets/48f33be8-8dd2-42f0-becc-8395f01538fd)


**Question 4**
```
Write a SQL query to find the minimum purchase amount.
Sample table: orders
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
For example:
Result
MINIMUM
----------
65.26
```

```sql
select min(purch_amt) as "MINIMUM"
from orders;
```

**Output:**

![image](https://github.com/user-attachments/assets/ccbd9126-09a2-4de5-ab01-239b87175c41)


**Question 5**
```
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.
Sample table: orders
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
For example:
Result
COUNT
----------
6
```

```sql
select count(DISTINCT salesman_id)as COUNT
from orders;
```

**Output:**

![image](https://github.com/user-attachments/assets/4c611f1b-3476-4072-a2b3-863c47483fe0)


**Question 6**
```
Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.
Table: employee
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:
Result
age_difference
--------------
13
```

```sql
select MAX(age)-MIN(age) as age_difference
from employee;
```

**Output:**

![image](https://github.com/user-attachments/assets/10f894d3-7dc6-49ac-a3cf-b62c8970f5e7)


**Question 7**
```
Write a SQL query to find the customer with longest name?
Table: customer
name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:
Result
name          length
------------  ----------
Preeti Patel  12
```

```sql
select name,LENGTH(name) as length
from customer
order by length(name) DESC LIMIT 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/a73e845c-6f84-468f-8c3c-8d2ec5f3ee74)


**Question 8**
```
How many appointments are scheduled in each hour of the day?
Sample table:Appointments Table
name                              type
--------------------          ----------
AppointmentID               INTEGER
PatientID                         INTEGER
DoctorID                         INTEGER
AppointmentDateTime   DATETIME
Purpose                           TEXT
Status                              TEXT     
For example:
Result
HourOfDay   TotalAppointments
----------  -----------------
09          2
10          5
11          1
14          1
16          1
```

```sql
select strftime('%H',AppointmentDateTime)as HourOfDay,count(*) as TotalAppointments
from Appointments
group by HourOfDay
order by HourOfDay;
```

**Output:**

![image](https://github.com/user-attachments/assets/c735de9a-6845-49bb-8860-32289194cf87)


**Question 9**
```
How many appointments are scheduled for each patient?
Sample table: Appointments Table
name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT
For example:
Result
PatientID   TotalAppointments
----------  -----------------
3           3
5           2
6           1
7           1
10          3
```

```sql
select PatientID,count(*) as TotalAppointments
from Appointments
group by PatientID
```

**Output:**

![image](https://github.com/user-attachments/assets/2170ab58-50bc-4be4-a09f-f6d294dac9fd)


**Question 10**
```
What is the average dosage prescribed for each medication?
Sample tablePrescriptions Table
For example:
Result
Medication     AvgDosage
-------------  ----------
Ciprofloxacin  500.0
Doxorubicin    60.0
Ibuprofen      400.0
Levothyroxine  50.0
Lisinopril     10.0
MMR            0.5
Pending        0.0
Prenatal vita  1.0
Sertraline     50.0
Topiramate     25.0
```

```sql
select Medication,avg(Dosage) as AvgDosage
from Prescriptions
group by Medication;
```

**Output:**

![image](https://github.com/user-attachments/assets/78dc03aa-41b0-43b5-81a7-59618e732042)



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
![image](https://github.com/user-attachments/assets/174819eb-0831-4464-ab9e-3a0cd2877976)
