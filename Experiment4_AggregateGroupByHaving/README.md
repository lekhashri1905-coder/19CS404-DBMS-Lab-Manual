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
--
<img width="1722" height="790" alt="image" src="https://github.com/user-attachments/assets/5b0e0cd3-f04f-4c90-9874-cb4c448a537c" />


```sql
SELECT Address, COUNT(*) AS TotalPatients
FROM Patients
GROUP BY Address
ORDER BY Address;
```

**Output:**

<img width="1552" height="828" alt="image" src="https://github.com/user-attachments/assets/cf925e37-7d36-4bfc-aa38-1239c5b3a63c" />


**Question 2**
---
<img width="1768" height="1070" alt="image" src="https://github.com/user-attachments/assets/64d2b9c6-2ecc-4c1e-abfa-b8875fc21180" />


```sql
SELECT PatientID, COUNT(*) AS TotalMedications
FROM Prescriptions
GROUP BY PatientID
ORDER BY PatientID;
```

**Output:**

<img width="1398" height="1420" alt="image" src="https://github.com/user-attachments/assets/25649bce-9d0e-41cf-9346-eeaa613528e4" />


**Question 3**
---
What is the average duration of insurance coverage for patients covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
StartDate          DATE
EndDate            DATE
For example:

Result
InsuranceCompany  AvgCoverageDurationDays
----------------  -----------------------
ABC Insurance     7.0
DEF Insurance     3.0
JKL Insurance     3.0
STU Insurance     3.0
VWX Insurance     3.0
XYZ Insurance     3.0
YZA Insurance     3.0


```sql
SELECT InsuranceCompany,
       AVG(CAST(strftime('%Y', EndDate) AS INTEGER) - CAST(strftime('%Y', StartDate) AS INTEGER)) AS AvgCoverageDurationDays
FROM Insurance
GROUP BY InsuranceCompany
ORDER BY InsuranceCompany;
```

**Output:**

<img width="1708" height="1230" alt="image" src="https://github.com/user-attachments/assets/6a2b9199-21e6-44b6-957a-91d4330ac682" />

**Question 4**
---
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city

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
avg_email_length_below_30
-------------------------
14.0


```sql
SELECT AVG(LENGTH(email)) AS avg_email_length_below_30
FROM customer
WHERE city = 'Mumbai'
  AND LENGTH(email) < 30;
```

**Output:**
<img width="1472" height="652" alt="image" src="https://github.com/user-attachments/assets/05301d0f-a31a-411c-aca4-0fdb3e542eb9" />


**Question 5**
---
Write a SQL query to find the shortest email address in the customer table?

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
name        email           min_email_length
----------  --------------  ----------------
Ravi Kumar  ravi@gmail.com  14


```sql
SELECT name,
       email,
       LENGTH(email) AS min_email_length
FROM customer
ORDER BY LENGTH(email) ASC
LIMIT 1;
```

**Output:**

<img width="1776" height="692" alt="image" src="https://github.com/user-attachments/assets/23afb5f7-cabe-41ea-99c5-ddf5df833b52" />


**Question 6**
---
<img width="1642" height="820" alt="image" src="https://github.com/user-attachments/assets/fc0f2d57-02e5-48da-8b0a-5428ecf0494a" />


```sql
SELECT COUNT(*) AS COUNT
FROM customer
WHERE city <> 'Noida';
```

**Output:**

<img width="1010" height="710" alt="image" src="https://github.com/user-attachments/assets/9291d1e5-24fc-4c35-8bfd-76abedcec37a" />


**Question 7**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?

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
price_diff
----------
4.65

```sql
SELECT MAX(price) - MIN(price) AS price_diff
FROM fruits;
```

**Output:**

<img width="1072" height="654" alt="image" src="https://github.com/user-attachments/assets/a3d5ebde-1279-4eac-b9fe-0edb199737d9" />

**Question 8**
---
<img width="1918" height="750" alt="image" src="https://github.com/user-attachments/assets/6ef6d1ed-ba31-4d2c-9738-6df98150b5fd" />


```sql
SELECT (age / 5) * 5 AS age_group,
       AVG(age)
FROM customer1
GROUP BY (age / 5) * 5
HAVING AVG(age) < 24;
```

**Output:**
<img width="1618" height="638" alt="image" src="https://github.com/user-attachments/assets/602f3663-1b83-4927-841c-d88244df70e3" />


**Question 9**
---
<img width="1922" height="930" alt="image" src="https://github.com/user-attachments/assets/e66e82eb-cee1-4b3c-ae66-9acfb4ff4771" />


```sql
SELECT jdate, MIN(workhour)
FROM employee1
GROUP BY jdate
HAVING MIN(workhour) < 10;
```

**Output:**

<img width="1338" height="772" alt="image" src="https://github.com/user-attachments/assets/542a444b-4c21-4075-b693-a876c6ae0559" />


**Question 10**
---
<img width="1794" height="898" alt="image" src="https://github.com/user-attachments/assets/25634e60-c2c4-46da-9aab-e576594a819c" />


```sql
SELECT occupation, SUM(workhour)
FROM employee1
GROUP BY occupation
HAVING SUM(workhour) > 20;
```

**Output:**

<img width="1486" height="940" alt="image" src="https://github.com/user-attachments/assets/f070cc1e-0b03-4d00-88b7-18c9bc6524f7" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
