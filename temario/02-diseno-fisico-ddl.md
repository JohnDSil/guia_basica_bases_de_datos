# 02. Diseño Físico de Tablas y Diccionario de Datos

El diseño físico define los tipos de datos, longitudes y especificaciones técnicas de almacenamiento para cada entidad de la base de datos[cite: 154, 179].

## Tipos de Datos Principales en Oracle

- `VARCHAR2(tamaño)`: Cadenas de caracteres de longitud variable (hasta 4000 bytes)[cite: 161].
- `CHAR(tamaño)`: Cadenas de caracteres de longitud fija (hasta 2000 bytes, rellena con espacios)[cite: 161].
- `NUMBER(precisión, escala)`: Tipo numérico exacto[cite: 161]. La precisión indica el número total de dígitos y la escala la cantidad de decimales[cite: 161]. Ejemplo: `NUMBER(7,2)`[cite: 161].
- `DATE`: Fechas que almacenan siglo, año, mes, día, horas, minutos y segundos[cite: 161].
- `CLOB`: Grandes volúmenes de datos de tipo carácter (más de 2 GB)[cite: 161].
- `BLOB`: Grandes volúmenes de datos binarios (imágenes, audio, documentos compilados)[cite: 161].

## Creación Básica de Tablas (`CREATE TABLE`)

Las tablas deben identificarse con un nombre autodescriptivo que comience por letra (máximo 30 caracteres) y que no sea palabra reservada[cite: 179].

```sql
CREATE TABLE alumnos (
    num_matri  NUMBER(6),
    nombre     VARCHAR2(25),
    fecha_nac  DATE,
    direccion  VARCHAR2(50)
);
```

## Vistas del Diccionario de Datos para Tablas

El diccionario almacena los metadatos de los objetos creados[cite: 181, 194]:

- `USER_TABLES` (o sinónimo `CAT`): Lista las tablas que pertenecen al usuario conectado[cite: 181].
- `ALL_TABLES`: Tablas que pertenecen al usuario o sobre las cuales tiene permisos concedidos[cite: 181].
- `DBA_TABLES`: Lista la totalidad de tablas de la base de datos (requiere privilegios de DBA)[cite: 181].

Para inspeccionar la estructura de campos de una tabla:
```sql
DESCRIBE alumnos;
-- O en formato abreviado:
DESC alumnos;
```
