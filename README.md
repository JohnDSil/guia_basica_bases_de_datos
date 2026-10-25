# Gestión de Bases de Datos Relacionales (Oracle SQL)

Repositorio de apuntes técnicos, diseño físico, DDL, DML, agregaciones, subconsultas y control transaccional basado en Oracle Database y SQL estándar para ASIR.

---

## 📑 Índice de Módulos

| Nº | Tema | Archivo | Contenido Temático |
| :---: | :--- | :--- | :--- |
| **01** | Entorno y Usuarios en Oracle | [`01-entorno-y-usuarios.md`](temario/01-entorno-y-usuarios.md) | Conexión a `xepdb1`, roles `CONNECT` y `RESOURCE`, cuota sobre `USERS` y esquemas |
| **02** | Diseño Físico y DDL | [`02-diseno-fisico-ddl.md`](temario/02-diseno-fisico-ddl.md) | Tipos de datos, `CREATE TABLE`, diccionario de datos y vistas (`USER_TABLES`, `DESC`) |
| **03** | Restricciones de Integridad | [`03-restricciones-integridad.md`](temario/03-restricciones-integridad.md) | `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`, `CHECK`, `DEFAULT` y `CASCADE` |
| **04** | Modificación y Borrado de Tablas | [`04-alter-drop-truncate.md`](temario/04-alter-drop-truncate.md) | `ALTER TABLE` (ADD, MODIFY, DROP), `DROP TABLE`, `TRUNCATE` y sinónimos |
| **05** | Consultas DML Básicas y Funciones | [`05-consultas-basicas-funciones.md`](temario/05-consultas-basicas-funciones.md) | `SELECT`, proyección, ordenación, funciones de cadena, numéricas, fechas y conversión |
| **06** | Agregaciones y Agrupamientos | [`06-agrupaciones-group-by-having.md`](temario/06-agrupaciones-group-by-having.md) | Funciones de grupo (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`), `GROUP BY` y filtro `HAVING` |
| **07** | Combinaciones de Tablas (Joins) | [`07-combinaciones-joins.md`](temario/07-combinaciones-joins.md) | Producto cartesiano, equijoins, non-equijoins, `LEFT/RIGHT JOIN`, sintaxis `(+)` y self-joins |
| **08** | Subconsultas y Operadores | [`08-subconsultas-y-operadores.md`](temario/08-subconsultas-y-operadores.md) | Mono-registro, multi-registro (`IN`, `ANY`, `ALL`), `EXISTS` y subconsultas correlacionadas |
| **09** | Operaciones DML de Modificación | [`09-modificacion-dml.md`](temario/09-modificacion-dml.md) | `INSERT INTO ... VALUES`, `INSERT ... SELECT`, `UPDATE` y `DELETE` con subconsultas |
| **10** | Control de Transacciones | [`10-control-transacciones.md`](temario/10-control-transacciones.md) | Unidades de trabajo, `COMMIT`, `ROLLBACK`, autocommit y bloqueos implícitos |
| **11** | Scripts de Limpieza y Mantenimiento | [`11-scripts-mantenimiento.md`](temario/11-scripts-mantenimiento.md) | Bloques anónimos PL/SQL para borrado masivo de objetos y sinónimos |

---

## 🛠️ Entorno de Trabajo
- **Motor SGBD:** Oracle Database Express Edition (XE) / Enterprise Edition.
- **Pluggable Database:** Servicio de base de datos conectable `xepdb1`.
- **Cliente:** SQL*Plus, SQL Developer o DBeaver[cite: 25].
