# 05. Consultas Básicas DML y Funciones SQL en Oracle

La sentencia fundamental de consulta es `SELECT`[cite: 209].

## Estructura Básica
```sql
SELECT [DISTINCT] columna1, columna2 AS alias_columna
FROM tabla
WHERE condicion
ORDER BY columna1 ASC, columna2 DESC;
```

- **Proyección:** Selección de columnas específicas[cite: 213].
- **Selección:** Filtrado de filas mediante la cláusula `WHERE`[cite: 214].
- **`DISTINCT`:** Elimina registros repetidos en la salida[cite: 210].
- **`ORDER BY`:** Ordena el resultado de forma ascendente (`ASC`, por defecto) o descendente (`DESC`)[cite: 216].

## Funciones SQL Integradas en Oracle

### 1. Aritméticas
- `ROUND(n, m)`: Redondea $n$ a $m$ decimales[cite: 169].
- `TRUNC(n, m)`: Trunca $n$ a $m$ decimales[cite: 169].
- `MOD(m, n)`: Resto entero de dividir $m$ entre $n$[cite: 169].
- `NVL(columna, valor_reemplazo)`: Sustituye valores nulos por el valor indicado[cite: 169].

### 2. Cadenas de Caracteres
- `LOWER(cad)` / `UPPER(cad)`: Transforma a minúsculas o mayúsculas[cite: 173].
- `SUBSTR(cad, inicio, longitud)`: Extrae una porción de texto[cite: 173].
- `LENGTH(cad)`: Devuelve la cantidad de caracteres[cite: 175].
- `LPAD(cad, longitud, relleno)`: Añade caracteres a la izquierda[cite: 173].

### 3. Fechas
- `SYSDATE`: Devuelve la fecha y hora actual del sistema operativo[cite: 176].
- `ADD_MONTHS(fecha, n)`: Suma $n$ meses a una fecha[cite: 176].
- `MONTHS_BETWEEN(f1, f2)`: Diferencia en meses entre dos fechas[cite: 176].

### 4. Conversión de Tipos
- `TO_CHAR(fecha_o_numero, 'formato')`: Convierte a texto con máscara[cite: 177].
- `TO_DATE('cadena', 'formato')`: Convierte texto a formato de fecha[cite: 177].
- `TO_NUMBER('cadena')`: Convierte texto a valor numérico[cite: 177].

```sql
SELECT ename, 
       sal, 
       NVL(comm, 0) AS comision, 
       sal + NVL(comm, 0) AS remuneracion_total,
       TO_CHAR(hiredate, 'DD-Month-YYYY') AS fecha_ingreso
FROM emp
WHERE deptno = 10;
```
