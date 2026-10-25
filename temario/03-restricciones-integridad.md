# 03. Restricciones de Integridad (Constraints)

Las restricciones aseguran la integridad de los datos evitando que el motor acepte valores incorrectos o que rompan las relaciones del modelo.

## Nomenclatura Recomendada (Oracle)
Oracle aconseja usar nombres estructurados para las restricciones: `TABLA_COLUMNA_TIPO`.
- `PK`: Primary Key
- `FK`: Foreign Key
- `NN`: Not Null
- `UK`: Unique
- `CK`: Check

## Tipos de Restricciones

1. **`PRIMARY KEY`:** Identificador unívoco obligatorio. Genera automáticamente un índice único.
2. **`FOREIGN KEY` (Clave Ajena / Integridad Referencial):** Asocia una columna con la clave primaria de otra tabla.
3. **`NOT NULL`:** Impide que la columna admita valores nulos.
4. **`UNIQUE`:** Evita valores repetidos en la columna, permitiendo nulos.
5. **`CHECK`:** Obliga a cumplir una condición lógica booleana al introducir el dato.
6. **`DEFAULT`:** Asigna un valor predeterminado si el campo se omite en el `INSERT` (no lleva nombre de restricción).

## Ejemplo Completo (Definición a Nivel de Tabla)

```sql
CREATE TABLE departamentos (
    deptno NUMBER(2) CONSTRAINT pk_dept PRIMARY KEY,
    dname  VARCHAR2(14) CONSTRAINT nn_dept_name NOT NULL,
    loc    VARCHAR2(13) CONSTRAINT uk_dept_loc UNIQUE
);

CREATE TABLE empleados (
    empno      NUMBER(4),
    ename      VARCHAR2(10) CONSTRAINT nn_emp_name NOT NULL,
    job        VARCHAR2(9),
    sal        NUMBER(7,2),
    fecha_alt  DATE DEFAULT SYSDATE,
    deptno     NUMBER(2),
    -- Restricciones a nivel de tabla
    CONSTRAINT pk_emp PRIMARY KEY (empno),
    CONSTRAINT ck_emp_sal CHECK (sal > 0),
    CONSTRAINT fk_emp_dept FOREIGN KEY (deptno) 
        REFERENCES departamentos(deptno) 
        ON DELETE CASCADE
);
```

> **Cláusula `ON DELETE CASCADE`:** Si se elimina una fila en la tabla padre (departamentos), Oracle borrará automáticamente todos los empleados asociados a dicho departamento.
