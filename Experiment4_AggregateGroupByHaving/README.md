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
![image](https://github.com/user-attachments/assets/68e58038-a741-45d1-a259-d29bdb59f69c)


```sql
SELECT PatientID, COUNT(AppointmentID) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;

```

**Output:**

![image](https://github.com/user-attachments/assets/632f0877-d7d2-4120-86cf-0439fdf5d77b)


**Question 2**
---
![image](https://github.com/user-attachments/assets/6f062c88-3538-4b00-9f11-8f3e438651b1)

```sql
SELECT DoctorID, COUNT(AppointmentID) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;

```

**Output:**

![image](https://github.com/user-attachments/assets/f8d33eca-2751-47cb-b4a5-e9718385235a)


**Question 3**
---
![image](https://github.com/user-attachments/assets/6d4130f1-346f-4c35-9b94-62099c20a25c)


```sql
SELECT 
    strftime('%Y-%m', Date) AS Month, 
    COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY Month
ORDER BY Month;

```

**Output:**

![image](https://github.com/user-attachments/assets/269d0736-b734-4501-80e8-1f45114d4468)


**Question 4**
---
![image](https://github.com/user-attachments/assets/f2e9986d-1edb-4664-9ba3-8c01b8f8919c)


```sql
SELECT COUNT(DISTINCT city) AS unique_cities
FROM customer;

```

**Output:**

![image](https://github.com/user-attachments/assets/665171d0-ab99-4ccc-b514-1aa95a6de054)


**Question 5**
---
![image](https://github.com/user-attachments/assets/34b2a0f1-5629-4b94-a1aa-90e0fac7725d)


```sql
SELECT MIN(purch_amt) AS MINIMUM
FROM orders;

```

**Output:**

![image](https://github.com/user-attachments/assets/925ad7fc-794f-4aa7-a6b8-058bbc612936)


**Question 6**
---
![image](https://github.com/user-attachments/assets/6f671b6d-bc60-4050-b0de-b4b626452f14)


```sql
SELECT name AS fruit_name, inventory AS lowest_quantity
FROM fruits
ORDER BY inventory ASC
LIMIT 1;

```

**Output:**

![image](https://github.com/user-attachments/assets/8dd7e262-6827-40f3-8500-edcc12548c9e)


**Question 7**
---
![image](https://github.com/user-attachments/assets/13af30c7-9381-4a75-b4e5-3dfde53791ba)


```sql
SELECT name, email, LENGTH(email) AS min_email_length
FROM customer
ORDER BY LENGTH(email)
LIMIT 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/b7c90a6e-af14-4fc3-ae3d-cb1b28c27f89)


**Question 8**
---
![image](https://github.com/user-attachments/assets/ae18f9e1-9fb7-4183-b9ce-246d9317e270)


```sql
SELECT jdate, MAX(workhour) AS "MAX(workhour)"
FROM employee1
GROUP BY jdate
HAVING MAX(workhour) > 12;

```

**Output:**

![image](https://github.com/user-attachments/assets/70898768-0e58-4ad2-8c63-a0137b95b5b0)


**Question 9**
---
![image](https://github.com/user-attachments/assets/e8b27a46-f5a6-4b0b-88c9-fbc8e5309b4e)


```sql
SELECT PatientID, COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID
HAVING COUNT(*) > 3;

```

**Output:**

![image](https://github.com/user-attachments/assets/a6805be7-ca31-4862-9f04-7d4c7756441e)


**Question 10**
---
![image](https://github.com/user-attachments/assets/26c8918e-bd4f-4118-ba31-9a7c63655733)


```sql
SELECT (age / 5) * 5 AS age_group, AVG(age) AS "AVG(age)"
FROM customer1
GROUP BY age_group
HAVING AVG(age) < 24;

```

**Output:**

![image](https://github.com/user-attachments/assets/913fddd5-8ffc-49a0-9db7-8fb0f2407a67)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
