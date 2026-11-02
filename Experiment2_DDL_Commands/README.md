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
Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           location     varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0  


```sql
Alter table customer RENAME city to location;

```
**Output:**

<img width="921" height="380" alt="image" src="https://github.com/user-attachments/assets/973de159-2eab-4a28-8f68-8f0973d94ead" />


**Question 2**
---
-- Paste Question 2 hereWrite a SQL query for adding a new column named "email" with the datatype VARCHAR(100) to the  table "customer" 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           email        VARCHAR(100)                       0   

```sql
alter table customer ADD email VARCHAR(100);
```
**Output:**

<img width="906" height="415" alt="image" src="https://github.com/user-attachments/assets/8d3291ce-c984-4b26-bdd8-a7f0023a03f9" />


**Question 3**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

For example:

Test	Result
select * from Customers;
CustomerID  Name             Address         Email
----------  ---------------  --------------  ---------------------
301         Michael Johnson  123 Elm Street  michael.j@example.com
302         Sarah Lee        456 Oak Avenue  sarah.lee@example.com
303         David Wilson     789 Pine Road   david.w@example.com


```sql
INSERT INTO Customers (CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email
FROM Old_customers;

```
**Output:**

<img width="906" height="346" alt="image" src="https://github.com/user-attachments/assets/c3bd7e55-4015-4474-8eb6-18b9d182fa4f" />


**Question 4**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
For example:

Test	Result
INSERT INTO Attendance (AttendanceID, EmployeeID, AttendanceDate, Status) VALUES (1, 1, '2024-08-01', 'Present');
SELECT * FROM Attendance;

```sql
CREATE TABLE Attendance (
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN ('Present', 'Absent', 'Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```
**Output:**

<img width="925" height="297" alt="image" src="https://github.com/user-attachments/assets/c8f092a2-6b43-4ef2-ae16-01c50b1c079d" />


**Question 5**
---
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

For example:

Test	Result
SELECT * FROM Customers WHERE CustomerID = 301;
CustomerID  Name            Address       City        ZipCode
----------  --------------  ------------  ----------  ----------
301         Michael Jordan  123 Maple St  Chicago     60616

```sql
INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES (301, 'Michael Jordan', '123 Maple St', 'Chicago', '60616');
```
**Output:**

<img width="1677" height="295" alt="image" src="https://github.com/user-attachments/assets/661b4c63-acba-49e4-8726-8970299a906b" />


**Question 6**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Error: FOREIGN KEY constraint faile

```sql
CREATE TABLE Shipments (
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1767" height="327" alt="image" src="https://github.com/user-attachments/assets/45e6ae3f-b8b8-4cd8-9880-a727fa1faead" />

**Question 7**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science
For example:

Test	Result
select * from Student_details;
RollNo      Name          Gender      Subject     MARKS
----------  ------------  ----------  ----------  ----------
205         Olivia Green  F
207         Liam Smith    M           Mathematic  85
208         Sophia Johns  F           Science

```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (205, 'Olivia Green', 'F', NULL, NULL);

INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (207, 'Liam Smith', 'M', 'Mathematics', 85);

INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (208, 'Sophia Johnson', 'F', 'Science', NULL);```
```
**Output:**

<img width="1397" height="327" alt="image" src="https://github.com/user-attachments/assets/d40a4eff-0153-4219-b947-a9dfec34eb3f" />

**Question 8**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint faile

```sql
CREATE TABLE ProjectAssignments (
    AssignmentID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**
<img width="1895" height="345" alt="image" src="https://github.com/user-attachments/assets/8f29a914-dc04-4aa2-a7ff-9244a8336755" />




**Question 9**
---
-- Paste Question 9 hereCreate a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
For example:

Test	Result
INSERT INTO Products (ProductID, ProductName, Price, StockQuantity) VALUES (1, 'Laptop', 999.99, 10);
select * from Products;
```sql
CREATE TABLE Products (
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT UNIQUE NOT NULL,
    Price REAL CHECK (Price > 0),
    StockQuantity INTEGER CHECK (StockQuantity >= 0)
);-- Paste your SQL code below for Question 9
```

**Output:**

<img width="1912" height="372" alt="image" src="https://github.com/user-attachments/assets/e7c354ef-02f9-4882-af01-32ea654ad8ee" />


**Question 10**
---
Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER
For example:

Test	Result
pragma table_info('Products');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     ProductID   INTEGER     0                       0
1     ProductNam  TEXT        0                       0
2     Price       REAL        0                       0
3     Stock       INTEGER     0                       0

```sql
CREATE TABLE Products (
    ProductID INTEGER,
    ProductName TEXT,
    Price REAL,
    Stock INTEGER
);
```

**Output:**



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
