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

1. Para seleccionar información para mostrar usamos `SELECT`, elegimos los atributos que queremos mostrar de la tabla. `SELECT` siempre debe venir acompañado de un `FROM` ya que es de donde provienen los datos. El `WHERE` nos sirve de filtro para depurar la información que nos pidió.

---

> [!Pregunta 2] 
>Show first name and last name of patients who does not have allergies. (null)

```sql
select 
first_name,
last_name
from patients
where allergies IS NULL; -- Verifica si es nulo
```

1. Que no tenga alergias significa que no tiene valor en ese atributo, por lo tanto está nulo. Para eso, usamos un filtro que verifique si es nulo o no. `WHERE allergies IS NULL`
---
> [!Pregunta 3] 
>Show first name of patients that start with the letter 'C'

``` sql
select 
first_name
from patients
where first_name like 'C%'; -- LIKE 'a%' que empieza con '%a' termina con
```

1. Para mostrar si empieza con una letra o termina con una, usamos `LIKE` para especificar un patrón en una columna. Esta puede tener varios comodines pero para este caso usamos `%` que representa 0, 1 o múltiples caracteres, lo que quiere decir es que si lo dejamos al final y especificamos un caracter antes, significa que no importa lo que esté después, lo importante es que empiece con ese.
2. Un ejemplo, sería `'Car%'` que en una lista de nombres, nos podría traer Carmen, Carlos, Carla, etc.
3. Si fuera al revés `'%el'` diría que debe terminar con `'el'` y lo demás no importa, por lo tanto, podría traer Daniel, Gabriel, etc. 

---
> [!Pregunta 4] 
>Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)

```SQL
select 
first_name, last_name
from patients
where weight between 100 and 120;
```

1. Para mostrar dentro de un rango podemos usar varias formas, una sería que evalué el atributo mayor a un rango y menor a otro. O simplemente, podemos usar `BETWEEN` dentro del `WHERE` para que busque un valor entre los dos rangos.

> [!Pregunta 5] 
>Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'

``` SQL
update patients
set allergies = 'NKA'
where allergies is Null;	
```

1. Lo mismo anterior, la diferencias es que vamos a cambiar un valor de un atributo, no solo filtrar esos atributos, por lo tanto, para realizar cambios en una tabla, usamos `UPDATE` y para cambiar un atributo a algo distinto usamos `SET`.
2. Usamos un `WHERE` para solo cambiar específicamente los cuáles son nulos

> [!Pregunta 6] 
Show first name and last name concatinated into one column to show their full name.

```SQL
select 
first_name ||' '|| last_name AS full_name 
FROM patients
```

```sql
SELECT
  CONCAT(first_name, ' ', last_name) AS full_name
FROM patients;
```

1. Para realizar concatenaciones, podemos usar la función `CONCAT()` o usar el operador estándar `||`

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

1. Cuando queremos unir información de dos tablas que tienen un atributo en común usamos `JOIN`.
2. Para utilizarlo, debemos ingresarlo después del `FROM` ya que los atributos que establecimos anteriormente provienen de esta tabla y va a ser de la que empezaremos a unir.
3. Luego de eso usamos `JOIN` → la tabla que queremos unir → `ON` → atributo = atributo (igual en ambas tablas)
4. Estas van con un "alias" que indica el nombre de la tabla de donde viene, puede ser cualquiera mientras no sea igual al otro. Por ejemplo: `doctor_names.doctor_id` o `dn.doctor_id`

> [!Pregunta 8] 
Show how many patients have a birth_date with 2010 as the birth year.

```sql
SELECT COUNT(*) AS total_patients
FROM patients
WHERE YEAR(birth_date) = 2010;
```

1. La función `YEAR()` nos funciona para extraer el año de una fecha. 

> [!Pregunta 9] 
Show the tallest patient.

```sql 
SELECT
  first_name,
  last_name,
  MAX(height) AS height
FROM patients;
```

1. La función `MAX()` entrega el valor más alto del atributo en comparación a todos. 

> [!Pregunta 10] 
Show all columns for patients who have one of the following patient_ids:  
1, 45, 534, 879, 1000

```sql
SELECT *
FROM patients
WHERE
  patient_id IN (1, 45, 534, 879, 1000);
```

1. Similar a otros lenguajes `IN` se puede usar para ver si está dentro de la lista de valores. `IN` `(1, 2 ,3 ,4 ,5)`

> [!Pregunta 11] 
Show the total number of admissions

```sql
SELECT COUNT(*) AS total_admissions
FROM admissions;
```

1. `COUNT()` cuenta el total de filas de la columna, si usamos `*` contará todas las filas, si queremos que agrupe por un atributo en particular, debemos usar `GROUP BY`

> [!Pregunta 12] 
Show all the columns from admissions where the patient was admitted and discharged on the same day.

```SQL
SELECT *
FROM admissions
WHERE admission_date = discharge_date;
```

1. En la tabla la fecha de admisión y de alta nos indican el inicio y el fin de la estadía, por lo tanto, nos piden pacientes que estuvieron por el día solamente. 
2. Para eso, hacemos un `WHERE` que correspondería a un filtro con la condición de que ambas fechas sean iguales.

> [!Pregunta 13] 
Show the patient id and the total number of admissions for patient_id 579.

```SQL
SELECT
  patient_id,
  COUNT(*) AS total_admissions
FROM admissions
WHERE patient_id = 579;
```

1. Para mostrar el total de admisiones, usamos `COUNT` para que cuente el total de filas.
2. Sin embargo, también nos pide que sea sólo del paciente con el ID 579, por lo tanto usamos un `WHERE` para filtrar.

> [!Pregunta 14] 
Based on the cities that our patients live in, show unique cities that are in province_id 'NS'.

```sql
SELECT DISTINCT(city) AS unique_cities
FROM patients
WHERE province_id = 'NS';
```

```SQL
SELECT city
FROM patients
GROUP BY city
HAVING province_id = 'NS';
```

1. Acá hay dos formas distintas de resolver el ejercicio. La primera usa `SELECT DISTINCT` que lo que hace es solo retornar los valores diferentes, si usáramos CITY en este caso, diríamos que solo retorne los valores diferentes de ese atributo.
2. Para el segundo, usamos un `HAVING`, la razón de por qué se utiliza un `HAVING` y no un `WHERE` (funcionan de manera similar), es porque `WHERE` no puede funcionar sobre funciones agregadas:
	1. `MIN()`, `MAX()`, `COUNT()`, `SUM()`, `MAX()`
	2. Por lo tanto, `HAVING` lo usamos después de agrupar, ya que funcionará en base a lo ya creado.

> [!Pregunta 15] 
Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70

``` sql
SELECT first_name, last_name, birth_date 
FROM patients
WHERE height > 160 AND weight > 70;
```

1. Nos piden dos condiciones, no podemos usar `IN BETWEEN` ya que tenemos que evaluar no solo una. Por lo tanto, simplemente usamos el operador lógico `AND` que evaluara que ambas condiciones se cumplan.

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

1. Nos piden una consulta donde encontremos diferentes atributos, pero lo más importante es que "alergias" no debe ser nulo y además debe ser de la ciudad de "Hamilton".
2. Para eso, simplemente usamos un `WHERE` para establecer condiciones y un operador lógico `AND` para que ambas se cumplan.
3. Por último, para que no sea nulo, establecimos `IS NOT` `null`. El operador lógico `NOT` establece que sería lo opuesto a `IS` de forma normal.