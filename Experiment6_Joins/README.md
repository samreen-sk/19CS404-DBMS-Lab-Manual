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
--
```
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
cust_name        city             grade            Salesman         city
---------------  ---------------  ---------------  ---------------  ----------
Brad Guzan       London           100              Pit Alex         London
Nick Rimando     Chennai          100              Bob Emily        New York
Jozy Altidore    Moscow           200              Paul Adam        Rome
Graham Zusi      California       200              Nail Knite       Paris
Brad Davis       New York         200              Bob Emily        New York
Geoff Cameron    Berlin           100              Lauson Hen       San Jose
```



```sql
-- select c.cust_name,c.city,c.grade,s.name as Salesman, s.city
from customer c
join salesman s on s.salesman_id = c.salesman_id
where c.grade < 300
order by c.customer_id asc;
```

**Output:**

![image](https://github.com/user-attachments/assets/25eab665-d75e-47d9-b15f-ffe47660695e)


**Question 2**
```
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date between '2012-08-01' and '2012-08-30'.
```

![image](https://github.com/user-attachments/assets/1ce783e4-a9a7-40b0-9f60-b0014ab58f92)
```
For example:

Result
customer_id      cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
3009             Geoff Cameron    Berlin           100              5003
3003             Jozy Altidore    Moscow           200              5007

```
```sql
select c.customer_id , c.cust_name, c.city, c.grade, o.salesman_id
from CUSTOMER c
left join ORDERS o on c.customer_id = o.customer_id
where o.ord_date between '2012-08-01' and '2012-08-30';
```

**Output:**

![image](https://github.com/user-attachments/assets/8f87aa25-0607-4519-a252-0d4a37efa9cc)


**Question 3**
```
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
cust_name        city             grade            Salesman         city
---------------  ---------------  ---------------  ---------------  ----------
Brad Guzan       London           100              Pit Alex         London
Nick Rimando     Chennai          100              Bob Emily        New York
Jozy Altidore    Moscow           200              Paul Adam        Rome
Fabian Johns     Paris            300              Mc Lyon          Paris
Graham Zusi      California       200              Nail Knite       Paris
Brad Davis       New York         200              Bob Emily        New York
Julian Green     London           300              Nail Knite       Paris
Geoff Cameron    Berlin           100              Lauson Hen       San Jose

```

```sql
select c.cust_name, c.city,c.grade,s.name as Salesman,s.city
from customer c
join salesman s on s.salesman_id = c.salesman_id
order by customer_id asc;
```

**Output:**

![image](https://github.com/user-attachments/assets/4fc8e72b-3458-4948-aad9-ecef91cb16bc)



**Question 4**
```
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)

For example:

Result
patient_name     Doctor_speciali
---------------  ---------------
Alice            Cardiology

```

```sql
select p.first_name as patient_name , d.specialization as Doctor_specialization
from PATIENTS P
INNER JOIN DOCTORS d on p.doctor_id = p.doctor_id 
where p.admission_date between '2024-01-01' and '2024-01-31'
group by patient_name; 
```

**Output:**

![image](https://github.com/user-attachments/assets/00d5c340-a1aa-41fc-94cf-c88bd0daa398)


**Question 5**
```
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
For example:

Result
ord_no           purch_amt        cust_name        city
---------------  ---------------  ---------------  ---------------
70007            948.5            Graham Zusi      California
70010            1983.43          Fabian Johns     Paris
```

```sql
select o.ord_no, o.purch_amt,c.cust_name,c.city
from orders o
join customer c on c.customer_id = o.customer_id
where o.purch_amt between 500 and 2000;
```

**Output:**

![image](https://github.com/user-attachments/assets/15d0e5d6-2f80-4f25-a65b-a24a26839f22)


**Question 6**
```
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table : salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
ord_no           purch_amt        ord_date         cust_name        customer_city  grade       salesman_name  salesman_city  commission
---------------  ---------------  ---------------  ---------------  -------------  ----------  -------------  -------------  ----------
70001            150.5            2012-10-05       Graham Zusi      California     200         Nail Knite     Paris          0.13
70009            270.65           2012-09-10       Brad Guzan       London         100         Pit Alex       London         0.11
70002            65.26            2012-10-05       Nick Rimando     Chennai        100         Bob Emily      New York       0.15
70004            110.5            2012-08-17       Geoff Cameron    Berlin         100         Lauson Hen     San Jose       0.12
70007            948.5            2012-09-10       Graham Zusi      California     200         Nail Knite     Paris          0.13
70005            2400.6           2012-07-27       Brad Davis       New York       200         Bob Emily      New York       0.15
70008            5760.0           2012-09-10       Nick Rimando     Chennai        100         Bob Emily      New York       0.15
70010            1983.43          2012-10-10       Fabian Johns     Paris          300         Mc Lyon        Paris          0.14
70003            2480.4           2012-10-10       Geoff Cameron    Berlin         100         Lauson Hen     San Jose       0.12
70012            250.45           2012-06-27       Julian Green     London         300         Nail Knite     Paris          0.13
70011            75.29            2012-08-17       Jozy Altidore    Moscow         200         Paul Adam      Rome           0.13
70013            3045.6           2012-04-25       Nick Rimando     Chennai        100         Bob Emily      New York       0.15

```

```sql
select o.ord_no, o.purch_amt,o.ord_date,c.cust_name, c.city as customer_city,c.grade,
s.name as salesman_name, s.city as salesman_city,s.commission
from orders o
join customer c on o.customer_id = c.customer_id
join salesman s on s.salesman_id = c.salesman_id
```

**Output:**

![image](https://github.com/user-attachments/assets/92559616-7f7d-4f6f-adf9-95ee4ac40242)


**Question 7**
```
Write the SQL query that achieves the selection of all columns from the "patients" table, with an inner join on the "doctor_id" column, and includes a condition filtering for patients whose doctors have the first name 'John' and last name 'Smith'.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)

For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
1                Alice            Williams         1980-05-12       2024-01-10                      1

```

```sql
select p.patient_id, p.first_name, p.last_name, p.date_of_birth,p.admission_date,p.discharge_date,p.doctor_id 
from PATIENTS p
inner join DOCTORS d on d.doctor_id = p.doctor_id 
where d.first_name = 'John' and d.last_name = 'Smith'
```

**Output:**

![image](https://github.com/user-attachments/assets/85170472-c549-4e17-8261-0ddf02114a39)


**Question 8**
```
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
For example:

Result
cust_name        city             ord_no           ord_date         Order Amount
---------------  ---------------  ---------------  ---------------  ------------
Nick Rimando     Chennai          70013            2012-04-25       3045.6
Julian Green     London           70012            2012-06-27       250.45
Brad Davis       New York         70005            2012-07-27       2400.6
Geoff Cameron    Berlin           70004            2012-08-17       110.5
Jozy Altidore    Moscow           70011            2012-08-17       75.29
Nick Rimando     Chennai          70008            2012-09-10       5760.0
Graham Zusi      California       70007            2012-09-10       948.5
Brad Guzan       London           70009            2012-09-10       270.65
Nick Rimando     Chennai          70002            2012-10-05       65.26
Graham Zusi      California       70001            2012-10-05       150.5
Fabian Johns     Paris            70010            2012-10-10       1983.43
Geoff Cameron    Berlin           70003            2012-10-10       2480.4
```

```sql
select c.cust_name, c.city,o.ord_no,o.ord_date,o.purch_amt as 'Order Amount'
from customer c
left join orders o on o.customer_id = c.customer_id 
order by o.ord_date asc;
```

**Output:**

![image](https://github.com/user-attachments/assets/cdb9ba2d-e8f0-4ac1-a990-06646511ddc2)


**Question 9**
```
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.
```
![image](https://github.com/user-attachments/assets/57b25741-4786-4a17-80fa-19249ce84020)
```
For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2
```

```sql
select p.patient_id,p.first_name,p.last_name,p.date_of_birth,p.admission_date,p.discharge_date,p.doctor_id
from PATIENTS P
INNER JOIN TEST_RESULTS t on t.patient_id = p.patient_id 
where t.test_date between '2024-03-01' and '2024-03-31';
```

**Output:**

![image](https://github.com/user-attachments/assets/353ee363-2b0f-4005-9071-b4dabab29aa2)


**Question 10**
```
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.
```

![image](https://github.com/user-attachments/assets/96bace8a-c0f7-4ed8-91e8-7b7e4db3fde7)
```
For example:

Result
cust_name
---------------
Nick Rimando
Jozy Altidore
```

```sql
select c.cust_name 
from CUSTOMER c
left join ORDERS o on c.customer_id = o.customer_id 
where o.purch_amt < 100;
```

**Output:**

![image](https://github.com/user-attachments/assets/40669ca2-56b4-4660-9cb6-7db2ad047aed)

### SCREENSHOT OF SEB MODULE COMPLETION:
![{C74FB1CC-6ACE-4CED-977F-7541C9EB465E}](https://github.com/user-attachments/assets/5b4fdbd8-59d3-42c4-9b46-5f0a63529e85)




## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
