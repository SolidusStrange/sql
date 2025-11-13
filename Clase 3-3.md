### script_ejemplos.sql

- Borrar tablas creadas y secuencia. 
```SQL
DROP TABLE empleado CASCADE CONSTRAINTS;
DROP TABLE comuna CASCADE CONSTRAINTS;
DROP SEQUENCE seq_comuna;

```
- Creamos nueva secuencia después.
```SQL
CREATE SEQUENCE seq_comuna;
```

- Crear tabla comuna con id
```SQL
CREATE TABLE comuna
(id_comuna   NUMBER(3) NOT NULL,
 nombre      VARCHAR2(25) NOT NULL CONSTRAINT un_comuna UNIQUE,
 CONSTRAINT pk_comuna PRIMARY KEY(id_comuna));
```
- Crear tabla empleado
```SQL
CREATE TABLE empleado(
    numrut_emp    NUMBER(10) CONSTRAINT pk_empleado PRIMARY KEY,
    dvrut_emp     VARCHAR2(1) NOT NULL,
    appaterno_emp VARCHAR2(15) CONSTRAINT nn_apellido_empleado NOT NULL,
    apmaterno_emp VARCHAR2(15) NOT NULL,
    nombre_emp    VARCHAR2(25) NOT NULL,
    direccion_emp VARCHAR2(60) NOT NULL,
    fonofijo_emp  VARCHAR2(15) NOT NULL CONSTRAINT un_fono_empleado UNIQUE,
    celular_emp   VARCHAR2(15),
    fecnac_emp    DATE,
    sueldo_emp    NUMBER(7) NOT NULL CONSTRAINT ck_sueldo CHECK (sueldo_emp >= 300000),
    id_comuna     NUMBER(3) NOT NULL,
    CONSTRAINT fk_empleado_comuna FOREIGN KEY (id_comuna) REFERENCES comuna(id_comuna)
);
```
- Crear tabla alumno
```SQL
--SIN COLUMNA IDENTIDAD
--AGREGAR GENERATED ALWAYS AS IDENTITY,
CREATE TABLE alumno (
    run              NUMBER(8),
    dv               VARCHAR2(1),
    nombre           VARCHAR2(20),
    apellido         VARCHAR2(20),
    fecha_nacimiento DATE
);

INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'Melipilla');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'Santiago');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'Viña del Mar');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'Ñuñoa');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'Vitacura');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'La Reina');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'La Florida');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'Maipú');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'Lo Barnechea');
INSERT INTO comuna VALUES (seq_comuna.NEXTVAL,'Macul');
```

