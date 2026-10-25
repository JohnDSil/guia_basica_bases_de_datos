# 02. Diseño Físico de Tablas y Diccionario de Datos

El diseño físico define los tipos de datos, longitudes y especificaciones técnicas de almacenamiento para cada entidad de la base de datos.

## Tipos de Datos Principales en Oracle

- `VARCHAR2(tamaño)`: Cadenas de caracteres de longitud variable (hasta 4000 bytes).
- `CHAR(tamaño)`: Cadenas de caracteres de longitud fija (hasta 2000 bytes, rellena con espacios).
- `NUMBER(precisión, escala)`: Tipo numérico exacto. La precisión indica el número total de dígitos y la escala la cantidad de decimales[cite: 161]. Ejemplo: `NUMBER(7,2)`.
- `DATE`: Fechas que almacenan siglo, año, mes, día, horas, minutos y segundos.
- `CLOB`: Grandes volúmenes de datos de tipo carácter (más de 2 GB).
- `BLOB`: Grandes volúmenes de datos binarios (imágenes, audio, documentos compilados).

## Creación Básica de Tablas (`CREATE TABLE`)

Las tablas deben identificarse con un nombre autodescriptivo que comience por letra (máximo 30 caracteres) y que no sea palabra reservada.

```sql
CREATE TABLE alumnos (
    num_matri  NUMBER(6),
    nombre     VARCHAR2(25),
    fecha_nac  DATE,
    direccion  VARCHAR2(50)
);
```

## Vistas del Diccionario de Datos para Tablas

El diccionario almacena los metadatos de los objetos creados:

- `USER_TABLES` (o sinónimo `CAT`): Lista las tablas que pertenecen al usuario conectado.
- `ALL_TABLES`: Tablas que pertenecen al usuario o sobre las cuales tiene permisos concedidos.
- `DBA_TABLES`: Lista la totalidad de tablas de la base de datos (requiere privilegios de DBA).

Para inspeccionar la estructura de campos de una tabla:
```sql
DESCRIBE alumnos;
-- O en formato abreviado:
DESC alumnos;
```
