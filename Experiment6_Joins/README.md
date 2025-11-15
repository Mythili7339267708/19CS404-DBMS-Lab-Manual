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

![image](https://github.com/user-attachments/assets/4f78d592-4cfe-4f84-be5f-8b406024e4d1)


```sql
    SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/75765b55-342f-41d6-9c62-9017959bf514)


**Question 2**

![image](https://github.com/user-attachments/assets/d0dfca95-c8e1-4bed-95d9-daab884007ee)


```sql
   SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name,
    s.commission
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
LEFT JOIN 
    salesman s ON o.salesman_id = s.salesman_id
```

**Output:**

![image](https://github.com/user-attachments/assets/d8e557b2-98bd-42a6-a39e-d8d3ec134bd5)


**Question 3**

![image](https://github.com/user-attachments/assets/bf2bebd0-fe95-40fe-9910-0af7047defed)


```sql
 SELECT s.*
FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id
WHERE c.cust_name = 'Fabian Johns';
```

**Output:**

![image](https://github.com/user-attachments/assets/dc736dbe-f86b-4b04-a526-6dd88c4a6297)


**Question 4**

![image](https://github.com/user-attachments/assets/3c0bb25f-28d4-4068-8307-e687eebf5050)


```sql
 SELECT s.name AS Salesman, c.cust_name, s.city
FROM salesman s
JOIN customer c ON s.city = c.city;

```

**Output:**

![image](https://github.com/user-attachments/assets/3be03473-dcff-45cc-b6d7-3eae42afa542)


**Question 5**

![image](https://github.com/user-attachments/assets/dcc296ab-657f-463d-b122-1d305c1292de)


```sql
 SELECT s.name
FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id
WHERE c.city = 'London';


```

**Output:**

![image](https://github.com/user-attachments/assets/6d624480-77a9-44c6-aa5b-f285c19f8ed9)

**Question 6**

![image](https://github.com/user-attachments/assets/8a43eb8c-2b97-410f-a678-3a69a2cc57d6)


```sql
SELECT c.cust_name as 'Customer Name', c.city, s.name AS Salesman, s.commission
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;

```

**Output:**

![image](https://github.com/user-attachments/assets/37a567ec-241d-47d3-ac0f-eae2d17f0872)


**Question 7**

![image](https://github.com/user-attachments/assets/6f7ca644-5836-4ac1-b585-c1e16760134d)


```sql
    SELECT 
    customer.cust_name, 
    customer.city , 
    customer.grade, 
    salesman.name AS Salesman , 
    salesman.city
FROM 
    customer
JOIN 
    salesman ON customer.salesman_id = salesman.salesman_id
WHERE 
    customer.grade < 300
ORDER BY 
    customer.customer_id ASC;

```

**Output:**

![image](https://github.com/user-attachments/assets/a428646b-c0ae-44fa-829a-4bc81998caf9)


**Question 8**

![image](https://github.com/user-attachments/assets/e7fb6204-dfb5-4cfa-9ff0-e77543a8ec75)


```sql
    SELECT 
    patients.first_name, 
    patients.last_name
FROM 
    patients
INNER JOIN 
    surgeries ON patients.patient_id = surgeries.patient_id
WHERE 
    surgeries.surgery_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**

![image](https://github.com/user-attachments/assets/feba59f5-d275-4be3-832f-ff3a1ef41d54)


**Question 9**

![image](https://github.com/user-attachments/assets/5be58ba6-a89a-4bc1-bdb3-1bf7baf10025)


```sql
    SELECT 
    patients.admission_date, 
    surgeries.surgery_date
FROM 
    patients
INNER JOIN 
    surgeries ON patients.patient_id = surgeries.patient_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/3e8304fb-3c7c-4eb9-b7c7-59066c54ed7d)


**Question 10**

![image](https://github.com/user-attachments/assets/6bb57c0d-a0a5-40ac-941d-ceae6c6d01ea)


```sql
    SELECT 
    n.*, 
    d.department_name
FROM 
    nurses AS n
INNER JOIN 
    departments AS d ON n.department_id = d.department_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/6148cc1c-8d66-4a17-bc10-6170f6dbf94f)



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
