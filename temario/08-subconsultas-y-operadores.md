# 08. Subconsultas y Operadores Avanzados

Una subconsulta es una sentencia `SELECT` anidada dentro de otra consulta principal (en las cláusulas `WHERE`, `HAVING` o `FROM`)[cite: 95, 128, 218]. La subconsulta se ejecuta en primer lugar y su resultado alimenta a la consulta externa[cite: 95, 128].

## 1. Subconsultas Mono-Registro
Devuelven una única fila con un único valor[cite: 98, 99, 130]. Utilizan operadores relacionales tradicionales (`=`, `>`, `<`, `>=`, `<=`, `<>`)[cite: 99, 130]:

```sql
SELECT ename, sal
FROM emp
WHERE sal > (SELECT sal FROM emp WHERE empno = 7566);
```

## 2. Subconsultas Multi-Registro
Devuelven múltiples filas[cite: 98, 105, 130]. Requieren operadores de conjunto[cite: 105]:

- **`IN`:** Comprueba si el valor coincide con alguno de la lista[cite: 105, 130, 223].
- **`ANY` (o `SOME`):** Devuelve verdadero si la comparación es cierta para al menos uno de los valores[cite: 105, 106, 131, 132, 225].
  - `> ANY(10, 20, 30)` significa mayor que el mínimo (mayor que 10)[cite: 132].
- **`ALL`:** Devuelve verdadero si la comparación es cierta para todos los valores de la lista[cite: 105, 107, 131, 132, 225].
  - `> ALL(10, 20, 30)` significa mayor que el máximo (mayor que 30)[cite: 132].

```sql
-- Empleados que ganan más que todos los salarios medios por departamento
SELECT empno, ename, sal
FROM emp
WHERE sal > ALL (SELECT AVG(sal) FROM emp GROUP BY deptno);
```

## 3. Test de Existencia (`EXISTS` / `NOT EXISTS`)
Evalúa si la subconsulta devuelve filas (devuelve un booleano `TRUE`/`FALSE` sin transportar datos)[cite: 133, 224]:

```sql
SELECT dname
FROM dept d
WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);
```

## 4. Subconsultas Correlacionadas
Hacen referencia a columnas de la consulta externa, evaluándose una vez por cada fila analizada por el bloque principal[cite: 247, 248]:

```sql
-- Empleados cuyo salario es igual al máximo salario de su propio departamento
SELECT *
FROM emp e
WHERE sal = (SELECT MAX(sal) FROM emp WHERE deptno = e.deptno);
```

## 5. Operadores de Conjuntos

Permiten combinar los resultados de dos consultas independientes con idéntico número y tipo de columnas[cite: 243, 246]:

- `UNION`: Une los resultados suprimiendo duplicados[cite: 243].
- `UNION ALL`: Une los resultados conservando duplicados[cite: 243].
- `INTERSECT`: Muestra únicamente las filas presentes en ambas consultas[cite: 244].
- `MINUS`: Devuelve las filas de la primera consulta que no están presentes en la segunda[cite: 245].
