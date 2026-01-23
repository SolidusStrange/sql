
> [!Pregunta 1] 
> Show unique birth years from patients and order them by ascending.

```sql
SELECT 
	distinct year(birth_date) as birth_year
FROM patients
order by year(birth_date); -- O podemos usar simplemente el alias birth_year
```

1. Para mostrar un valores únicos de fechas de nacimiento, usamos `SELECT DISTINCT` y para ordenarlos usamos `ORDER BY` se acompaña del atributo que queremos que ordene. 
2. Por defecto es ascendente. Si quisiéramos que fuera descendente, pondríamos `ORDER BY birth_year desc`.

> [!Pregunta 2] 
>Show unique first names from the patients table which only occurs once in the list. For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output. 
  
```SQL
SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(first_name) = 1
```

1. Para mostrar nombres únicos de la tabla que solo ocurren una vez en la lista usamos un `GROUP BY` que agrupa todos los valores únicos, y después con `HAVING` evaluamos que el conteo de estos sea igual a 1.

> [!Pregunta 3] 
>Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.

```SQL
select
	patient_id,
    first_name
from patients
where first_name like "s%____%s";
```

1. Para filtrar con que empiece y termine con un carácter, debemos usar `WHERE` y `LIKE` y para que empiece y termine usamos `%`.
2. Si queremos que empiece con s, usamos `s%`, si queremos que termine `s%`, para que sea máximo 6 caracteres usamos el comodín `_` que representa cualquier carácter. 
3. Por lo tanto, si queremos por ejemplo un nombre como "Jaime", necesitaríamos hacer que empiece con J (`s%`), termine con E `(%e`) y tenga 3 caracteres entre medio de esos dos, por lo tanto `___`. Quedando como resultado: `%J___%e`

| %   | Represents zero or more characters                         |
| --- | ---------------------------------------------------------- |
| _   | Represents a single character                              |
| []  | Represents any single character within the brackets *      |
| ^   | Represents any character not in the brackets               |
| -   | Represents any single character within the specified range |
| {}  | Represents any escaped character                           |

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

1. Acá nos piden filtrar por información que no está en esta tabla, por lo tanto debemos unirla con otra mediante un `JOIN` y buscando un atributo que se comparta en ambos, normalmente es el ID.
2. Usamos un alias o el nombre de la tabla para reconocer a cuál tabla pertenece, podemos usar cualquiera: `alias.patient_id` en el cual significaría que existe una tabla llamada alias donde hay un atributo llamado `patient_id`
3. Para unir, nos ubicamos debajo del `FROM` (ya que estamos indicando que hay atributos seleccionados que provienen de una tabla que se unirá a la otra) y usamos la tabla que queremos unir más un `ON` para después indicar cuáles son los atributos que son iguales en ambos siempre indicando con un alias donde provienen.

> [!Pregunta 5] 
>Display every patient's first_name. Order the list by the length of each name and then by alphabetically.

``` sql
SELECT first_name
FROM patients
ORDER BY
  len(first_name),
  first_name
```

1. Nos piden que ordenemos la lista por el largo de cada nombre y de forma alfabética.
2. Para ordenar una lista, usamos `ORDER BY`
3. Podemos usar múltiples condiciones que se harán en el orden que establezcamos, en este caso, usaremos LEN() para evaluar el largo, y después el atributo que queramos que ordene de forma alfabética

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

1. Para poder calcular el monto total de un atributo, debemos hacer un SUM() y podemos realizar la condición dentro. Requiere mostrar ambos en la misma fila, por lo que simplemente debemos hacer un `SELECT` a los dos `SUM()`

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

> [!Pregunta 19] 
>Show first_name, last_name, and the total number of admissions attended for each doctor.  Every admission has been attended by a doctor.
  
```SQL
SELECT
  first_name,
  last_name,
  count(*) as admissions_total
from admissions a
  join doctors ph on ph.doctor_id = a.attending_doctor_id
group by attending_doctor_id
```

```SQL
select first_name, last_name, count(admission_date)
from doctors
join admissions on admissions.attending_doctor_id = doctors.doctor_id
group by first_name;
```

``` SQL
SELECT
  first_name,
  last_name,
  count(*)
from
  doctors p,
  admissions a
where
  a.attending_doctor_id = p.doctor_id
group by p.doctor_id;
```

