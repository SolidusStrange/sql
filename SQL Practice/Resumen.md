### Principiante

Cada ítem: **(qué hace)** — **Sintaxis / ejemplo corto** — **Preguntas donde aparece**

- **SELECT / FROM**  
    (Seleccionar columnas desde una tabla).  
    `SELECT col1, col2 FROM tabla;` — P1, P3, P4, P6, P9, P10, P12, P15, P16, P23, P24...
    
- **WHERE (filtros simples)**  
    (Filtrar filas según condiciones).  
    `WHERE gender = 'M'` — P1, P2, P3, P4, P12, P15, P16, P23...
    
- **IS NULL / IS NOT NULL**  
    (Comprobar valores nulos).  
    `WHERE allergies IS NULL` / `IS NOT NULL` — P2, P5, P11
    
- **LIKE y comodines `%` y `_`**  
    (Búsqueda por patrón en texto).  
    `WHERE first_name LIKE 'C%'` — P3, P33 (ejemplos de patrón más complejos en intermedio)
    
- **BETWEEN**  
    (Rango inclusivo).  
    `WHERE weight BETWEEN 100 AND 120` — P4
    
- **UPDATE ... SET ... WHERE**  
    (Modificar filas).  
    `UPDATE patients SET allergies='NKA' WHERE allergies IS NULL;` — P5
    
- **Concatenación de strings**  
    (`||` o `CONCAT`) — `first_name || ' ' || last_name` o `CONCAT(...)` — P6, P22, P26, P20
    
- **JOIN (INNER JOIN básico)**  
    (Unir tablas por columna común).  
    `FROM patients JOIN province_names ON ...` — P7, P4, P22, P26
    
- **COUNT() simple**  
    (Contar filas).  
    `SELECT COUNT(*) FROM admissions;` — P11, también en P8, P13
    
- **MAX() / MIN()**  
    (Máximo / mínimo de una columna).  
    `SELECT MAX(height) FROM patients;` — P9, P15
    
- **IN (lista de valores)**  
    (Equivalente a múltiples OR).  
    `WHERE patient_id IN (1,45,534)` — P10, P7 (ej. Penicillin/Morphine)

---
### Intermedio

Cada ítem: **(qué hace)** — **Sintaxis / ejemplo corto** — **Preguntas donde aparece**

- **DISTINCT**  
    (Eliminar duplicados en la salida).  
    `SELECT DISTINCT YEAR(birth_date)` — Interm P1
    
- **YEAR(), DAY(), funciones de fecha**  
    (Extraer partes de una fecha; **pueden variar según SGBD**).  
    `WHERE YEAR(birth_date)=2010` / `DAY(admission_date)` — Interm P1, P12, P16
    
- **GROUP BY + agregados (COUNT, SUM, AVG, MIN, MAX)**  
    (Agrupar filas para agregaciones).  
    `GROUP BY city; COUNT(*)` — Interm P2, P9, P11, P14, P19, P21, P25
    
- **HAVING**  
    (Filtrar grupos después de agrupar — para condiciones sobre agregados).  
    `GROUP BY patient_id HAVING COUNT(*) > 1` — Interm P2, P8, P14, P22, P25
    
- **ORDER BY con múltiples criterios y direcciones**  
    `ORDER BY num_patients DESC, city ASC` — Interm P9, Interm P5
    
- **SUM con condición / subqueries escalares**  
    (Sumar con expresión booleana o usar subselects).  
    `SUM(gender='M')` o subqueries en SELECT. — Interm P6, Interm P25
    
- **CASE WHEN**  
    (Condicional en SELECT).  
    `CASE WHEN gender='M' THEN 'MALE' ELSE 'FEMALE' END` — Interm P23
    
- **ROUND() y transformaciones numéricas**  
    (Redondeo y conversión de unidades).  
    `ROUND(height/30.48,1)` — Interm P23
    
- **UNION / UNION ALL**  
    (Combinar resultados de varias SELECTs).  
    `SELECT ... FROM patients UNION ALL SELECT ... FROM doctors` — Interm P10
    
- **LEFT JOIN para encontrar no-coincidencias**  
    (Mostrar todos de la izquierda y NULL donde no hay match).  
    `LEFT JOIN admissions ... WHERE admissions.patient_id IS NULL` — Interm P24
    
- **Subconsultas correlacionadas y no correlacionadas**  
    (Usar SELECT dentro de WHERE o FROM para comparar resultados).  
    `WHERE admission_date = (SELECT MAX(a2.admission_date) FROM admissions a2 WHERE a2.patient_id = p.patient_id)` — Interm P26, Interm P17
    
- **Derived table (subquery en FROM)**  
    (Tratar el resultado de una consulta como tabla).  
    `FROM ( SELECT admission_date, COUNT(*) as number_of_visits FROM admissions GROUP BY admission_date )` — Interm P25
    
- **Funciones de cadena y cambio de case**  
    `UPPER(), LOWER(), CONCAT()` — Interm P13, P22
    
- **Operadores aritméticos y modulus (%)**  
    (Cálculos y evaluación de paridad).  
    `patient_id % 2 = 1` — Interm P18
    
- **Uso de LEN() / LENGTH()**  
    (Longitud de cadenas — nombre puede variar por SGBD).  
    `LEN(first_name)` — Interm P5, P18
    
- **LIKE con `%` y `_` y patrones complejos**  
    (Más avanzado: comienzo y fin con cantidad mínima de caracteres).  
    `first_name LIKE 's%____%s'` — Interm P3

---
### Avanzado

### Índice rápido (Dónde buscar un tema específico)

Formato: **Tema** — **Qué buscar** — **Ejemplo corto** — **Preguntas relacionadas**

- **Filtrado básico** — `WHERE` — `WHERE gender='M'` — Principiante P1, P15
- **Nulos** — `IS NULL / IS NOT NULL` — `WHERE allergies IS NULL` — P2, P5, P11
- **Patrones de texto** — `LIKE '%...%' / '_'` — `LIKE 'C%'` — P3, Interm P3, P18
- **Rangos** — `BETWEEN` — `weight BETWEEN 100 AND 120` — P4
- **Actualizar filas** — `UPDATE ... SET ...` — `UPDATE patients SET ...` — P5
- **Unir tablas** — `JOIN ... ON ...` — `JOIN admissions ON patients.patient_id = admissions.patient_id` — P7, P4, P22
- **Left join para no-existentes** — `LEFT JOIN ... WHERE right.col IS NULL` — P24
- **Contar / agrupar** — `GROUP BY`, `COUNT()` — `GROUP BY city; COUNT(*)` — Interm P9, P11, P19
- **Filtrar agregados** — `HAVING` — `HAVING COUNT(*) > 1` — Interm P2, P8, P14, P22
- **Ordenar** — `ORDER BY` — `ORDER BY len(first_name), first_name` — Interm P5, P9
- **Subconsultas** — `(SELECT ...)` — `WHERE admission_date = (SELECT MAX(...))` — Interm P17, P26
- **Derived tables** — `FROM (SELECT ...)` — Interm P25
- **Funciones de fecha** — `YEAR(), DAY()` — `YEAR(birth_date)=2010` — P8, Interm P12, P16
- **String case y concatenación** — `UPPER(), LOWER(), CONCAT()` — P13, P22, P20
- **Unión de resultados** — `UNION ALL` — P10
- **Cálculos y formato** — `ROUND(), SUM(), AVG()` — P23, P25
- **Condicional en SELECT** — `CASE WHEN ... THEN ... END` — P23
- **Patrones y longitudes especiales** — `LEN()` / `%` / `_` / modulus (%) — Interm P3, P18