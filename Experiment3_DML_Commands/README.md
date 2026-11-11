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
For example:

Test	Result
SELECT*FROM Products WHERE supplier_id = 10;
product_id  product_name      category    cost_price  sell_price  reorder_lvl  quantity    supplier_id
----------  ----------------  ----------  ----------  ----------  -----------  ----------  -----------
6           Detergent Powder  Snacks      60          80          20           40          10
7           Surf Excel Deter  Snacks      85          100         10           40          10
8           Detergent Ariel   Items       85          100         10           40          10
product_id  product_name      category    cost_price  sell_price  reorder_lvl  quantity    supplier_id
----------  ----------------  ----------  ----------  ----------  -----------  ----------  -----------
6           Detergent Powder  Snacks      60          81          20           40          10
7           Surf Excel Deter  Snacks      85          114         10           40          10
8           Detergent Ariel   Items       85          114         10           40          10


```sql
UPDATE Products
SET sell_price = CAST(cost_price * 1.35 AS INTEGER)
WHERE (sell_price - cost_price) / sell_price < 0.30;
```

**Output:**

<img width="1848" height="958" alt="image" src="https://github.com/user-attachments/assets/1909c846-3a6c-4e14-b6b7-cb4b334ef38d" />


**Question 2**
---
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id


```sql
UPDATE Products
SET reorder_lvl = 20
WHERE quantity < 10 AND category = 'Snacks';
```

**Output:**

<img width="1876" height="1070" alt="image" src="https://github.com/user-attachments/assets/40e1c0f8-8580-4216-9ce6-8e40fa65b3e0" />


**Question 3**
---
Update the 'Selling_Price' to add 10% extra margin for all products supplied by the supplier with id 6.

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
For example:

Test	Result
select changes();
changes()
----------


```sqlUPDATE Products
SET sell_price = ROUND(sell_price * 1.10)
WHERE supplier_id = 6;
```

**Output:**

<img width="1852" height="976" alt="image" src="https://github.com/user-attachments/assets/7ad7a136-22e8-4254-aeca-dff6bc1e4444" />


**Question 4**
---
Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
UPDATE Products
SET quantity = quantity * 1.10;
```

**Output:**
<img width="1896" height="1096" alt="image" src="https://github.com/user-attachments/assets/02445d1e-990a-4855-b969-e8b6b23469ff" />


**Question 5**
---
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.



For example:

Test	Result
select changes();
changes()
----------
2


```sql
UPDATE purchases
SET per_unit_price = 25,
    total_price = 25 * quantity
WHERE purchase_date = '2022-08-15'
  AND product_id = 12;
```

**Output:**

<img width="1874" height="970" alt="image" src="https://github.com/user-attachments/assets/5a15426a-bfb5-4c87-801e-671901c01294" />


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
DELETE FROM customer
WHERE CUST_CITY <> 'New York'
AND OUTSTANDING_AMT > 5000;
```

**Output:**

<img width="1986" height="1076" alt="image" src="https://github.com/user-attachments/assets/86477c02-e24d-4686-ba3f-0a5097e92221" />


**Question 7**
---Write a SQL query to Delete customers with following conditions

'CUST_COUNTRY' is not in a list of specified countries ('UK', 'USA', 'Canada')
'GRADE' is greater than or equal to 3
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



```sql
DELETE FROM customer
WHERE CUST_COUNTRY NOT IN ('UK', 'USA', 'Canada')
AND GRADE >= 3;
```

**Output:**

<img width="1830" height="808" alt="image" src="https://github.com/user-attachments/assets/3343929b-3445-4f1a-83fb-202461dffbf7" />

**Question 8**
---
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

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
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology

```sql
DELETE FROM doctors
WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**

<img width="1866" height="1354" alt="image" src="https://github.com/user-attachments/assets/793445c6-f3a9-44ee-9ab0-6518b6271fe6" />


**Question 9**
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
Answer:(penalty regime: 0 %)



```sql
DELETE FROM customer
WHERE AGENT_CODE IN ('A003', 'A008');
```

**Output:**

<img width="1702" height="1338" alt="image" src="https://github.com/user-attachments/assets/8c62af9e-28d9-4697-9b07-6d87831109d2" />


**Question 10**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select distinct(grade)from customer;
GRADE
----------
2
3
1
0
GRADE
----------
2
3


```sql
DELETE FROM customer
WHERE GRADE < 2;
```

**Output:**

<img width="1598" height="1092" alt="image" src="https://github.com/user-attachments/assets/f2b57f57-a5af-463a-9bd3-d2eecfc85f0e" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
