
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
SELECT first_name, last_name, 'Patient' as role FROM patients
    union all
select first_name, last_name, 'Doctor' from doctors;
```

> [!Pregunta 11] 
>Show all allergies ordered by popularity. Remove NULL values from query.

```SQL
SELECT
  allergies,
  COUNT(*) AS total_diagnosis
FROM patients
WHERE
  allergies IS NOT NULL
GROUP BY allergies
ORDER BY total_diagnosis DESC
```

> [!Pregunta 12] 
>  Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.

```SQL
SELECT
  first_name,
  last_name,
  birth_date
FROM patients
WHERE
  YEAR(birth_date) BETWEEN 1970 AND 1979
ORDER BY birth_date ASC;
```

> [!Pregunta 13] 
> We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order  EX: SMITH,jane

```SQL
SELECT
  CONCAT(UPPER(last_name), ',', LOWER(first_name)) AS new_name_format
FROM patients
ORDER BY first_name DESC;
```

```sql
SELECT
  UPPER(last_name) || ',' || LOWER(first_name) AS new_name_format
FROM patients
ORDER BY first_name DESC;
```

> [!Pregunta 14] 
> Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.

```SQL
SELECT
  province_id,
  SUM(height) AS sum_height
FROM patients
GROUP BY province_id
HAVING sum_height >= 7000
```

> [!Pregunta 15] 
> Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'

```SQL
SELECT
  (MAX(weight) - MIN(weight)) AS weight_delta
FROM patients
WHERE last_name = 'Maroni';
```

> [!Pregunta 16] 
> Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.

```sql
SELECT
  DAY(admission_date) AS day_number,
  COUNT(*) AS number_of_admissions
FROM admissions
GROUP BY day_number
ORDER BY number_of_admissions DESC
```

> [!Pregunta 17] 
> Show all columns for patient_id 542's most recent admission_date.

```SQL
SELECT *
FROM admissions
WHERE patient_id = 542
GROUP BY patient_id
HAVING
  admission_date = MAX(admission_date);
```

> [!Pregunta 18] 
> Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria: 
>  1. patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.  
>  2. attending_doctor_id contains a 2 and the length of patient_id is 3 characters.

```SQL
select patient_id,
	attending_doctor_id,
    diagnosis
from admissions
where 
	((patient_id % 2) = 1 AND attending_doctor_id IN (1, 5, 19)) 
    OR 
    (attending_doctor_id LIKE '%2%' AND LEN(patient_id) = 3);
```

```SQL
SELECT
  patient_id,
  attending_doctor_id,
  diagnosis
FROM admissions
WHERE
  (
    attending_doctor_id IN (1, 5, 19)
    AND patient_id % 2 != 0
  )
  OR 
  (
    attending_doctor_id LIKE '%2%'
    AND len(patient_id) = 3
```



