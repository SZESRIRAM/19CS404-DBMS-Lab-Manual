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
<img width="660" height="672" alt="image" src="https://github.com/user-attachments/assets/77fb188d-114c-4585-8a18-719afd219142" />


```sql
SELECT DATE(AppointmentDateTime) as AppointmentDate, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DATE(AppointmentDateTime);
```

**Output:**
<img width="807" height="605" alt="image" src="https://github.com/user-attachments/assets/b1b03f81-81d3-4e32-91cd-9cd0e7f5d560" />


**Question 2**
---
<img width="1038" height="647" alt="image" src="https://github.com/user-attachments/assets/970ba01c-bb1a-4c31-8755-4518180c5c07" />


```sql
SELECT Medication, ROUND(AVG(CAST(Dosage AS REAL)),1) AS AvgDosage
FROM Prescriptions
GROUP BY Medication
ORDER BY Medication;
```

**Output:**

<img width="667" height="691" alt="image" src="https://github.com/user-attachments/assets/b0712933-5a1f-4c11-8dc8-14fb7b7471ef" />


**Question 3**
---
<img width="925" height="661" alt="image" src="https://github.com/user-attachments/assets/53d872f5-4d5a-4471-b513-991211274949" />


```sql
SELECT InsuranceCompany,ROUND(AVG(EndDate - StartDate),1) AS AvgCoverageDurationDays
FROM Insurance
GROUP BY InsuranceCompany
ORDER BY InsuranceCompany;
```

**Output:**

<img width="925" height="612" alt="image" src="https://github.com/user-attachments/assets/46245722-9fdc-4d6b-9b43-5af0ea5bffbd" />


**Question 4**
---
<img width="733" height="476" alt="image" src="https://github.com/user-attachments/assets/f56714d6-b2d3-45d0-86f5-0f3365b9a6aa" />

```sql
SELECT SUM(income) as total_income
FROM employee
WHERE age >= 40;
```

**Output:**

<img width="368" height="243" alt="image" src="https://github.com/user-attachments/assets/3375b86c-bd82-49ff-ad1b-cc392951301e" />


**Question 5**
---
<img width="995" height="495" alt="image" src="https://github.com/user-attachments/assets/f961ea88-8d65-42c8-9508-70b2f7ad415d" />


```sql
SELECT COUNT(city) as COUNT
FROM customer
WHERE city <> 'Noida';
```

**Output:**
<img width="400" height="252" alt="image" src="https://github.com/user-attachments/assets/12a2b688-1c2d-4297-98fd-b29dd69f719c" />


**Question 6**
---
<img width="797" height="532" alt="image" src="https://github.com/user-attachments/assets/9a6f9204-9c31-4685-a5f1-f5b1400eb150" />


```sql
SELECT SUM(inventory) as total
FROM fruits
WHERE unit = 'LB';
```

**Output:**

<img width="342" height="245" alt="image" src="https://github.com/user-attachments/assets/694ee39a-7ce1-45ba-99a4-475aa83a3823" />


**Question 7**
---
<img width="886" height="488" alt="image" src="https://github.com/user-attachments/assets/6ce37deb-8eb7-4529-a4a3-f60b224ac4a8" />


```sql
SELECT COUNT(DISTINCT salesman_id) as COUNT
FROM orders;
```

**Output:**

<img width="372" height="243" alt="image" src="https://github.com/user-attachments/assets/d5f8dc53-f1a3-4103-a69c-6077f9f09a52" />


**Question 8**
---
<img width="1202" height="480" alt="image" src="https://github.com/user-attachments/assets/a455a37e-5edb-4209-b60e-304f3a4dcd11" />


```sql
SELECT jdate, AVG(workhour) as "AVG(workhour)"
From employee1
GROUP BY jdate
HAVING AVG(workhour) < 10;
```

**Output:**

<img width="642" height="281" alt="image" src="https://github.com/user-attachments/assets/78062fed-b64f-4585-b313-9406fb3e47e7" />


**Question 9**
---
<img width="1182" height="500" alt="image" src="https://github.com/user-attachments/assets/e17bf905-693e-45ff-94d0-2c963b06c293" />


```sql
SELECT p.category_id, p.product_name, p.price as Price
FROM products p
JOIN (
    SELECT
    category_id,MAX(price) as Price
    FROM products
    GROUP BY category_id
    HAVING MAX(price) > 15
)m
ON p.category_id = m.category_id
AND p.price = m.Price;
```

**Output:**

<img width="818" height="326" alt="image" src="https://github.com/user-attachments/assets/f2f5967a-d4f0-4197-ad73-b86ffcd024e8" />


**Question 10**
---
<img width="1223" height="487" alt="image" src="https://github.com/user-attachments/assets/65eb790c-2602-4306-9f15-7a6877e6793c" />



```sql
SELECT age, AVG(income) AS "AVG(income)"
FROM employee
GROUP BY age
HAVING AVG(income) BETWEEN 300000 AND 500000
```

**Output:**
<img width="575" height="265" alt="image" src="https://github.com/user-attachments/assets/8f82a078-b85e-4abc-a024-0b324853095f" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
