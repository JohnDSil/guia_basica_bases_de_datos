# 05. Consultas Básicas DML y Funciones SQL en Oracle

La sentencia fundamental de consulta es `SELECT`.

## Estructura Básica
```sql
SELECT [DISTINCT] columna1, columna2 AS alias_columna
FROM tabla
WHERE condicion
ORDER BY columna1 ASC, columna2 DESC;
```

- **Proyección:** Selección de columnas específicas.
- **Selección:** Filtrado de filas mediante la cláusula `WHERE`.
- **`DISTINCT`:** Elimina registros repetidos en la salida.
- **`ORDER BY`:** Ordena el resultado de forma ascendente (`ASC`, por defecto) o descendente (`DESC`).

## Funciones SQL Integradas en Oracle

### 1. Aritméticas
- `ROUND(n, m)`: Redondea $n$ a $m$ decimales.
- `TRUNC(n, m)`: Trunca $n$ a $m$ decimales.
- `MOD(m, n)`: Resto entero de dividir $m$ entre $n$.
- `NVL(columna, valor_reemplazo)`: Sustituye valores nulos por el valor indicado.

### 2. Cadenas de Caracteres
- `LOWER(cad)` / `UPPER(cad)`: Transforma a minúsculas o mayúsculas.
- `SUBSTR(cad, inicio, longitud)`: Extrae una porción de texto.
- `LENGTH(cad)`: Devuelve la cantidad de caracteres.
- `LPAD(cad, longitud, relleno)`: Añade caracteres a la izquierda.

### 3. Fechas
- `SYSDATE`: Devuelve la fecha y hora actual del sistema operativo.
- `ADD_MONTHS(fecha, n)`: Suma $n$ meses a una fecha.
- `MONTHS_BETWEEN(f1, f2)`: Diferencia en meses entre dos fechas.

### 4. Conversión de Tipos
- `TO_CHAR(fecha_o_numero, 'formato')`: Convierte a texto con máscara.
- `TO_DATE('cadena', 'formato')`: Convierte texto a formato de fecha.
- `TO_NUMBER('cadena')`: Convierte texto a valor numérico.

```sql
SELECT ename, 
       sal, 
       NVL(comm, 0) AS comision, 
       sal + NVL(comm, 0) AS remuneracion_total,
       TO_CHAR(hiredate, 'DD-Month-YYYY') AS fecha_ingreso
FROM emp
WHERE deptno = 10;
```
