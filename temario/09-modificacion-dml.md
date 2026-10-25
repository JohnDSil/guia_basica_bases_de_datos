# 09. Modificación de Datos: Inserción, Actualización y Borrado

El Lenguaje de Manipulación de Datos (DML) altera el contenido de las tablas.

## 1. Inserción de Registros (`INSERT`)

### Inserción simple de valores literales:
```sql
INSERT INTO profesores (id_profesor, apellidos, especialidad, cod_centro)
VALUES (101, 'Quiroga Martín, Mª Isabel', 'INFORMATICA', 45);
```

### Inserción mediante consultas (Consultas de datos anexados):
Permite traspasar datos entre tablas:
```sql
INSERT INTO emp_historico (empno, ename, sal, deptno)
SELECT empno, ename, sal, deptno
FROM emp
WHERE deptno = 10;
```

## 2. Modificación de Registros (`UPDATE`)

Si se omite la cláusula `WHERE`, **se actualizarán absolutamente todas las filas de la tabla**.

```sql
UPDATE emp
SET sal = sal + 100,
    comm = NVL(comm, 0) + 10
WHERE empno = 7369;
```

### Consultas de Actualización con Subconsultas:
```sql
-- Actualiza los salarios de los empleados de ACCOUNTING con el doble del salario de JAMES
UPDATE emp
SET sal = (SELECT sal * 2 FROM emp WHERE ename = 'JAMES')
WHERE deptno = (SELECT deptno FROM dept WHERE dname = 'ACCOUNTING');
```

## 3. Borrado de Registros (`DELETE`)

Elimina filas completas que satisfacen una condición. Si se omite `WHERE`, se vacía la tabla por completo:

```sql
DELETE FROM emp
WHERE deptno = (SELECT deptno FROM dept WHERE loc = 'CHICAGO');
```
