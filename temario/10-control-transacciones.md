# 10. Control de Transacciones en SQL

Una **transacción** es una secuencia lógica de una o varias sentencias SQL que conforman una unidad de trabajo atómica (principio ACID).

## Instrucciones Fundamentales

- **`COMMIT`:** Guarda y confirma de forma definitiva en el disco todas las modificaciones DML efectuadas desde el inicio de la transacción o desde el último commit.
- **`ROLLBACK`:** Cancela y revierte las modificaciones de la transacción en curso, devolviendo los datos al estado previo al último `COMMIT`.

## Comportamiento de `AUTOCOMMIT`
- En **Oracle SQL\*Plus**, por defecto `AUTOCOMMIT` está en `OFF`[cite: 24]. Las operaciones `INSERT`, `UPDATE` y `DELETE` no se consolidan hasta que se ejecuta explícitamente `COMMIT`.
- Para verificar el estado:
```sql
SHOW AUTOCOMMIT;
```
- Para forzar la validación automática:
```sql
SET AUTOCOMMIT ON;
```

## Bloqueos y Commits Implícitos
Las siguientes acciones provocan un `COMMIT` automático e implícito en la base de datos sin confirmación del usuario:
- Salida ordenada de la sesión (`QUIT`, `EXIT`, `DISCONNECT`).
- Ejecución de cualquier sentencia DDL (`CREATE`, `ALTER`, `DROP`, `TRUNCATE`).
- Ejecución de sentencias DCL (`GRANT`, `REVOKE`).
