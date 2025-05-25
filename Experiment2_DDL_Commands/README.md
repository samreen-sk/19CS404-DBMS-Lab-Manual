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
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

For example:

##### Test	
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;

##### Result
job_id      job_title          min_salary  max_salary
----------  -----------------  ----------  ----------
1           Software Engineer  9000        15000

#### Code:

```
CREATE TABLE jobs
(
    job_id INTEGER PRIMARY KEY,
    job_title VARCHAR(255) DEFAULT '',
    min_salary INTEGER DEFAULT 8000,
    max_salary INTEGER DEFAULT NULL
);
```
**Output:**

![image](https://github.com/user-attachments/assets/0263e409-c43f-43ed-850a-15294dd76296)


**Question 2**
---
Create a table named Employees with the following columns:
```
EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE
For example:
```
##### Test	
pragma table_info('Employees');

##### Result
```
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     EmployeeID  INTEGER     0                       0
1     FirstName   TEXT        0                       0
2     LastName    TEXT        0                       0
3     HireDate    DATE        0                       0
```

#### Code:

```
CREATE TABLE Employees
(
    EmployeeID INTEGER,
    FirstName TEXT,
    LastName TEXT,
    HireDate DATE
);
```

**Output:**

![image](https://github.com/user-attachments/assets/ef4dbe13-c4e3-4ed6-8bbd-0c4af732eb8e)

**Question 3**
---
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

For example:

##### Test	
SELECT * FROM Student_details WHERE RollNo = 201;
##### Result
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
201         David Lee   M           Physics     92

#### Code:
```
INSERT INTO Student_details(RollNo,Name,Gender,Subject,MARKS)
VALUES (201,'David Lee','M','Physics',92)
```

**Output:**
![image](https://github.com/user-attachments/assets/2684010b-c94b-474f-aad1-95f7ef9bedbe)



**Question 4**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
For example:

##### Test	
-- Attempt to insert a record with NULL FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);
##### Result
Error: NOT NULL constraint failed: Employees.FirstName

#### Code:
```
CREATE TABLE Employees
(
    EmployeeID INTEGER PRIMARY KEY,
    FirstName VARCHAR(30) NOT NULL,
    LastName VARCHAR(30) NOT NULL,
    Email VARCHAR(255) UNIQUE,
    Salary DECIMAL(10,2) CHECK (Salary>0),
    DepartmentID INTEGER,
    FOREIGN KEY(DepartmentID) REFERENCES Departments(DepartmentID)
);
```
**Output:**

![image](https://github.com/user-attachments/assets/f7f4bded-69e5-44c1-82aa-6a8b5a6586b1)

**Question 5**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science
For example:

##### Test	
select * from Student_details;
##### Result
RollNo      Name          Gender      Subject     MARKS
----------  ------------  ----------  ----------  ----------
205         Olivia Green  F
207         Liam Smith    M           Mathematic  85
208         Sophia Johns  F           Science

#### Code:
```
INSERT INTO Student_details(RollNo,Name,Gender,Subject,MARKS)
VALUES (205,'Olivia Green','F',NULL,NULL);
INSERT INTO Student_details(RollNo,Name,Gender,Subject,MARKS)
VALUES (207,'Liam Smith','M','Mathematics',85);
INSERT INTO Student_details(RollNo,Name,Gender,Subject,MARKS)
VALUES (208,'Sophia Johnson','F','Science',NULL);
```

**Output:**

![image](https://github.com/user-attachments/assets/24bce137-54ba-4ec9-8deb-b9ec2abf73dd)


**Question 6**
Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

##### Test	
pragma table_info('Student_details');
##### Result
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           Country     TEXT        0                       0

#### Code:
```
ALTER TABLE Student_details 
ADD COLUMN Country TEXT;
```

**Output:**

![image](https://github.com/user-attachments/assets/17acb212-0167-4443-a62c-1bc8a1201fb2)


**Question 7**
---
Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

For example:

##### Test	
pragma table_info('employee');
##### Result
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           designatio  varchar(50  0                       0

#### Code:
```
ALTER TABLE employee
ADD COLUMN designation varchar(50);
```

**Output:**

![image](https://github.com/user-attachments/assets/63049dfe-34e6-4bd4-aad5-14f08e217359)


**Question 8**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

##### Test	
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
##### Result
Error: UNIQUE constraint failed: Invoices.InvoiceID

#### Code:
```
CREATE TABLE Invoices
(
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    DueDate DATE CHECK (DueDate > InvoiceDate),
    Amount REAL CHECK (Amount>0)
);
```
**Output:**

![image](https://github.com/user-attachments/assets/503412c7-22c0-4f5b-9f44-2a2d8160a4d0)


**Question 9**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
For example:

##### Test	
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;
##### Result
OrderID     OrderDate   CustomerID
----------  ----------  ----------
1           2024-08-01  1
#### Code:
```
CREATE TABLE Orders
(
    OrderID INTEGER PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```
**Output:**

![image](https://github.com/user-attachments/assets/6a4ef27b-0633-4299-912a-4c089902eb47)


**Question 10**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

For example:

##### Test	
select * from Customers;
##### Result
CustomerID  Name             Address         Email
----------  ---------------  --------------  ---------------------
301         Michael Johnson  123 Elm Street  michael.j@example.com
302         Sarah Lee        456 Oak Avenue  sarah.lee@example.com
303         David Wilson     789 Pine Road   david.w@example.com

#### Code:
```
INSERT INTO Customers(CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email
FROM Old_customers;
```
**Output:**

![image](https://github.com/user-attachments/assets/687876de-d64d-4d71-8d32-d6030629c06b)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