> [!Pregunta  20] 
>For each doctor, display their id, full name, and the first and last admission date they attended.

```SQL
select 
	doctor_id,
    first_name ||" "|| last_name as full_name,
    min(admission_date) as first_admission_date,
    max(admission_date) as last_admission_date
FROM doctors
join admissions on doctors.doctor_id = admissions.attending_doctor_id
group by doctor_id;
```

> [!Pregunta  21] 
>Display the total amount of patients for each province. Order by descending.

```sql
select
	province_names.province_name,
    count(patient_id) as patient_count
from patients
join province_names on patients.province_id = province_names.province_id
group by province_name
order by patient_count desc;
```

``` SQL
SELECT
  province_name,
  COUNT(*) as patient_count
FROM patients pa
  join province_names pr on pr.province_id = pa.province_id
group by pr.province_id
order by patient_count desc;
```

> [!Pregunta  22] 
>For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.

```SQL
select 
	patients.first_name ||' '|| patients.last_name as patient_name,
    admissions.diagnosis AS diagnosis,
    doctors.first_name ||' '|| doctors.last_name as doctor_name
from patients
join admissions on patients.patient_id = admissions.patient_id
join doctors on admissions.attending_doctor_id = doctors.doctor_id;
```

```sql
SELECT
  CONCAT(patients.first_name, ' ', patients.last_name) as patient_name,
  diagnosis,
  CONCAT(doctors.first_name,' ',doctors.last_name) as doctor_name
FROM patients
  JOIN admissions ON admissions.patient_id = patients.patient_id
  JOIN doctors ON doctors.doctor_id = admissions.attending_doctor_id;
```

> [!Pregunta  22] 
>display the first name, last name and number of duplicate patients based on their first name and last name.  Ex: A patient with an identical name can be considered a duplicate.
  
``` sql
select
  first_name,
  last_name,
  count(*) as num_of_duplicates
from patients
group by
  first_name,
  last_name
having count(*) > 1
```

|Cláusula|Cuándo se usa|
|---|---|
|`WHERE`|Filtra **filas individuales**|
|`HAVING`|Filtra **grupos agregados**|
*-`COUNT()` **solo puede ir en `HAVING` o `SELECT`**, nunca en `WHERE`.

> [!Pregunta  23] 
>Display patient's full name,  
height in the units feet rounded to 1 decimal,  
weight in the unit pounds rounded to 0 decimals,  
birth_date,  
gender non abbreviated.  
Convert CM to feet by dividing by 30.48.  
Convert KG to pounds by multiplying by 2.205.

```SQL
select
    first_name ||' '|| last_name as patient_name,
    ROUND(height / 30.48, 1) as 'height "Feet"', 
    ROUND(weight * 2.205, 0) AS 'weight "Pounds"', birth_date,
CASE
	WHEN gender = 'M' THEN 'MALE' 
  ELSE 'FEMALE' 
END AS 'gender_type'
from patients  
```

> [!Pregunta  24] 
>Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.

```sql
SELECT
  patients.patient_id,
  first_name,
  last_name
from patients
  left join admissions on patients.patient_id = admissions.patient_id
where admissions.patient_id is NULL
```

> [!Pregunta  25] 
>Display a single row with max_visits, min_visits, average_visits where the maximum, minimum and average number of admissions per day is calculated. Average is rounded to 2 decimal places.

```sql
select 
	max(number_of_visits) as max_visits, 
	min(number_of_visits) as min_visits, 
  round(avg(number_of_visits),2) as average_visits 
from (
  select admission_date, count(*) as number_of_visits
  from admissions 
  group by admission_date
  )
```

> [!Pregunta  26] 
>Display every patient that has at least one admission and show their most recent admission along with the patient and doctor's full name.

```sql
SELECT 
    p.first_name || ' ' || p.last_name AS patient_name,
    a.admission_date,
    d.first_name || ' ' || d.last_name AS doctor_name
FROM patients p
JOIN admissions a ON p.patient_id = a.patient_id
JOIN doctors d ON a.attending_doctor_id = d.doctor_id
WHERE a.admission_date = (
    SELECT MAX(a2.admission_date)
    FROM admissions a2
    WHERE a2.patient_id = p.patient_id
);
```

