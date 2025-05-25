# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
![image](https://github.com/user-attachments/assets/62350bae-ee70-45c3-8ded-24ec58d7d520)


```sql
SELECT student_name, grade
FROM GRADES g
WHERE grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);

```

**Output:**

![image](https://github.com/user-attachments/assets/6017b4a8-8cd5-4555-af0d-7cdc1506d94b)


**Question 2**
---
![image](https://github.com/user-attachments/assets/b189af73-6fa4-460f-8210-a0a138c42c1d)



```sql
SELECT * 
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';

```

**Output:**

![image](https://github.com/user-attachments/assets/5b62ff0b-19f1-4748-96ad-a7ddcb76dd3b)


**Question 3**
---
![image](https://github.com/user-attachments/assets/6d6c749d-da00-4642-b2d9-783ba0cbb1bd)


```sql
SELECT *
FROM customer
WHERE customer_id = (
    SELECT salesman_id - 2001
    FROM salesman
    WHERE name = 'Mc Lyon'
);

```

**Output:**

![image](https://github.com/user-attachments/assets/acd1c824-fe4e-4abe-ad96-7623df880f72)


**Question 4**
---
![image](https://github.com/user-attachments/assets/1033dbcd-7f77-4907-b1f5-4fbee18ba6c1)


```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```

**Output:**

![image](https://github.com/user-attachments/assets/1e8b7c54-a0d9-4388-958a-5f6cf14b3f0f)


**Question 5**
---
![image](https://github.com/user-attachments/assets/7a21c256-5c03-41ee-9ce1-8ad59ea0dd40)


```sql
SELECT * 
FROM CUSTOMERS
WHERE AGE < 30;

```

**Output:**

![image](https://github.com/user-attachments/assets/7f58e9cc-dcfa-432c-9113-14228f100de4)


**Question 6**
---
![image](https://github.com/user-attachments/assets/7251367a-46ae-4bfc-ba5c-13915b0ab8cb)


```sql
SELECT *
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);

```

**Output:**

![image](https://github.com/user-attachments/assets/7a212c23-a394-4b91-acb3-2a73986579ae)

**Question 7**
---
![image](https://github.com/user-attachments/assets/ded22bf2-072a-4676-92ac-0cc4b176eafb)


```sql
SELECT * 
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';

```

**Output:**

![image](https://github.com/user-attachments/assets/81677a32-859d-4197-b891-bd1c9be9956e)


**Question 8**
---
![image](https://github.com/user-attachments/assets/dd2e7ca7-b0a9-4530-946a-7841df24c03c)


```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM orders
    WHERE ord_date = '2012-10-10'
);

```

**Output:**

![image](https://github.com/user-attachments/assets/d37cc7d0-7bc9-4117-9be4-5348dc45306b)


**Question 9**
---
![image](https://github.com/user-attachments/assets/edca934a-44f0-4fee-bb02-80813cbf8ee7)


```sql
SELECT 
    ord_no,
    purch_amt,
    ord_date,
    customer_id,
    salesman_id
FROM 
    orders
WHERE 
    salesman_id = (
        SELECT salesman_id
        FROM salesman
        WHERE name = 'Paul Adam'
    );

```

**Output:**

![image](https://github.com/user-attachments/assets/454533d4-2f1e-4193-b114-e9856ba6826d)

**Question 10**
---
![image](https://github.com/user-attachments/assets/efd06b1e-61f0-4b72-8334-c71a9eb5d15e)


```sql
SELECT medication_id AS medic, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MAX(dosage)
    FROM Medications
);


```

**Output:**

![image](https://github.com/user-attachments/assets/e4ab611a-4e84-442b-be02-32a4b32f7601)



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
