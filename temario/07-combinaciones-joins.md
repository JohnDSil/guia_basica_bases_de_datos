# 07. Combinación de Múltiples Tablas (JOINS)

Permite relacionar registros de distintas entidades a través de sus claves primarias y foráneas.

## 1. Producto Cartesiano
Ocurre cuando se omiten las condiciones de enlace en el `WHERE`, multiplicando cada fila de una tabla por todas las filas de la otra.
*(Si la tabla A tiene 14 filas y la B tiene 4, el resultado arroja $14 \times 4 = 56$ filas erróneas)*.

## 2. Equijoin (Combinación Interna / INNER JOIN)
Muestra únicamente las filas que encuentran correspondencia exacta en ambas tablas:

### Sintaxis Tradicional (con condición en WHERE):
```sql
SELECT e.empno, e.ename, e.deptno, d.dname, d.loc
FROM emp e, dept d
WHERE e.deptno = d.deptno;
```

### Sintaxis Estándar ANSI SQL (`INNER JOIN`):
```sql
SELECT e.empno, e.ename, d.dname
FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno;
```

## 3. Non-Equijoins
Combinaciones donde el criterio de unión no utiliza el operador igual (`=`), sino un rango mediante `BETWEEN`:
```sql
SELECT e.ename, e.sal, s.grade
FROM emp e, salgrade s
WHERE e.sal BETWEEN s.losal AND s.hisal;
```

## 4. Combinaciones Externas (Outer Joins)
Permiten visualizar todas las filas de una tabla, incluso si no tienen filas relacionadas en la otra tabla:

### Sintaxis Clásica de Oracle (Operador `(+)`):
El operador `(+)` se coloca en el lado que carece de información (el lado que completará con nulos):
```sql
-- Muestra todos los departamentos, tengan o no empleados
SELECT d.deptno, d.dname, e.ename
FROM emp e, dept d
WHERE e.deptno(+) = d.deptno;
```

### Sintaxis ANSI (`LEFT JOIN` / `RIGHT JOIN`):
```sql
SELECT d.deptno, d.dname, e.ename
FROM dept d
LEFT JOIN emp e ON d.deptno = e.deptno;
```

## 5. Self-Join (Combinación con la Misma Tabla)
Permite relacionar una tabla consigo misma usando alias diferentes (ejemplo: vincular al empleado con su jefe):
```sql
SELECT trabajador.ename || ' trabaja para ' || jefe.ename AS jerarquia
FROM emp trabajador, emp jefe
WHERE trabajador.mgr = jefe.empno;
```
