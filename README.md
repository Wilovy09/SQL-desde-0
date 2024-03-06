# Aprendiendo SQL / SQLite

[MIN: 01:26:10](https://youtu.be/DFg1V-rO6Pg?si=6FaMEJAtSyI17vUn)

## ¿Qué es SQL?

El lenguaje de consulta estructurada (SQL) es un lenguaje de programación para almacenar y procesar información en una base de datos relacional. Una base de datos relacional almacena información en forma de tabla, con filas y columnas que representan diferentes atributos de datos y las diversas relaciones entre los valores de datos. Puede usar las instrucciones SQL para almacenar, actualizar, eliminar, buscar y recuperar información de la base de datos. También puede usar SQL para mantener y optimizar el rendimiento de la base de datos.

## Tipos de datos en SQL

- `INT / INTEGER`, almacena números enteros.
- `TEXT`, utilizado para almacenar cadenas de texto de longitud variable.
- `BLOB`, (Binary Large Object) se utiliza para almacenar `datos binarios`, como `imágenes`, archivos `PDF` u `otros` tipos de archivos.
- `REAL`, almacena números de punto flotante de precisión simple.
  - Es de 8 bits.
  - Es mas rapido.
- `NUMERIC`,  almacena números con precisión exacta, incluyendo valores decimales.
  - No tiene limite.
  - Son valores muy precisos y largos (Pi).

## Comentarios en código SQL

Como todo leguaje, dentro de SQL se pueden poner comentarios en el código para evitar que esa porción sea procesada.

```sql
-- Este es un comentario de una sola linea
```

```sql
/*
    Este es un 
    comentario 
    multilinea
*/
```

## Crear tablas

Utilizamos `CREATE TABLE 'NOMBRE_TABLA' ()` para crear nuestra tabla y dentro de los `()` agregaremos sus columnas.

```sql
CREATE TABLE 'MiPrimeraTabla' (
    'nombre' TEXT
);
```

## Valores por defecto

Podemos asignar un valor por defecto si es que el usuario no lo ingresa.

Para lograr esto agregamos `DEFAULT 'VALOR'` en nuestra columna.

```sql
CREATE TABLE MiPrimeraTabla (
    'nombre' TEXT DEFAULT 'Wilovy',
    'apellido' TEXT,
    'edad' INT
);
```

## Borrar tablas

Para borrar toda una tabla usaremos `DROP TABLE 'NOMBRE_TABLA'`.

```sql
DROP TABLE MiPrimeraTabla
```

## Consultas - Querys

- `C`reate
- `R`ead
- `U`pdate
- `D`elete

### Seleccionar - SELECT

#### Seleccionar todo - *

Para seleccionar todo usamos el operador `*`, usamos `SELECT * FROM 'NOMBRE_TABLA'`

```sql
SELECT * FROM 'MiPrimeraTabla'
```

#### Seleccionar solo una columna

Podemos extraer la información de solo una columna usando `SELECT 'NOMBRE_COLUMNA' FROM 'NOMBRE_TABLA'`.

```sql
SELECT 'NOMBRE_COLUMNA' FROM 'NOMBRE_TABLA'
```

Tambien podemos extrar la información de 2 o más columnas separandolas por `,`.

```sql
SELECT 'NOMBRE_COLUMNA','NOMBRE_COLUMNA' FROM 'NOMBRE_TABLA'
```

### Insertar datos - INSERT INTO

Para insertar datos pondremos `INSERT INTO NOMBRE_TABLA (columna_afectada1,columna_afectada2) VALUES ('valor1','valor2')`.

TEXTO SIEMPRE VA ENTRE COMILLAS `'TEXT'` o `"TEXTO"`.

```sql
INSERT INTO MiPrimeraTabla (nombre,apellido,edad) VALUES ('Wilovy','Garza',22)
```

Para insertar varios datos a la vez los `VALUES` los separamos por una `,`

```sql
INSERT INTO MiPrimeraTabla (nombre,apellido,edad)
VALUES ('Wilovy','Garza',22),
       ('Wilovy','Maldonado',23),
       ('Wilovy','Github',24)
```

### Borrar registros - DELETE

Para borrar registros (filas) usamos `DELETE FROM 'MiPrimeraTabla'`

```sql
DELETE FROM 'MiPrimeraTabla' 
```

## Identificadores

### Llaves primarias - PRIMARY KEY

- No pueden ser `NULL`.

Funciona para identificar/diferenciar el registro.

- `INTEGER`, tipo INT.
- `PRIMARY KEY`, es nuestra llave primaria.
- `AUTOINCREMENT`, queremos que se auto incremente (`ultimo_id + 1` en cada registro).

```sql
CREATE TABLE MiPrimeraTabla (
    'id' INTEGER PRIMARY KEY AUTOINCREMENT,
    'nombre' TEXT,
    'apellido' TEXT,
    'edad' INT
);
```

### Llaves foraneas - FOREIGN KEY

Las **llaves foraneas (foreign key)** no pueden ser una llave foranea si no esta haciendo referencia a una **llave primaria (primary key)**.

Para lograr crear la **FOREIGN KEY** usamos `FOREIGN KEY (columna) REFERENCES nombre_tabla (columna)`

Para llevar acabo esto, tenemos que crear unas tablas mas realistas

```sql
CREATE TABLE usuarios (
    'id' INTEGER PRIMARY KEY AUTOINCREMENT,
    'nombre' TEXT,
    'apellido' TEXT,
    'edad' INT
);

CREATE TABLE turnos_medicos (
    'id' INTEGER PRIMARY KEY AUTOINCREMENT,
    'profesional' TEXT,
    'motivo' TEXT,
    'id_usuario' INT,
    'horario' TEXT,
    FOREIGN KEY (id_usuario) REFERENCES usuarios (id)
)
```

Insertamos unos valores

```sql
INSERT INTO usuarios (nombre,apellido,edad)
VALUES ('Wilovy','Garza',22);

INSERT INTO turnos_medicos (profesional,motivo,id_usuario,horario)
VALUES ('Doc Wilovy','Dolor de panza',1,'12:30')
```

Si intentamos insertar un valor con un `id_usuario` que no existe, nos dara error

```error
Error while executing SQL query on database 'testDB': FOREIGN KEY constraint failed
```
