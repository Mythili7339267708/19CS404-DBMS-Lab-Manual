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
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```
CREATE TABLE item(
item_id TEXT primary key,
item_desc TEXT not null,
rate INTEGER not null,
icom_id TEXT CHECK(length(icom_id)=4),
FOREIGN KEY (icom_id)
 REFERENCES company(com_id)
 ON UPDATE SET null
 ON DELETE SET null);

```

**Output:**

<img width="1263" height="324" alt="image" src="https://github.com/user-attachments/assets/603ab505-778d-4ee0-b699-25ccb3a185cd" />


**Question 2**
--
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```
INSERT INTO Books(ISBN, Title,Author, Publisher, YearPublished)
SELECT ISBN, Title,Author, Publisher, YearPublished
FROM Out_of_print_books;

```

**Output:**


<img width="1132" height="207" alt="image" src="https://github.com/user-attachments/assets/1084b5a9-ef7b-4cbd-ac9e-5e766bf75c2d" />


**Question 3**
--
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

```
CREATE TABLE Products(
ProductID primary key,
ProductName TEXT not null,
Price REAL CHECK(Price>0),
Stock INTEGER CHECK(Stock>=0));
```

**Output:**


<img width="1362" height="309" alt="image" src="https://github.com/user-attachments/assets/4dd01eac-d418-43e8-b4a4-a6036277fe21" />


**Question 4**
--
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```
CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT);
```

**Output:**


<img width="1491" height="327" alt="image" src="https://github.com/user-attachments/assets/7186e6e4-3597-4656-90a6-462dc405e28c" />


**Question 5**
--
Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

```
ALTER TABLE customer
RENAME COLUMN city TO location;
```

**Output:**


<img width="1583" height="286" alt="image" src="https://github.com/user-attachments/assets/c2a09b46-9ea6-45f7-94dd-359872a14651" />


**Question 6**
--
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER primary key,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE not null,
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID));
```

**Output:**


<img width="1587" height="235" alt="image" src="https://github.com/user-attachments/assets/af81c7bd-76ed-4f73-b104-85458abc4aa3" />


**Question 7**
--
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

```
INSERT INTO Products(ProductID, Name, Category, Price, Stock)
VALUES (101, 'Laptop', 'Electronics', 1500, 50);
```

**Output:**


<img width="1223" height="213" alt="image" src="https://github.com/user-attachments/assets/a80b30a0-11f1-4d95-9012-ad6cc4c3d72f" />


**Question 8**
--
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100

```
INSERT INTO Products(ProductID, Name, Category, Price, Stock)
VALUES 
 (106, 'Fitness Tracker', 'Wearables', NULL, NULL),
 (107, 'Laptop', 'Electronic', 999.99, 50),
 (108, 'Wireless Earbud', 'Accessorie', NULL, 100);
```

**Output:**


<img width="1181" height="243" alt="image" src="https://github.com/user-attachments/assets/1cbf2057-972f-470b-9991-d3072e29ae8d" />


**Question 9**
--
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```
CREATE TABLE contacts(
contact_id INTEGER primary key,
first_name TEXT not null,
last_name TEXT not null,
email TEXT,
phone TEXT not null CHECK(length(phone)>=10));
```

**Output:**


<img width="1287" height="190" alt="image" src="https://github.com/user-attachments/assets/b896ed5e-348f-42a9-8522-62b1846d057e" />


**Question 10**
--
Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies.

```
ALTER TABLE Companies
RENAME COLUMN name TO first_name;

ALTER TABLE Companies
ADD COLUMN mobilenumber number;
ALTER TABLE Companies
ADD COLUMN DOB Date;
ALTER TABLE Companies
ADD COLUMN State varchar(30);

```

**Output:**


<img width="1292" height="332" alt="image" src="https://github.com/user-attachments/assets/9046da0c-0be6-489f-90e9-9ad0466e5bc6" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
