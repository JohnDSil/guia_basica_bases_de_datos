# 01. Entorno, Creación de Usuarios y Esquemas en Oracle

En Oracle existe una arquitectura basada en contenedores (CDB) y bases de datos conectables (PDB)[cite: 158]. Por regla general, el trabajo de desarrollo y prácticas se ejecuta dentro de la PDB asignada (habitualmente `xepdb1`)[cite: 158].

## Procedimiento Inicial de Configuración

Para no trabajar directamente sobre el usuario administrativo `SYSTEM`, se crea un usuario de trabajo que actúa como propietario de su propio **esquema** (conjunto de tablas, vistas e índices)[cite: 158].

### 1. Conexión al servicio `xepdb1` como administrador:
```sql
CONNECT system@xepdb1;
```

### 2. Creación del usuario y asignación de privilegios:
```sql
-- 1. Creación del usuario con su contraseña
CREATE USER nombre_usuario IDENTIFIED BY password_usuario;

-- 2. Concesión de roles básicos:
-- CONNECT: Permite iniciar sesión en la base de datos
-- RESOURCE: Permite crear objetos de esquema (tablas, secuencias, disparadores)
GRANT CONNECT, RESOURCE TO nombre_usuario;

-- 3. Asignación de cuota de almacenamiento sobre el tablespace de trabajo
ALTER USER nombre_usuario QUOTA UNLIMITED ON USERS;
```

### 3. Conexión con el nuevo usuario de trabajo:
```sql
CONNECT nombre_usuario/password_usuario@xepdb1;

-- Comprobar usuario activo
SHOW USER;
```
