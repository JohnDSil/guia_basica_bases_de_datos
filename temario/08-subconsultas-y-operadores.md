# 08. Subconsultas y Operadores Avanzados

Una subconsulta es una sentencia `SELECT` anidada dentro de otra consulta principal (en las cláusulas `WHERE`, `HAVING` o `FROM`). La subconsulta se ejecuta en primer lugar y su resultado alimenta a la consulta externa.

## 1. Subconsultas Mono-Registro
Devuelven una única fila con un único valor. Utilizan operadores relacionales tradicionales (`=`, `>`, `<`, `>=`, `<=`, `<>`):

```sql
SELECT ename, sal
FROM emp
WHERE sal > (SELECT sal FROM emp WHERE empno = 7566);
```

## 2. Subconsultas Multi-Registro
Devuelven múltiples filas. Requieren operadores de conjunto:

- **`IN`:** Comprueba si el valor coincide con alguno de la lista.
- **`ANY` (o `SOME`):** Devuelve verdadero si la comparación es cierta para al menos uno de los valores.
  - `> ANY(10, 20, 30)` significa mayor que el mínimo (mayor que 10).
- **`ALL`:** Devuelve verdadero si la comparación es cierta para todos los valores de la lista.
  - `> ALL(10, 20, 30)` significa mayor que el máximo (mayor que 30).

```sql
-- Empleados que ganan más que todos los salarios medios por departamento
SELECT empno, ename, sal
FROM emp
WHERE sal > ALL (SELECT AVG(sal) FROM emp GROUP BY deptno);
```

## 3. Test de Existencia (`EXISTS` / `NOT EXISTS`)
Evalúa si la subconsulta devuelve filas (devuelve un booleano `TRUE`/`FALSE` sin transportar datos):

```sql
SELECT dname
FROM dept d
WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);
```

## 4. Subconsultas Correlacionadas
Hacen referencia a columnas de la consulta externa, evaluándose una vez por cada fila analizada por el bloque principal:

```sql
-- Empleados cuyo salario es igual al máximo salario de su propio departamento
SELECT *
FROM emp e
WHERE sal = (SELECT MAX(sal) FROM emp WHERE deptno = e.deptno);
```

## 5. Operadores de Conjuntos

Permiten combinar los resultados de dos consultas independientes con idéntico número y tipo de columnas:

- `UNION`: Une los resultados suprimiendo duplicados.
- `UNION ALL`: Une los resultados conservando duplicados.
- `INTERSECT`: Muestra únicamente las filas presentes en ambas consultas.
- `MINUS`: Devuelve las filas de la primera consulta que no están presentes en la segunda.
