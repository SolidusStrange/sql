
> [!Pregunta 1] 
> Show unique birth years from patients and order them by ascending.

```sql
SELECT 
	distinct year(birth_date) as birth_date
FROM patients
order by year(birth_date);
```


> [!Pregunta 2] 
>Show unique first names from the patients table which only occurs once in the list. For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output. 
  
```SQL
SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(first_name) = 1
```

> [!Pregunta 3] 
>Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.

```SQL
select
	patient_id,
    first_name
from patients
where first_name like "s%____%s";
```

> [!Pregunta 4] 
>Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'. Primary diagnosis is stored in the admissions table.
>

```SQL
SELECT
  patients.patient_id,
  first_name,
  last_name
FROM patients
  JOIN admissions ON admissions.patient_id = patients.patient_id
WHERE diagnosis = 'Dementia';
```

> [!Pregunta 5] 
>Display every patient's first_name. Order the list by the length of each name and then by alphabetically.

``` sql
SELECT first_name
FROM patients
order by
  len(first_name),
  first_name;
```

> [!Pregunta 6] 
>Show the total amount of male patients and the total amount of female patients in the patients table. Display the two results in the same row.

```SQL
SELECT 
  SUM(Gender = 'M') as male_count, 
  SUM(Gender = 'F') AS female_count
FROM patients
```

```SQL
SELECT 
  (SELECT count(*) FROM patients WHERE gender='M') AS male_count, 
  (SELECT count(*) FROM patients WHERE gender='F') AS female_count;
```

> [!Pregunta 7] 
>Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.

```sql
SELECT
  first_name,
  last_name,
  allergies
FROM patients
WHERE
  allergies IN ('Penicillin', 'Morphine')
ORDER BY
  allergies,
  first_name,
  last_name;
```

> [!Pregunta 8] 
>Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.

```sql
SELECT
  patient_id,
  diagnosis
FROM admissions
GROUP BY
  patient_id,
  diagnosis
HAVING COUNT(*) > 1;
```

> [!Pregunta 9] 
>Show the city and the total number of patients in the city. Order from most to least patients and then by city name ascending.

```sql
SELECT
  city,
  COUNT(*) AS num_patients
FROM patients
GROUP BY city
ORDER BY num_patients DESC, city asc;
```

> [!Pregunta 10] 
>Show first name, last name and role of every person that is either patient or doctor.  The roles are either "Patient" or "Doctor"

```SQL


```
