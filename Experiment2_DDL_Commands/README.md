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
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
```sql
CREATE TABLE Bonuses (
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK (BonusAmount > 0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1302" height="287" alt="image" src="https://github.com/user-attachments/assets/2aaf0ed7-8486-452e-bbb2-612b705d45d6" />

**Question 2**
---
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT

```sql
CREATE TABLE Locations (
    LocationID INTEGER,
    LocationName TEXT,
    Address TEXT
);
```

**Output:**
<img width="1298" height="357" alt="image" src="https://github.com/user-attachments/assets/ee1f644b-eaf9-4139-b53c-3a8e3ce5196a" />

**Question 3**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```sql
CREATE TABLE Invoices (
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK (Amount > 0),
    DueDate DATE,
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    CHECK (DueDate > InvoiceDate)
);
```

**Output:**
<img width="1301" height="280" alt="image" src="https://github.com/user-attachments/assets/9434ebf3-0f2a-46b5-8b24-06461ae58c1b" />


**Question 4**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email
```sql
INSERT INTO Customers (CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email
FROM Old_customers;
```

**Output:**
<img width="1256" height="273" alt="image" src="https://github.com/user-attachments/assets/e59181a1-06f7-463d-aaae-a2dc523459f1" />


**Question 5**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
```sql
CREATE TABLE item (
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
<img width="1292" height="312" alt="image" src="https://github.com/user-attachments/assets/c5159af2-797e-4651-b6dd-aaa3846b5364" />


**Question 6**
---
Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.


```sql
INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES ('001', 'Sarah Parker', 'Manager', 'HR', 60000);
```

**Output:**

<img width="1296" height="233" alt="image" src="https://github.com/user-attachments/assets/af0fdbe8-5531-4dbc-975f-ab20e0885142" />

**Question 7**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
CREATE TABLE jobs (
    job_id INTEGER PRIMARY KEY,
    job_title TEXT DEFAULT '',
    min_salary INTEGER DEFAULT 8000,
    max_salary INTEGER DEFAULT NULL
);
```

**Output:**

<img width="1296" height="307" alt="image" src="https://github.com/user-attachments/assets/5188c35e-53cc-4405-9bc7-169b7956ac2b" />

**Question 8**
---
Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type             notnu  dflt_value  pk
---------------  ---------------  ---------------  -----  ----------  ----------
0                RollNo           int              0                  1
1                Name             VARCHAR(100)     1                  0
2                Gender           TEXT             1                  0
3                Subject          VARCHAR(30)      0                  0
4                MARKS            INT (3)          0                  0
```sql
ALTER TABLE Student_details
ADD COLUMN Mobilenumber number;
```

**Output:**

<img width="1305" height="332" alt="image" src="https://github.com/user-attachments/assets/1937842e-563c-41e9-9c3a-8712d9fa668c" />

**Question 9**
---
In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
```sql
-- Record with some fields as NULL
INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES (5, 'George Clark', 'Consultant', NULL, NULL);

-- Record with all fields filled
INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES (7, 'Noah Davis', 'Manager', 'HR', 60000);

-- Record with some fields filled, others NULL
INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES (8, 'Ava Miller', 'Consultant', 'IT', NULL);
```

**Output:**

<img width="1216" height="261" alt="image" src="https://github.com/user-attachments/assets/6ce7042d-cf14-4533-b7e9-9ccdac32c99b" />

**Question 10**
---
Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
```sql
ALTER TABLE Student_details
ADD COLUMN Country TEXT;
```

**Output:**

<img width="1298" height="328" alt="image" src="https://github.com/user-attachments/assets/fca6dbc0-c9f1-4f93-acd4-9e89751e2ebb" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
