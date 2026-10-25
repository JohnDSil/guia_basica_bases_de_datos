# 11. Scripts de Limpieza y Mantenimiento

En entornos de prácticas o antes de comenzar un examen, es común requerir la eliminación completa de los objetos existentes en el esquema de usuario sin necesidad de destruir la cuenta.

## Script de Borrado Masivo en PL/SQL

El siguiente bloque anónimo PL/SQL consulta la vista `USER_OBJECTS`, itera sobre todas las tablas, vistas, secuencias y paquetes del usuario y ejecuta su borrado en cascada mediante SQL dinámico (`EXECUTE IMMEDIATE`), procediendo luego a borrar los sinónimos públicos asociados:

```sql
BEGIN
  -- 1. Iterar y borrar objetos propiedad del usuario
  FOR cur_rec IN (
    SELECT object_name, object_type
    FROM user_objects
    WHERE object_type IN (
      'TABLE',
      'VIEW',
      'MATERIALIZED VIEW',
      'PACKAGE',
      'PROCEDURE',
      'FUNCTION',
      'SEQUENCE',
      'SYNONYM',
      'PACKAGE BODY'
    )
  )
  LOOP
    BEGIN
      IF cur_rec.object_type = 'TABLE' THEN
        EXECUTE IMMEDIATE 'DROP ' || cur_rec.object_type || ' "' || cur_rec.object_name || '" CASCADE CONSTRAINTS';
      ELSE
        EXECUTE IMMEDIATE 'DROP ' || cur_rec.object_type || ' "' || cur_rec.object_name || '"';
      END IF;
    EXCEPTION
      WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('FAILED: DROP ' || cur_rec.object_type || ' ' || cur_rec.object_name);
    END;
  END LOOP;

  -- 2. Limpieza de sinónimos públicos asociados al esquema
  FOR cur_rec IN (
    SELECT synonym_name 
    FROM all_synonyms 
    WHERE table_owner IN (SELECT USER FROM dual)
  )
  LOOP
    BEGIN
      EXECUTE IMMEDIATE 'DROP PUBLIC SYNONYM "' || cur_rec.synonym_name || '"';
    EXCEPTION
      WHEN OTHERS THEN
        NULL;
    END;
  END LOOP;
END;
/
```
