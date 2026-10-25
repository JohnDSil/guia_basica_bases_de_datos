# 06. Funciones de Grupo y Cláusulas GROUP BY / HAVING

Las funciones de grupo o agregación procesan conjuntos de filas para devolver un único dato resumen por cada conjunto[cite: 67, 123].

## Funciones de Agregación
- `COUNT(*)`: Cuenta todas las filas del conjunto[cite: 68, 124, 171].
- `COUNT(columna)`: Cuenta únicamente las filas cuyo valor en esa columna no sea nulo[cite: 73, 124].
- `SUM(columna)`: Suma acumulada de valores numéricos[cite: 68, 70, 124, 171].
- `AVG(columna)`: Promedio aritmético (ignora nulos automáticamente)[cite: 68, 70, 74, 124, 171].
- `MIN(columna)` / `MAX(columna)`: Valor mínimo y máximo (admiten números, texto y fechas)[cite: 68, 71, 124, 171].

## Cláusula `GROUP BY`
Permite segmentar la tabla en grupos para calcular subtotales[cite: 76, 77, 126]:

> **Regla Crítica:** Toda columna que aparezca en la cláusula `SELECT` y no esté dentro de una función de grupo, **debe estar incluida obligatoriamente** en la cláusula `GROUP BY`[cite: 78, 82, 126].

```sql
SELECT deptno, job, COUNT(*) AS total_empleados, AVG(sal) AS salario_medio
FROM emp
GROUP BY deptno, job;
```

## Cláusula `HAVING`
Filtra grupos de filas después de calcular la agregación (el `WHERE` filtra registros individuales antes de agrupar)[cite: 83, 85, 127, 240]:

```sql
SELECT deptno, AVG(sal) AS salario_medio
FROM emp
WHERE job <> 'PRESIDENT'        -- Filtro a nivel de fila individual
GROUP BY deptno
HAVING AVG(sal) > 2000          -- Filtro a nivel de grupo
ORDER BY salario_medio DESC;
```
