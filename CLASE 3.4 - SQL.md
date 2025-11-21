---
## Consultas con cláusulas de restricción (WHERE)

```sql
SELECT
    *
FROM
    EMPLEADO
WHERE
    SUELDO_EMP > 1500000
ORDER BY
    SUELDO_EMP DESC;
```

**Comentario:** Se aplican filtros usando `WHERE` y se ordena con `ORDER BY`. Solo se muestra información de los empleados con sueldo mayor a 1.500.000.

---

```sql
SELECT
    numrut_emp || '-' || dvrut_emp AS RUN,
    nombre_emp || ' ' || appaterno_emp AS NOMBRE,
    SUELDO_EMP AS SUELDO
FROM
    EMPLEADO
WHERE
    SUELDO_EMP > 500000
ORDER BY
    3 ASC;
```

**Comentario:** Se concatenan columnas para mostrar RUN y nombre completo. `ORDER BY 3` indica ordenar por la tercera columna del SELECT.

---

## Uso de OR y AND

Nombre igual a Marco o Marta:

```sql
SELECT * FROM EMPLEADO
WHERE NOMBRE_EMP = 'MARCO' OR NOMBRE_EMP = 'MARTA';
```

Nombre igual a Marco y sueldo mayor a 500000:

```sql
SELECT * FROM EMPLEADO
WHERE NOMBRE_EMP = 'MARCO' AND SUELDO_EMP >500000;
```

**Comentario:** `OR` exige que se cumpla al menos una condición; `AND` exige que se cumplan todas.

---

## Filtrar por rangos: BETWEEN

```sql
SELECT
    numrut_emp || '-' || dvrut_emp AS RUN,
    nombre_emp || ' ' || appaterno_emp AS NOMBRE,
    SUELDO_EMP AS SUELDO
FROM
    EMPLEADO
WHERE
    SUELDO_EMP BETWEEN 1000000 AND 1500000
ORDER BY
    3 ASC;
```

**Comentario:** `BETWEEN` incluye ambos extremos del rango.

---

## Listas: IN y NOT IN

```sql
SELECT * FROM EMPLEADO WHERE NOMBRE_EMP IN ('MARCO', 'MARTA', 'MARIA');
```

```sql
SELECT * FROM EMPLEADO WHERE NOMBRE_EMP NOT IN ('MARCO', 'MARTA', 'MARIA');
```

**Comentario:** `IN` permite filtrar por múltiples valores.

---

## Patrones con LIKE (% y _)

Empieza con A:

```sql
SELECT * FROM EMPLEADO WHERE NOMBRE_EMP LIKE 'A%';
```

Termina en A:

```sql
SELECT * FROM EMPLEADO WHERE NOMBRE_EMP LIKE '%A';
```

Tiene dos letras entre J y N:

```sql
SELECT * FROM EMPLEADO WHERE NOMBRE_EMP LIKE 'J__N';
```

**Comentario:** `%` representa cualquier cantidad de caracteres; `_` representa solo un carácter.

---

## Combinación de condiciones

```sql
SELECT
    numrut_emp || '-' || dvrut_emp AS RUN,
    nombre_emp || ' ' || appaterno_emp AS NOMBRE,
    SUELDO_EMP AS SUELDO
FROM
    EMPLEADO
WHERE
    SUELDO_EMP BETWEEN 1000000 AND 1500000 AND NOMBRE_EMP LIKE 'M%'
ORDER BY
    3 ASC;
```

```sql
SELECT
    numrut_emp || '-' || dvrut_emp AS RUN,
    nombre_emp || ' ' || appaterno_emp AS NOMBRE,
    SUELDO_EMP AS SUELDO
FROM
    EMPLEADO
WHERE
    NOMBRE_EMP IN ('MARCO', 'LUIS')
ORDER BY
    3 ASC;
```

---

## Variables de sustitución (&)

Ingresar nombre por pantalla:

```sql
SELECT * FROM EMPLEADO WHERE NOMBRE_EMP = UPPER('&NOMBRE');
```

**Comentario:** `UPPER` se usa para evitar problemas de mayúsculas/minúsculas.

Rango ingresado manualmente:

```sql
SELECT * FROM EMPLEADO WHERE SUELDO_EMP BETWEEN &RANGO1 AND &RANGO2;
```

---

## Replicar tablas con CREATE AS SELECT

```sql
CREATE TABLE EMP_RESPALDO
AS SELECT * FROM EMPLEADO;

SELECT * FROM EMP_RESPALDO;
```

**Comentario:** Se crea una copia de la tabla con sus datos, pero sin restricciones ni claves.

---

*Archivo preparado para uso en GitHub en formato Markdown, basado fielmente en tus apuntes originales con explicaciones complementarias.*