- Insertar información en las tablas
```SQL
INSERT INTO empleado VALUES (11649964,'0','GALVEZ','CASTRO','MARTA','CLOVIS MONTERO 0260 D/202','23417556','25273328','20121971',1515239,2);
INSERT INTO empleado VALUES (12113369,'4','ROMERO','DIAZ','NANCY','TENIENTE RAMON JIMENEZ 4753','25631567','22623877','09061968',2710153,1);
INSERT INTO empleado VALUES (12456905,'1','CANALES','BASTIAS','JORGE','GENERAL CONCHA PEDREGAL #885','27779827','27413395','21121957',2945675,3);
INSERT INTO empleado VALUES (12466553,'2','VIDAL','PEREZ','TERESA','FCO. DE CAMARGO 14515 D/14','28583700','28122603','20111969',1202614,4);
INSERT INTO empleado VALUES (11745244,'3','VENEGAS','SOTO','KARINA','ARICA 3850','27790734','27494190','23061963',1439042,5);
INSERT INTO empleado VALUES (11999100,'4','CONTRERAS','CASTILLO','CLAUDIO','ISABEL RIQUELME 6075','27764142','25232677','15031966',364163,2);
INSERT INTO empleado VALUES (12888868,'5','PAEZ','MACMILLAN','JOSE','FERNANDEZ CONCHA 500','22399493','27735417','25071964',1896155,1);
INSERT INTO empleado VALUES (12811094,'6','MOLINA','GONZALEZ','PAULA','PJE.TIMBAL 1095 V/POMAIRE','25313830',NULL,'26081978',1757577,1);
INSERT INTO empleado VALUES (14255602,'7','MUÑOZ','ROJAS','CARLOTA','TERCEIRA 7426 V/LIBERTAD','26490093','27414886','27091982',2658577,2);
INSERT INTO empleado VALUES (11630572,'8','ARAVENA','HERBAGE','GUSTAVO','FERNANDO DE ARAGON 8420','25588481','26256661','15031966',1957095,4);
INSERT INTO empleado VALUES (11636534,'9','ADASME','ZUÑIGA','LUIS','LITTLE ROCK 117 V/PDTE.KENNEDY','26483081','26213403','29101973',1614934,3);
INSERT INTO empleado VALUES (12272880,'K','LAPAZ','SEPULVEDA','MARCO','GUARDIA MARINA. RIQUELME 561','26038967','22814034','01101989',1352596,2);
INSERT INTO empleado VALUES (11846972,'5','OGAZ','VARAS','MARCO','OVALLE Nº5798 V/ OHIGGINS','27763209','27377830','31121959',353590,1);
INSERT INTO empleado VALUES (14283083,'6','MONDACA','COLLAO','AUGUSTO','NUEVA COLON Nº1152','27357104','25376873','01101989',1144245,1);
INSERT INTO empleado VALUES (14541837,'7','ALVAREZ','RIVERA','MARCO','HONDURAS B/8908 D/102 L.BRISAS','22875902','25292497','02011977',1541418,3);
INSERT INTO empleado VALUES (12482036,'8','OLAVE','CASTILLO','ADRIAN','ELISA CORREA 188','22888897','28441077','03011956',1068086,5);
INSERT INTO empleado VALUES (12468081,'9','SANCHEZ','GONZALEZ','PAOLA','AV.OSSA 01240 V/MI VIÑITA','25273328','25581593','04101987',1330355,5);
INSERT INTO empleado VALUES (12260812,'0','RIOS','ZUÑIGA','RAFAEL','LOS CASTAÑOS 1427 VILLA C.C.U.','26410462','28501857','05111991',367056,5);
INSERT INTO empleado VALUES (12899759,'1','CACERES','JIMENEZ','ERIKA','PJE.NAVARINO 15758 V/P.DE OÑA','28593881','22650316','06011974',2281415,2);
INSERT INTO empleado VALUES (12868553,'2','CHACON','AMAYA','PATRICIA','LO ERRAZURIZ 530 V/EL SENDERO','25577963',NULL,'07111985',1723055,3);
INSERT INTO empleado VALUES (12648200,'3','NARVAEZ','MUÑOZ','LUIS','AMBRIOSO OHIGGINS 2010','27742268','25317272','08101993',1966613,4);
INSERT INTO empleado VALUES (11670042,'5','GONGORA','DEVIA','VALESKA','PASAJE VENUS 2765','23244270','26224817','10011975',1635086,5);
INSERT INTO Empleado VALUES (12642309,'K','NAVARRO','SANTIBAÑEZ','JUAN','SANTA ELENA 300 V/LOS ALAMOS','27441530','25342599','11101986',1659230,5);
INSERT INTO empleado VALUES (18560875,'5','BARRERA','ONETO','MARIA','CARRERA 520','23247042','26817224','10012000',420000,3);
INSERT INTO Empleado VALUES (17963421,'K','RIVAS','MORENO','JUAN','SANTA MARIA 520 V/LOS ALERCES','21530744','22599534','11101998',480000,2);
```
---
### PRACTICA DE CODIGOS
```SQL
SELECT * FROM COMUNA; -- SELECCIONA TODO DE LA TABLA COMUNA
SELECT * FROM EMPLEADO; -- SELECCIONA TODO DE LA TABLA EMPLEADO
SELECT nombre_emp, direccion_emp, sueldo_emp,  FROM EMPLEADO; -- SELECCIONA NOMBRE, DIRECCION, SUELDO DE LA TABLA EMPLEADO
```

