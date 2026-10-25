# 04. Modificación de Tablas, Borrado y Sinónimos

## Modificación de Estructura (`ALTER TABLE`)

Permite añadir, modificar o eliminar columnas y restricciones sin destruir la tabla[cite: 196]:

### 1. Añadir columnas (`ADD`):
```sql
ALTER TABLE empleados ADD (email VARCHAR2(50));
```

### 2. Modificar columnas (`MODIFY`):
```sql
-- Ampliar el tamaño de un campo
ALTER TABLE empleados MODIFY (ename VARCHAR2(20));

-- Hacer obligatoria una columna (solo si no existen filas con valores nulos)
ALTER TABLE empleados MODIFY (email NOT NULL);
```

### 3. Eliminar columnas (`DROP COLUMN`):
```sql
ALTER TABLE empleados DROP COLUMN email;
```

### 4. Gestión de Restricciones:
```sql
-- Añadir restricción
ALTER TABLE empleados ADD CONSTRAINT ck_sal_min CHECK (sal >= 600);

-- Desactivar y activar restricción (útil en cargas masivas)
ALTER TABLE empleados DISABLE CONSTRAINT ck_sal_min;
ALTER TABLE empleados ENABLE CONSTRAINT ck_sal_min;

-- Eliminar restricción
ALTER TABLE empleados DROP CONSTRAINT ck_sal_min;
```

## Borrado de Tablas

### `DROP TABLE`
Elimina la estructura completa, sus datos y los índices asociados[cite: 159, 202].
```sql
-- CASCADE CONSTRAINTS elimina las claves foráneas en otras tablas que apuntaban a esta
DROP TABLE departamentos CASCADE CONSTRAINTS;
```

### `TRUNCATE TABLE`
Instrucción DDL que vacía rápidamente todos los registros de una tabla y libera el espacio de almacenamiento, conservando la definición intacta[cite: 203]. No puede revertirse mediante `ROLLBACK`[cite: 203].
```sql
TRUNCATE TABLE empleados;
```

## Uso de Sinónimos (`SYNONYM`)
Permiten asignar un alias alternativo a un objeto para no usar la sintaxis `esquema.objeto`[cite: 204]:
```sql
-- Crear sinónimo público (requiere privilegios administrativos)
CREATE PUBLIC SYNONYM emp FOR scott.emp;
```
