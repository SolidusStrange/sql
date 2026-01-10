> [!Pregunta 1]
> Show first name, last name, and gender of patients whose gender is 'M'

```SQL
SELECT 
first_name, 
last_name, 
gender
FROM patients
where gender = 'M';

```

> [!Pregunta 2] 
>Show first name and last name of patients who does not have allergies. (null)

```sql
select 
first_name,
last_name
from patients
where allergies IS NULL; -- Verifica si es nulo
```

> [!Pregunta 3] 
>Show first name of patients that start with the letter 'C'

``` sql
select 
first_name
from patients
where first_name like 'C%'; -- LIKE 'a%' que empieza con '%a' termina con
```

> [!Pregunta 4] 
>Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)

```SQL
select 
first_name, last_name
from patients
where weight between 100 and 120;
```

> [!Pregunta 5] 
>Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'

``` SQL
update patients
set allergies = 'NKA'
where allergies is Null;	
```

> [!Pregunta 6] 
Show first name and last name concatinated into one column to show their full name.

v1
```SQL
select 
first_name ||' '|| last_name AS full_name 
FROM patients
```
v2
```sql
SELECT
  CONCAT(first_name, ' ', last_name) AS full_name
FROM patients;
```

> [!Pregunta 7] 
Show first name, last name, and the **full** province name of each patient.
Example: 'Ontario' instead of 'ON'  

``` SQL
SELECT
  first_name,
  last_name,
  province_name
FROM patients
  JOIN province_names ON province_names.province_id = patients.province_id;
```

> [!Pregunta 8] 
Show how many patients have a birth_date with 2010 as the birth year.

```sql
SELECT COUNT(*) AS total_patients
FROM patients
WHERE YEAR(birth_date) = 2010;
```

> [!Pregunta 9] 
Show how many patients have a birth_date with 2010 as the birth year.

```sql 
SELECT
  first_name,
  last_name,
  MAX(height) AS height
FROM patients;
```

> [!Pregunta 10] 
Show all columns for patients who have one of the following patient_ids:  
1, 45, 534, 879, 1000

```sql
SELECT *
FROM patients
WHERE
  patient_id IN (1, 45, 534, 879, 1000);
```

> [!Pregunta 11] 
Show the total number of admissions

```sql
SELECT COUNT(*) AS total_admissions
FROM admissions;
```

> [!Pregunta 12] 
Show all the columns from admissions where the patient was admitted and discharged on the same day.

```SQL
SELECT *
FROM admissions
WHERE admission_date = discharge_date;
```

> [!Pregunta 13] 
Show the patient id and the total number of admissions for patient_id 579.

```SQL
SELECT
  patient_id,
  COUNT(*) AS total_admissions
FROM admissions
WHERE patient_id = 579;
```

> [!Pregunta 14] 
Based on the cities that our patients live in, show unique cities that are in province_id 'NS'.

V1
```sql
SELECT DISTINCT(city) AS unique_cities
FROM patients
WHERE province_id = 'NS';
```
V2
```SQL
SELECT city
FROM patients
GROUP BY city
HAVING province_id = 'NS';
```

> [!Pregunta 15] 
Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70

``` sql
SELECT first_name, last_name, birth_date 
FROM patients
WHERE height > 160 AND weight > 70;
```

> [!Pregunta 16] 
Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'

``` SQL
SELECT
  first_name,
  last_name,
  allergies
FROM patients
WHERE
  city = 'Hamilton'
  and allergies is not null
```