- Traiganme solo el nombre, direccion, sueldo y sueldo ajustado
```SQL
SELECT nombre_emp, direccion_emp, sueldo_emp, sueldo_emp*1.1 FROM EMPLEADO;
```
- Para cambiar las columnas y darle nombre, así se vería de forma correcta: 
```SQL
SELECT 
    numrut_emp AS RUT,
    dvrut_emp AS DV,
    nombre_emp AS NOMBRE,
    direccion_emp AS DIRECCION,
    sueldo_emp AS SUELDO,
    sueldo_emp*1.1 AS SUELDO_CALCULADO
FROM
    empleado```
- Queremos concatenar el rut con el digito verificador para eso usamos concatenar con `||'-'||` para incluir un guion entre medio
```SQL
SELECT 
    numrut_emp ||'-'|| dvrut_emp AS RUT,
    nombre_emp AS NOMBRE,
    direccion_emp AS DIRECCION,
    sueldo_emp AS SUELDO,
    sueldo_emp*1.1 AS SUELDO_CALCULADO 
FROM
    empleado
```

- Agregamos el nombre concatenado con espacio
```SQL
SELECT 
    numrut_emp ||'-'|| dvrut_emp AS RUT,
    nombre_emp ||' '|| appaterno_emp ||' '|| apmaterno_emp AS NOMBRE_COMPLETO,
    direccion_emp AS DIRECCION,
    sueldo_emp AS SUELDO,
    sueldo_emp*1.1 AS SUELDO_CALCULADO
FROM
    empleado
```

- Redondear sueldo
```sql
SELECT 
    numrut_emp ||'-'|| dvrut_emp AS RUT,
    nombre_emp ||' '|| appaterno_emp ||' '|| apmaterno_emp AS NOMBRE_COMPLETO,
    direccion_emp AS DIRECCION,
    sueldo_emp AS SUELDO,
    ROUND(sueldo_emp*1.1) AS SUELDO_CALCULADO
FROM
    EMPLEADO
```

- Queremos traer un atributo duplicado pero una sola vez, no queremos que aparezca duplicado, para eso usamos `DISTINCT`
```SQL
SELECT DISTINCT
    id_comuna
FROM
    empleado;
```

- Ordenar de mayor a menor o viceversa:
```SQL
-- ORDER BY
--	posicion,
--	nombre atributo,
--	atributo calculado
-- ASC/DESC
```

```SQL
SELECT 
    numrut_emp ||'-'|| dvrut_emp AS RUT,
    nombre_emp ||' '|| appaterno_emp ||' '|| apmaterno_emp AS NOMBRE_COMPLETO,
    direccion_emp AS DIRECCION,
    sueldo_emp AS SUELDO,
    ROUND(sueldo_emp*1.1) AS SUELDO_CALCULADO
FROM
    EMPLEADO
ORDER BY SUELDO_CALCULADO DESC; -- DESCENDIENTE
```

```SQL
SELECT 
    numrut_emp ||'-'|| dvrut_emp AS RUT,
    nombre_emp ||' '|| appaterno_emp ||' '|| apmaterno_emp AS NOMBRE_COMPLETO,
    direccion_emp AS DIRECCION,
    sueldo_emp AS SUELDO,
    ROUND(sueldo_emp*1.1) AS SUELDO_CALCULADO
FROM
    EMPLEADO
ORDER BY 5 DESC; -- EN VEZ DE PONER EL ATRIBUTO, SE PUEDE USAR LA POSICION 
```

- Creamos una comuna replica con toda la información de la original
```SQL
CREATE TABLE COMUNA_REPLICA
    AS
SELECT * FROM COMUNA; 
```

- Copiar tabla pero con indicando atributos específicos
```SQL
	CREATE TABLE EMPLEADO_RESPALDO
	    AS
	SELECT 
		nombre_emp,
		numrut_emp
	FROM
		empleado;
```