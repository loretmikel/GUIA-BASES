# 🎯 GUÍA DEFINITIVA — EXAMEN FINAL BASES DE DATOS (ITAM, COM-12101)

> Guía construida a partir de: **Tema 1** (Introducción), **Tema 2** (Consultas SQL), **Tema 3** (DDL/DML), **Tema 4** (Normalización), **ERD de Fotomultas CDMX** y **Examen tipo Final (YouTube)**.
>
> Esta guía no es un resumen bonito. Es un arma de búsqueda rápida. Usa **Ctrl+F** agresivamente.

---

## 📑 TABLA DE CONTENIDO

1. [Cómo usar esta guía eficientemente](#-cómo-usar-esta-guía-eficientemente)
2. [Mapa mental de keywords del documento](#-mapa-mental-de-keywords-del-documento)
3. [Detección de patrones del examen (PRIORIDADES)](#-detección-de-patrones-del-examen-prioridades)
4. **TEORÍA**
   - [TEMA 1 — Introducción a las bases de datos](#tema-1--introducción-a-las-bases-de-datos)
   - [TEMA 2 — Consultas SQL](#tema-2--consultas-sql)
   - [TEMA 3 — Definición y modificación de datos (DDL/DML)](#tema-3--definición-y-modificación-de-datos-en-sql)
   - [TEMA 4 — Normalización](#tema-4--normalización)
5. [ANÁLISIS PROFUNDO DEL ERD — Fotomultas CDMX](#-análisis-profundo-del-erd--fotomultas-cdmx)
6. [Tablas rápidas de referencia (cheat sheet)](#-tablas-rápidas-de-referencia-cheat-sheet)
7. **EJERCICIOS RESUELTOS** (cada uno con keywords + enunciado + solución paso a paso + respuesta final)
   - [Bloque A — Conceptual / Teoría](#bloque-a--ejercicios-conceptuales)
   - [Bloque B — ERD, cardinalidad, llaves](#bloque-b--ejercicios-de-erd-y-cardinalidad)
   - [Bloque C — SQL: JOINs y consultas básicas](#bloque-c--joins-y-consultas-básicas)
   - [Bloque D — Aggregation, GROUP BY, HAVING](#bloque-d--aggregation-group-by-having)
   - [Bloque E — Subconsultas y EXISTS](#bloque-e--subconsultas-y-exists)
   - [Bloque F — Window functions](#bloque-f--funciones-de-ventana)
   - [Bloque G — DDL: CREATE / ALTER / constraints](#bloque-g--ddl-create-alter-constraints)
   - [Bloque H — DML: INSERT / UPDATE / DELETE](#bloque-h--dml-insert-update-delete)
   - [Bloque I — Normalización, DFs y DMVs](#bloque-i--normalización-dfs-y-dmvs)
   - [Bloque J — Debugging y preguntas tramposas](#bloque-j--debugging-y-preguntas-tramposas)
   - [Bloque K — Ejercicios MUY difíciles estilo final ITAM](#bloque-k--ejercicios-muy-difíciles-estilo-final-itam)

---

## 🧭 Cómo usar esta guía eficientemente

### Estrategia 1-2 días antes del examen

**Día 1 (la víspera o dos días antes):**
1. Lee de un tirón toda la sección de **Detección de patrones** y memoriza qué temas tienen alta probabilidad.
2. Lee toda la sección de **TEORÍA** marcando con resaltador todo lo que NO recuerdes inmediatamente.
3. Lee el **Análisis del ERD de Fotomultas** dos veces.
4. Resuelve los **Bloques A, B, C, D** sin ver la solución; compara después.

**Día 2 (día del examen, mañana):**
1. Revisa solo las **tablas rápidas de referencia (cheat sheet)**.
2. Resuelve **Bloque K** (los muy difíciles); si los entiendes, estás listo.
3. Repasa las **trampas típicas** marcadas en cada ejercicio.

### Método de búsqueda rápida con Ctrl+F

| Si buscas… | Usa Ctrl+F con… |
|---|---|
| Un tipo de JOIN | `LEFT JOIN`, `INNER JOIN`, `RIGHT JOIN`, `FULL OUTER`, `CROSS JOIN`, `NATURAL JOIN` |
| Una función agregada | `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`, `DISTINCT` |
| WHERE vs HAVING | `WHERE vs HAVING` |
| Subconsultas | `subquery`, `subconsulta`, `correlacionada`, `EXISTS`, `IN` |
| Window functions | `window`, `OVER`, `PARTITION BY`, `RANGE`, `ROWS`, `GROUPS`, `LAG`, `LEAD`, `RANK`, `ROW_NUMBER` |
| CREATE TABLE | `CREATE TABLE`, `constraint`, `CHECK`, `FOREIGN KEY`, `PRIMARY KEY`, `UNIQUE`, `NOT NULL` |
| Modificar tablas | `ALTER TABLE`, `ADD COLUMN`, `DROP COLUMN`, `RENAME`, `SET DEFAULT` |
| Cardinalidad | `cardinalidad`, `uno a muchos`, `muchos a muchos`, `obligatoria`, `opcional` |
| Llaves del ERD | `propietario_id`, `vehiculo_id`, `camara_id`, `infraccion_id`, `acreedor_id`, `creador_id`, `usuario_id` |
| Normalización | `FNBC`, `4FN`, `1FN`, `2FN`, `3FN`, `dependencia funcional`, `dependencia multivaluada`, `DMV`, `trivial` |
| ERD Fotomultas | `infraccion`, `camara`, `vehiculo`, `propietario`, `pago`, `fotomultas` |
| Tablas de YouTube | `usuario`, `video`, `comentario`, `suscripcion`, `reproduccion` |
| Anomalías | `anomalía de inserción`, `anomalía de borrado`, `anomalía de modificación` |
| Debugging | `debugging`, `error`, `trampa`, `incorrecta` |
| Dificultad | `examen difícil`, `MUY difícil`, `fácil`, `media` |

### Cómo usar los ejercicios (formato activo)

Cada ejercicio tiene:
- **Keywords para buscar:** lista enorme — busca un keyword aquí y aparecerán TODOS los ejercicios similares.
- **Tipo de pregunta:** conceptual / SQL / ERD / debugging / normalización / constraints.
- **Dificultad:** fácil, media, difícil, MUY difícil.
- **Patrones relacionados:** otros ejercicios o conceptos similares.
- **Trampas típicas:** lo que el profesor te tiende a poner.
- **Enunciado.**
- **Solución paso a paso.**
- **Respuesta final.**

Lee el enunciado, **intenta resolver en tu cabeza o en papel**, baja a la solución y compara.

---

## 🧠 Mapa mental de keywords del documento

Para que tu Ctrl+F sea quirúrgico, esta es la nomenclatura recurrente:

- **Relvar** = "variable de relación" = tabla con esquema fijo y restricciones.
- **Relación (r)** = par ordenado `(E, e)` donde E es el encabezado y e el cuerpo (conjunto de tuplas).
- **Tupla** = renglón.
- **DF** = Dependencia Funcional `X → Y`.
- **DMV** = Dependencia Multivaluada `X ↠ Y`.
- **FNBC** = Forma Normal de Boyce-Codd.
- **4FN** = Cuarta Forma Normal.
- **PK** = Primary Key / llave primaria.
- **FK** = Foreign Key / llave foránea.
- **SK** = Súper llave.
- **DDL** = Data Definition Language (CREATE, ALTER, DROP).
- **DML** = Data Manipulation Language (INSERT, UPDATE, DELETE, SELECT).
- **DCL** = Data Control Language (GRANT, REVOKE).
- **CTE** = Common Table Expression (`WITH ... AS`).
- **FRAME CLAUSE** = parte del `OVER(...)` que define qué renglones entran a la ventana (`RANGE`, `ROWS`, `GROUPS`).

---

## 🔥 Detección de patrones del examen (PRIORIDADES)

Después de analizar **las diapositivas + ERD + examen tipo final**, estos son los temas con mayor probabilidad de venir, en orden de importancia:

### 🟥 PROBABILIDAD ALTÍSIMA (siempre cae algo de esto)

1. **Identificar llaves foráneas en un ERD y la cardinalidad de cada relación.**
   *Apareció literalmente como Pregunta 1 en el examen práctica. Es OBLIGATORIO saber leer notación crow's foot.*
2. **Query SQL con JOIN entre tabla pivote / tabla principal + filtros + ORDER BY.**
   *Pregunta 6 del examen práctica. Patrón clásico: "muestra X de la tabla A junto con Y de la tabla B".*
3. **Aggregation con HAVING para contar relaciones de "muchos a muchos".**
   *Pregunta 7 del examen práctica: "creadores con al menos 50 suscriptores". Patrón: `JOIN → GROUP BY → HAVING COUNT(...) >= N`.*
4. **CREATE TABLE con constraints — PK, FKs con CASCADE, NOT NULL.**
   *Pregunta 11 del examen práctica. Cae siempre algo de DDL.*
5. **Justificar por qué se usa una llave artificial (id) en lugar de una natural (correo, RFC).**
   *Pregunta 2 del examen práctica. Tienes que dar argumentos ingenieriles: estabilidad, performance, tamaño, evolución del esquema.*

### 🟧 PROBABILIDAD ALTA

6. **Identificar dependencias funcionales triviales vs no triviales.**
   *Pregunta 5 del examen práctica. Definición: `X → Y` es trivial sii `Y ⊆ X`.*
7. **Argumentar si una relvar sigue en una forma normal después de añadir un atributo.**
   *Pregunta 3 del examen práctica: ¿uuid en video rompe 4FN?*
8. **Acciones para mejorar performance / integridad: CHECK, índices, defaults.**
   *Pregunta 4 del examen práctica.*
9. **Window function con `PARTITION BY ... ORDER BY ...` para acumular conteos.**
   *Pregunta 9 del examen práctica. Patrón clásico: "cuántos X ha visto el usuario hasta este punto en el tiempo".*
10. **ALTER TABLE para agregar columna con default + UPDATE correlacionado.**
    *Pregunta 10 del examen práctica.*

### 🟨 PROBABILIDAD MEDIA

11. **Identificar DMVs triviales.** (`X ↠ Y` trivial sii `Y ⊆ X` ∨ `XY = E`).
12. **Diferencia entre `RANGE`, `ROWS` y `GROUPS` en frame clause.**
13. **Top-N por tiempo / por monto con LIMIT + ORDER BY.**
14. **Subconsultas correlacionadas con EXISTS / NOT EXISTS.**
15. **Anomalías (inserción, borrado, modificación) que justifican normalizar.**

### 🟩 PROBABILIDAD MENOR pero asegurada en parcial / preguntas cortas

16. **Diferencia entre orden sintáctico y orden de ejecución (FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY).**
17. **Operaciones de conjuntos: UNION, INTERSECT, EXCEPT (y sus reglas).**
18. **Diferencia entre INNER, LEFT, RIGHT, FULL, CROSS, NATURAL JOIN.**
19. **Diferencia entre `UNIQUE` y `PRIMARY KEY`.**
20. **Comportamiento de `NULL` en `UNIQUE` (NULLS NOT DISTINCT).**

### Patrones recurrentes del profesor (Jose Lechuga)

- **Le gusta** dar **encabezados de relaciones resultantes** y pedirte la query que llegue a ese resultado exacto.
- **Le gusta** combinar **una tabla pivote** (suscripcion, reproduccion, comentario) con consultas que requieren JOIN + COUNT.
- **Le gusta** pedirte **acciones sobre la BD sin código** (entender qué hace internamente el manejador).
- **Le encanta** preguntar sobre **trivialidad de DF/DMV** porque mucha gente confunde "trivial" con "fácil de probar".
- **Le encanta** preguntar sobre **CASCADE en FKs** porque mucha gente lo olvida.

---

# 📚 PARTE 1 — TEORÍA

---

## TEMA 1 — Introducción a las bases de datos

### 1.1 ¿Qué es una base de datos? ¿Y un DBMS?

**Base de datos** = colección **organizada** de información **relacionada**. Lo importante no es que sea "muchos datos" sino que está **estructurada** y **persistente**.

**DBMS (Database Management System)** = software que provee almacenamiento y acceso **eficiente, confiable, conveniente y multiusuario** a datos masivos y persistentes. Ejemplos:
- **Relacionales:** PostgreSQL, MySQL, SQL Server, Oracle, SQLite.
- **NoSQL:** MongoDB (documentos), Cassandra (columnar), Redis (clave-valor), Neo4j (grafos).
- **Cloud-managed:** Amazon RDS, Google Cloud SQL.

**Características deseables de un sistema de BD:**
- **Masivos** — manejan volúmenes enormes.
- **Persistentes** — los datos sobreviven al apagado.
- **Seguros** — control de acceso y privilegios.
- **Multiusuario** — concurrencia.
- **Consistentes** — restricciones de integridad.
- **Eficientes** — índices, planes de ejecución.
- **Confiables** — transacciones ACID, backups.
- **Escalables** — vertical / horizontal.
- **Mantenibles** — migraciones, evolución del esquema.

**Por qué importa para el examen:** cualquier pregunta del estilo "indica las ventajas de usar un DBMS sobre archivos planos" toca esta lista.

### 1.2 Arquitectura cliente / servidor

El patrón mínimo es:

```
Cliente  →  Servidor o API  →  Base de Datos
```

A escala:
```
Cliente → API → BD1 ┐
                    ├→ Data Lake (raw) → ETL/ELT → DWH (Data Warehouse)
              BD2 ┘                                  ↓
              BD3                                    Business Intelligence
                                                     Data Scientists
                                                     Data Analysts
```

- **OLTP** = base operacional (transacciones del día a día).
- **OLAP / DWH** = base analítica (consultas pesadas, agregaciones).
- **Data Lake** = almacén de datos crudos sin esquema rígido.
- **ETL / ELT** = pipelines que mueven datos del operacional al analítico.

### 1.3 Modelos de datos (los 5 grandes)

| Modelo | Estructura | Cuándo usarlo |
|---|---|---|
| **Jerárquico** | Árbol — un padre por nodo | Datos rígidamente anidados (file systems viejos, XML strict). |
| **Documental** | Documentos JSON/BSON autónomos | Datos semiestructurados, esquema flexible (MongoDB). |
| **Red** | Como jerárquico pero permite múltiples padres → many-to-many | Histórico, casi en desuso. |
| **Grafos** | Cualquier nodo se conecta con cualquier otro | Redes sociales, recomendaciones, fraude (Neo4j). |
| **Relacional** | Tablas (relaciones) con renglones (tuplas) y columnas (atributos) | Datos estructurados con relaciones claras. Es lo que usas. |

**Cita exacta de las slides:** "Los modelos de datos no solo afectan cómo se representan/estructuran los datos, sino que también modifican la manera en que pensamos sobre el problema a resolver."

**Intuición:** elegir un modelo es elegir cómo vas a *pensar* el problema. Si eliges relacional, vas a pensar en relaciones y JOINs. Si eliges grafos, vas a pensar en aristas y caminos. **No es solo una decisión técnica, es una decisión cognitiva.**

### 1.4 Modelo relacional — componentes

Propuesto por **Edgar F. Codd** (IBM) en **1970**. Para mediados de 1980 los RDBMS con SQL ya eran el estándar. Su principal virtud: **esconde detalles de implementación detrás de una interfase declarativa**.

Componentes:

1. **Relaciones (tablas/entidades):** nombre único en la BD.
2. **Atributos (columnas):** cada relación tiene un conjunto fijo de atributos con nombres únicos.
3. **Tipos / dominios:** cada atributo tiene un tipo (Int, String, Date…).
4. **Tuplas (renglones):** instancias concretas que pueblan la relación.
5. **Esquema:** estructura formal — nombre de relación + atributos + tipos + restricciones.
6. **Datos:** la información concreta almacenada.
7. **Valores nulos (`NULL`):** "no se sabe / no aplica" — NO es 0 ni vacío.
8. **Llave primaria (PK):** conjunto mínimo de atributos que identifica unívocamente una tupla.
9. **Llave foránea (FK):** atributo cuya validez depende de los valores en otra tabla (integridad referencial).

### 1.5 Esquema vs Datos — distinción CRUCIAL

- **Esquema** = la *estructura* (definición). Cambia raramente. Cambiarlo se llama **migración**.
- **Datos** = el *contenido* (instancias). Cambia constantemente.

Esta distinción justifica la separación entre **DDL** (define esquema) y **DML** (manipula datos).

### 1.6 DDL vs DML vs DCL

| Lenguaje | Para qué sirve | Comandos típicos |
|---|---|---|
| **DDL** | Definir y gestionar **estructura** | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** | Manipular **datos** | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| **DCL** | Controlar **privilegios y seguridad** | `GRANT`, `REVOKE` |

> 💡 Algunos autores agregan **TCL** (Transaction Control Language): `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`. No olvides que las **transacciones** son una pieza fundamental.

### 1.7 Diagramas Entidad-Relación (ERD) y cardinalidad

Un **ERD** representa visualmente:
- Las **entidades** (rectángulos / tablas).
- Las **relaciones** entre ellas (líneas con símbolos crow's foot).
- La **cardinalidad** (cuántas tuplas de A se relacionan con cuántas de B).
- La **opcionalidad / obligatoriedad** (si la relación es opcional o requerida).

**Notación Crow's foot (la que usa el profe):**

| Símbolo en el extremo | Significado |
|---|---|
| `\|\|` (dos rayas verticales) | **Exactamente uno** (uno y obligatorio) |
| `o\|` (círculo + raya) | **Cero o uno** (opcional, máximo uno) |
| `\|<` o `}\|` (raya + pata de cuervo) | **Uno o muchos** (al menos uno, obligatorio) |
| `o<` o `}o` (círculo + pata de cuervo) | **Cero o muchos** (opcional, sin tope) |

**Cardinalidad** = el *máximo* (uno o muchos).
**Opcionalidad** = el *mínimo* (cero o al menos uno).

**Ejemplo del ERD de fotomultas:**
La línea entre `propietario` y `vehiculo` es `||---o<` interpretada del lado de `propietario` hacia `vehiculo`: "**Un propietario tiene cero o muchos vehículos**", y del lado contrario: "**Un vehículo tiene exactamente un propietario**".

> ⚠️ **Trampa típica:** confundir cardinalidad con opcionalidad. La pregunta de "¿es obligatoria?" siempre se refiere al **mínimo**, no al máximo.

### 1.8 Tipos comunes de relaciones

1. **Uno a uno (1:1):** un alumno tiene una credencial. Raro porque suele fusionarse en una sola tabla.
2. **Uno a muchos (1:N):** un propietario tiene muchos vehículos. **La más común**; se resuelve poniendo la FK en el lado N.
3. **Muchos a muchos (N:M):** un alumno toma muchas clases y una clase tiene muchos alumnos. **Se resuelve con una tabla pivote** (alumno_clase).

> 🔑 **Regla mental:** *cuando ves N:M, siempre debe existir una tabla pivote*. Si no la ves en un ERD, está mal diseñado.

### 1.9 Errores comunes en el modelo relacional

- Confundir `NULL` con `0`, `''`, `FALSE`. `NULL` es **ausencia de información**, no un valor.
- Asumir que las tuplas tienen orden (no lo tienen).
- Asumir que las columnas tienen orden (formalmente no).
- Asumir que puede haber tuplas duplicadas en una relación pura (no las hay; las que ves en SQL son porque SQL relaja esta regla con `bag semantics`).

---

## TEMA 2 — Consultas SQL

### 2.1 Propiedades del lenguaje SQL

| Propiedad | Significado |
|---|---|
| **Declarativo** | Dices *qué* quieres, no *cómo* obtenerlo. El optimizador del DBMS resuelve el cómo. |
| **Cerradura** | El resultado de toda consulta es una tabla (relación). Por eso puedes anidar queries. |
| **Especializado** | Gramática reducida (CRUD: Create, Read, Update, Delete). |
| **Relacional** | Implementa el álgebra relacional sobre el modelo de Codd. |

**Intuición de "cerradura":** como toda consulta produce una tabla, puedes usar el resultado como input de otra consulta → eso es exactamente lo que pasa con **subconsultas** y **CTEs**.

### 2.2 Mecánica interna de una consulta (los 6 pasos)

Cuando lanzas un `SELECT`, el servidor:

1. Genera o reutiliza una **conexión** con el cliente.
2. Valida que el usuario tenga **permiso para ejecutar** la sentencia.
3. Valida que el usuario tenga **permiso para acceder** a los datos.
4. Valida la **sintaxis**.
5. El **optimizador** genera un **plan de ejecución** (basado en estadísticas, índices, costos).
6. El servidor **ejecuta** el plan y envía resultados.

> 💡 Este es el detalle que el profe puede pedir en una pregunta del estilo "explica los pasos de ejecución de un SELECT".

### 2.3 Cláusulas de consulta — Orden sintáctico vs orden de ejecución

**ESTO CAE — entiéndelo bien:**

| Orden Sintáctico (cómo lo escribes) | Orden de Ejecución (cómo se procesa) |
|---|---|
| 1. `SELECT` | 1. `FROM` |
| 2. `FROM` | 2. `WHERE` |
| 3. `WHERE` | 3. `GROUP BY` |
| 4. `GROUP BY` | 4. `HAVING` |
| 5. `HAVING` | 5. `SELECT` |
| 6. `ORDER BY` | 6. `ORDER BY` |

**Por qué importa:**
- Como `SELECT` se ejecuta DESPUÉS de `WHERE`, no puedes usar un alias del SELECT en el WHERE.
- Como `GROUP BY` va antes que `SELECT`, en SELECT solo puedes poner columnas agrupadas o funciones de agregación.
- Como `HAVING` va después del agrupamiento, ahí sí puedes filtrar por `COUNT(*) > 50`.

**Patrón mental:** "¿qué filas voy a tomar?" (FROM, JOIN) → "¿cuáles me quedo?" (WHERE) → "¿cómo las junto?" (GROUP BY) → "¿qué grupos descarto?" (HAVING) → "¿qué columnas regreso?" (SELECT) → "¿cómo las ordeno?" (ORDER BY).

### 2.4 Cláusulas principales (descripción detallada)

- **`SELECT`** — Proyección: define las columnas (y expresiones derivadas) en el resultado.
  - `SELECT DISTINCT` elimina duplicados.
  - `SELECT *` regresa todo.
- **`FROM`** — Identifica las relaciones de origen. Aquí van los JOINs.
- **`WHERE`** — Filtra **tuplas individuales** antes de agrupar.
- **`GROUP BY`** — Agrupa tuplas que comparten valores comunes en las columnas indicadas.
- **`HAVING`** — Filtra **grupos** ya creados (no tuplas).
- **`ORDER BY`** — Ordena el resultado final. `ASC` (default) / `DESC`.

> 🔑 **Regla de oro WHERE vs HAVING:**
> - `WHERE` opera sobre **renglones individuales**, ANTES de agrupar.
> - `HAVING` opera sobre **grupos**, DESPUÉS de agrupar.
> Si tu filtro NO involucra una función agregada, casi siempre va en `WHERE` (es más eficiente).

### 2.5 Joins — la pieza más importante del temario

#### Producto cartesiano

```sql
SELECT * FROM tabla_1, tabla_2;
-- equivalente a:
SELECT * FROM tabla_1 CROSS JOIN tabla_2;
```

Genera **todas las combinaciones posibles** entre filas de A y B. Si A tiene m filas y B tiene n, el resultado tiene **m × n**. Casi siempre lo quieres EVITAR (a menos que generes combinaciones a propósito).

> ⚠️ **Trampa común:** olvidar la condición `ON` en un JOIN → en algunos dialectos eso se convierte en un producto cartesiano disfrazado y revientas la BD.

#### INNER JOIN

```sql
SELECT * FROM tabla_1
INNER JOIN tabla_2 ON tabla_1.x = tabla_2.y;
-- alias:
SELECT * FROM tabla_1 JOIN tabla_2 ON tabla_1.x = tabla_2.y;
```

Solo regresa filas donde **AMBAS tablas** tienen match. Si en la tabla izquierda hay un valor sin pareja en la derecha (o viceversa), **se descarta**.

#### LEFT (OUTER) JOIN

```sql
SELECT * FROM tabla_1
LEFT JOIN tabla_2 ON tabla_1.x = tabla_2.y;
```

Conserva **todas las filas de la izquierda**; las que no tengan match en la derecha aparecen con `NULL` en las columnas de la derecha.

**Uso típico:** "muéstrame todos los usuarios y, si tienen comentarios, los comentarios; si no, los usuarios igual aparecen".

#### RIGHT (OUTER) JOIN

Espejo del LEFT JOIN. **En la práctica, casi nadie lo usa** porque puedes invertir las tablas y usar LEFT.

#### FULL (OUTER) JOIN

```sql
SELECT * FROM tabla_1
FULL OUTER JOIN tabla_2 ON tabla_1.x = tabla_2.y;
```

Combina LEFT + RIGHT: conserva **todas las filas de ambos lados**, llenando con NULL donde no haya match.

#### NATURAL JOIN

```sql
SELECT * FROM tabla_1 NATURAL JOIN tabla_2;
```

Auto-detecta columnas con **el mismo nombre** entre las dos tablas y las usa como condición de JOIN. **Peligroso porque depende del nombrado**: si cambias el nombre de una columna, el join se rompe silenciosamente.

> 🚫 **Buena práctica:** prefiere `INNER JOIN ... ON ...` explícito. Es más seguro y más legible.

#### Tabla comparativa de JOINs

| JOIN | Conserva izq | Conserva der | Rellena NULL? |
|---|---|---|---|
| `CROSS` | sí (todo×todo) | sí (todo×todo) | no |
| `INNER` | solo con match | solo con match | no |
| `LEFT` | sí | solo con match | sí (derecha) |
| `RIGHT` | solo con match | sí | sí (izquierda) |
| `FULL` | sí | sí | sí (ambos lados) |

### 2.6 Funciones de agrupación (aggregations)

| Función | Qué hace | Ignora NULL? |
|---|---|---|
| `COUNT(*)` | Cuenta TODOS los renglones (incluso con NULL) | NO |
| `COUNT(col)` | Cuenta valores **no nulos** de col | SÍ |
| `COUNT(DISTINCT col)` | Cuenta valores **distintos y no nulos** | SÍ |
| `SUM(col)` | Suma valores | SÍ |
| `AVG(col)` | Promedio aritmético | SÍ |
| `MAX(col)` | Valor máximo | SÍ |
| `MIN(col)` | Valor mínimo | SÍ |

> ⚠️ **Trampa MUY común:** `AVG(col)` excluye los NULL del divisor. Si quieres tratar NULL como 0, usa `AVG(COALESCE(col, 0))`.

> ⚠️ **Trampa MUY común con COUNT:** `COUNT(*)` cuenta filas incluyendo aquellas con NULL en *todas* las columnas; `COUNT(columna)` cuenta filas donde *esa* columna no es NULL. Si la columna tiene 100 filas y 30 son NULL, `COUNT(col)` regresa 70, `COUNT(*)` regresa 100.

### 2.7 Visualización mental de GROUP BY

Imagina la tabla. Identifica las columnas del `GROUP BY`. **Junta mentalmente todas las filas que comparten esos valores en una "caja"**. Cada caja se convierte en una fila del resultado. Las funciones agregadas se aplican dentro de cada caja.

```sql
SELECT clase_id, MAX(calificacion_final)
FROM alumno_clase
GROUP BY clase_id;
```

Resultado: una fila por cada `clase_id` distinto, con el máximo de las calificaciones de esa clase.

> 🔑 **Regla:** en `SELECT`, después de un `GROUP BY`, solo puedes proyectar:
> 1. Columnas que estén en el `GROUP BY`.
> 2. Funciones de agregación.
> 3. Constantes / expresiones derivadas de lo anterior.

### 2.8 HAVING — filtrado de grupos

```sql
SELECT clase_id, MAX(calificacion_final)
FROM alumno_clase
GROUP BY clase_id
HAVING MAX(calificacion_final) < 6;
```

**Filtra grupos completos** que no cumplan la condición.

**HAVING vs WHERE:**
- WHERE: "esta fila individual cumple la condición" → se ejecuta antes del GROUP BY.
- HAVING: "este grupo cumple la condición" → se ejecuta después del GROUP BY.

Por ejemplo, "creadores con al menos 50 suscriptores": el filtro `COUNT(suscriptor_id) >= 50` debe ir en HAVING porque hay que agrupar primero por creador.

### 2.9 Operaciones de conjuntos (UNION, INTERSECT, EXCEPT)

Operan a nivel **tupla** entre dos consultas:

| Versión | Mantiene duplicados? |
|---|---|
| `UNION` | NO (elimina duplicados) |
| `UNION ALL` | SÍ |
| `INTERSECT` | NO |
| `INTERSECT ALL` | SÍ |
| `EXCEPT` | NO |
| `EXCEPT ALL` | SÍ |

**Reglas obligatorias** para usarlos:

1. Ambos conjuntos deben tener el **mismo número de columnas**.
2. Los tipos deben coincidir (o ser convertibles trivialmente).
3. Los nombres NO necesitan coincidir.
4. El `ORDER BY` se aplica al final (en la última consulta) y usa los nombres de la **primera consulta**.
5. **Precedencia:** `INTERSECT` > `UNION` ≈ `EXCEPT` (izquierda a derecha).
6. Puedes usar paréntesis para imponer orden.

### 2.10 Subconsultas (subqueries)

Definición: **una consulta dentro de otra**. Suele ejecutarse antes (no siempre) y existe solo durante la ejecución.

**3 tipos de resultados** (define cómo se puede usar):

| Tipo de resultado | Operadores válidos |
|---|---|
| **Escalar** (1 valor) | `=`, `<>`, `<`, `<=`, `>`, `>=`, `BETWEEN` |
| **Columnar** (N filas, 1 col) | `IN`, `NOT IN`, `ANY`, `ALL`, `EXISTS` |
| **Tabular** (N filas, M cols) | `IN`, `NOT IN`, en `JOIN`, en `FROM` |

**2 categorías por correlación:**

#### A) No correlacionadas

- Se ejecutan **una sola vez**, independientes de la consulta exterior.
- Eficientes.
- Se pueden ejecutar sueltas sin error.

```sql
SELECT * FROM video
WHERE creador_id IN (SELECT id FROM usuario WHERE pais = 'MX');
```

**CTE (Common Table Expression)** — caso especial nombrado:

```sql
WITH suscriptores_por_creador AS (
    SELECT creador_id, COUNT(*) AS n
    FROM suscripcion
    GROUP BY creador_id
)
SELECT * FROM suscriptores_por_creador WHERE n >= 50;
```

Ventajas de CTEs: legibilidad, reutilización, una CTE puede usar otra previa.

#### B) Correlacionadas

- Hacen referencia a columnas de la consulta exterior.
- Se ejecutan **una vez por cada fila** de la exterior.
- Útiles en EXISTS/NOT EXISTS y modificaciones.

```sql
SELECT u.nombre, u.apellido
FROM usuario u
WHERE EXISTS (
    SELECT 1 FROM prestamo p
    WHERE p.usuario_id = u.id   -- ← referencia a la externa
);
```

**`EXISTS` / `NOT EXISTS`:**
- Solo evalúa si la subconsulta regresa **al menos una fila** o ninguna.
- No le importa qué regrese, por eso `SELECT 1`, `SELECT *`, `SELECT col` son equivalentes.
- Más eficiente que `IN` cuando hay muchas filas.

### 2.11 Funciones de ventana (window functions)

**Diferencia clave con GROUP BY:**
- `GROUP BY` colapsa filas → reduce la cardinalidad del resultado.
- Window function **NO colapsa filas** → agrega una columna calculada sobre una "ventana" de filas pero conserva la cardinalidad original.

**Sintaxis general:**

```sql
SELECT col1, col2,
       funcion(...) OVER (
           PARTITION BY col_part
           ORDER BY col_orden
           frame_clause
       ) AS nombre
FROM tabla;
```

O con cláusula `WINDOW`:

```sql
SELECT *,
       AVG(calificacion) OVER w
FROM tabla
WINDOW w AS (PARTITION BY clase_id ORDER BY semestre);
```

**Componentes:**
- `PARTITION BY` → divide las filas en grupos (como un GROUP BY) pero no colapsa.
- `ORDER BY` → ordena dentro de cada partición (para acumulados, ranks, etc.).
- `frame_clause` → define qué subconjunto de filas cuenta para el cálculo.

#### Frame clause — 3 tipos críticos

| Tipo | Cómo se define el frame |
|---|---|
| `RANGE` | Por **valores de la columna ORDER BY**. Si dices `RANGE BETWEEN 1 PRECEDING AND 1 FOLLOWING`, el frame incluye todas las filas cuyo valor en la columna ORDER BY esté en `[actual - 1, actual + 1]`. |
| `ROWS` | Por **número físico de filas**. `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING` = la fila actual, la anterior física y la siguiente física. Si hay empates, el resultado NO es determinístico. |
| `GROUPS` | Por **grupos lógicos** generados según el ORDER BY. `GROUPS BETWEEN 1 PRECEDING AND 1 FOLLOWING` = grupo actual + grupo anterior + grupo siguiente, donde "grupo" = filas con el mismo valor en ORDER BY. |

Tabla de opciones de extremos:

| Extremo inferior | Extremo superior |
|---|---|
| `UNBOUNDED PRECEDING` | `CURRENT ROW` |
| `offset PRECEDING` | `offset FOLLOWING` |
| `CURRENT ROW` | `UNBOUNDED FOLLOWING` |

> 💡 **Combinación más común para acumulados:** `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` — "todas las filas desde el inicio de la partición hasta la actual". Útil para "cantidad acumulada hasta este punto".

> ⚠️ **Diferencia sutil RANGE vs ROWS vs GROUPS:**
> Si tienes valores repetidos en la columna ORDER BY (varios alumnos con semestre = 4):
> - `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: cada fila ve diferente acumulado (depende del orden físico). NO DETERMINÍSTICO si hay empates.
> - `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: todas las filas con el mismo semestre ven el MISMO acumulado (incluyen TODAS las filas hasta su valor).
> - `GROUPS BETWEEN 1 PRECEDING AND 1 FOLLOWING`: agrupa filas por igualdad en ORDER BY y mueve grupos enteros.

#### Funciones específicas de ventana (no agregadas)

| Función | Descripción |
|---|---|
| `ROW_NUMBER()` | Número consecutivo (1, 2, 3, ...) dentro de la partición. |
| `RANK()` | Ranking con huecos por empate (1, 2, 2, 4). |
| `DENSE_RANK()` | Ranking SIN huecos por empate (1, 2, 2, 3). |
| `FIRST_VALUE(col)` | Primer valor de col en la partición/frame. |
| `LAST_VALUE(col)` | Último valor de col en la partición/frame. |
| `LAG(col, n)` | Valor de col n filas ANTES en la partición. |
| `LEAD(col, n)` | Valor de col n filas DESPUÉS en la partición. |
| `NTILE(n)` | Asigna a cada fila un número entre 1 y n distribuyendo por cuantiles. |
| `CUME_DIST()` | Fracción acumulativa de filas ≤ la actual. |

**Patrón clásico — "cuántos X ha hecho el usuario hasta este punto en el tiempo":**

```sql
SELECT *,
       COUNT(*) OVER (
           PARTITION BY usuario_id, EXTRACT(MONTH FROM fecha)
           ORDER BY fecha
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS conteo_acumulado_mes
FROM reproduccion;
```

**Esto cae en el examen como Pregunta 9.**

---

## TEMA 3 — Definición y modificación de datos en SQL

### 3.1 Tipos de datos en PostgreSQL (los que usa el profe)

| Categoría | Tipos |
|---|---|
| **Numéricos** | `smallint`, `int`, `bigint`, `decimal`, `numeric(p,s)`, `real`, `double precision`, `smallserial`, `serial`, `bigserial` |
| **Caracteres** | `varchar(n)`, `char(n)`, `bpchar`, `text` |
| **Tiempo** | `timestamp`, `date`, `time`, `interval` |
| **Booleanos** | `boolean` |
| **Otros** | `enum`, `geometric`, `JSON`, arrays, etc. |

**`SERIAL` vs `BIGSERIAL`:** ambos son tipos especiales que crean automáticamente una **secuencia** y le dan al atributo un default `NEXTVAL`. `BIGSERIAL` usa `bigint` (recomendado para PKs por escalabilidad).

> ⚠️ **`numeric(p, s)`** = `p` dígitos totales, `s` decimales. `numeric(10,2)` permite 10 dígitos totales, 2 después del punto → rango `-99999999.99` a `99999999.99`.

### 3.2 Sintaxis CREATE TABLE

**Forma básica:**

```sql
CREATE TABLE nombre_tabla (
    columna_1 tipo_dato,
    columna_2 tipo_dato,
    ...
);
```

**Forma idempotente** (no falla si ya existe):

```sql
CREATE TABLE IF NOT EXISTS nombre_tabla ( ... );
```

**Con defaults:**

```sql
CREATE TABLE usuario (
    id BIGSERIAL,
    nombre VARCHAR(100),
    activo BOOLEAN DEFAULT TRUE,
    fecha_registro TIMESTAMP DEFAULT NOW()
);
```

### 3.3 Restricciones (constraints) — LA SECCIÓN MÁS IMPORTANTE

| Constraint | Para qué |
|---|---|
| `NOT NULL` | La columna no puede ser nula. |
| `CHECK (expr)` | La columna debe cumplir un predicado booleano. |
| `UNIQUE` | El valor (o combinación de valores) debe ser único en la tabla. |
| `PRIMARY KEY` | Identificador único de tupla. Es `UNIQUE + NOT NULL + ÍNDICE`. |
| `FOREIGN KEY` | El valor debe existir en otra tabla (integridad referencial). |

#### Diferencia entre `PRIMARY KEY` y `UNIQUE NOT NULL`

Ambos garantizan unicidad y no-nulidad. Pero `PRIMARY KEY`:
1. **Solo puede haber UNA por tabla** (aunque puede ser compuesta).
2. **Automáticamente** genera un **índice único basado en B-tree**.
3. Es el "punto de entrada canónico" para JOINs y FKs.

`UNIQUE NOT NULL` puede haber múltiples en una tabla.

#### Tratamiento de NULL en UNIQUE

**Por default**, dos valores `NULL` se consideran **diferentes** entre sí. Por lo tanto, puedes tener varias filas con `NULL` en una columna `UNIQUE`.

Si quieres lo contrario:

```sql
CREATE TABLE products (
    product_no INTEGER UNIQUE NULLS NOT DISTINCT,
    ...
);
```

> 🔥 **Pregunta tramposa típica:** "¿Por qué la BD me deja insertar dos filas con NULL en una columna UNIQUE?" → porque, por default, NULL ≠ NULL.

#### CHECK — restricciones genéricas

```sql
-- Inline:
CREATE TABLE products (
    price NUMERIC CHECK (price > 0)
);

-- Con nombre:
CREATE TABLE products (
    price NUMERIC CONSTRAINT positive_price CHECK (price > 0)
);

-- A nivel de tabla (combina columnas):
CREATE TABLE products (
    price NUMERIC,
    discounted_price NUMERIC,
    CHECK (price > discounted_price)
);
```

> 💡 **Buena práctica:** dale nombre a tus constraints con `CONSTRAINT nombre CHECK(...)`. Si fallan, el mensaje de error es leíble; si no, el DBMS te tira un nombre auto-generado feo.

#### PRIMARY KEY compuesta

```sql
CREATE TABLE alumno_clase (
    alumno_id INT,
    clase_id INT,
    calificacion NUMERIC(3,1),
    PRIMARY KEY (alumno_id, clase_id)
);
```

**Patrón clásico para tablas pivote** de relaciones N:M.

#### FOREIGN KEY — sintaxis completa (BN)

```sql
[ CONSTRAINT fk_name ]
FOREIGN KEY (fk_columns)
REFERENCES parent_table (parent_key_columns)
[ ON DELETE { NO ACTION | SET NULL | SET DEFAULT | RESTRICT | CASCADE } ]
[ ON UPDATE { NO ACTION | SET NULL | SET DEFAULT | RESTRICT | CASCADE } ]
```

**Acciones referenciales** (lo que hace la FK cuando borras / modificas el padre):

| Acción | Comportamiento |
|---|---|
| `NO ACTION` | Default. Verifica al final de la transacción. Si hay referencias, falla. |
| `RESTRICT` | Igual a NO ACTION pero no permite diferir; falla inmediato. |
| `CASCADE` | Propaga el borrado/update a las filas dependientes. ⚠️ Cuidado, borra TODO. |
| `SET NULL` | Pone NULL en la FK al borrar/actualizar el padre. Requiere que la FK acepte NULL. |
| `SET DEFAULT` | Pone el valor DEFAULT en la FK. |

> 🔥 **Pregunta del examen Q11:** "Las llaves foráneas deben hacer CASCADE en caso de borrado." → usas `ON DELETE CASCADE`.

#### Forma corta para FKs simples

```sql
CREATE TABLE orders (
    product_no INTEGER REFERENCES products (product_no)
);
```

#### FK compuesta

```sql
FOREIGN KEY (b, c) REFERENCES other_table (c1, c2)
```

### 3.4 ALTER TABLE — modificaciones sin perder datos

En sistemas productivos NUNCA se hace `DROP + CREATE`. Se usa `ALTER`.

#### Agregar columnas

```sql
ALTER TABLE products ADD COLUMN description TEXT;
ALTER TABLE products ADD COLUMN description TEXT DEFAULT '1 pieza';
ALTER TABLE products ADD COLUMN description TEXT CHECK (description > '');
```

> 💡 Si agregas una columna `NOT NULL` sin default, **fallará** en tablas con datos. Estrategia: primero agregas con default, luego cambias a NOT NULL.

#### Quitar columnas

```sql
ALTER TABLE products DROP COLUMN description;
ALTER TABLE products DROP COLUMN description CASCADE;
```

`CASCADE` aquí elimina también los objetos dependientes (vistas, FKs, etc.).

#### Agregar restricciones

```sql
ALTER TABLE products ADD CHECK (name > '');
ALTER TABLE products ALTER COLUMN product_no SET NOT NULL;
ALTER TABLE products ADD CONSTRAINT some_name UNIQUE (product_no);
ALTER TABLE products ADD FOREIGN KEY (product_group_id) REFERENCES product_groups (id);
```

> ⚠️ **Trampa:** las restricciones se verifican **inmediatamente** contra los datos existentes. Si un dato existente las viola, falla el ALTER. **Estrategia:** corrige primero los datos, luego agrega la restricción.

#### Quitar restricciones

```sql
ALTER TABLE products DROP CONSTRAINT some_name;
ALTER TABLE products ALTER COLUMN product_no DROP NOT NULL;
```

#### Modificar valor por default

```sql
ALTER TABLE products ALTER COLUMN price SET DEFAULT 7.77;
ALTER TABLE products ALTER COLUMN price DROP DEFAULT;
```

#### Cambiar tipo de dato

```sql
ALTER TABLE products ALTER COLUMN price TYPE NUMERIC(10,2);
```

> ⚠️ **Solo funciona** si los valores existentes se pueden convertir implícitamente. **Buena práctica:** quitar defaults y constraints, cambiar tipo, volver a agregar.

#### Renombrar columnas y tablas

```sql
ALTER TABLE products RENAME COLUMN product_no TO product_number;
ALTER TABLE products RENAME TO items;
```

### 3.5 Esquemas (schemas)

Una BD contiene **esquemas**, los esquemas contienen **tablas**.

```
Base de datos
└── Esquema
    └── Tablas
```

**Por qué existen los esquemas:**
1. Organizan objetos en grupos lógicos.
2. Permiten controlar acceso por esquema (no tabla por tabla).
3. Evitan colisión de nombres ("ventas.cliente" no choca con "rh.cliente").

```sql
CREATE SCHEMA myschema;
DROP SCHEMA myschema;
DROP SCHEMA myschema CASCADE;  -- elimina también las tablas adentro
```

Para acceder a una tabla en un esquema: `myschema.mytable`.

### 3.6 INSERT — Inserción de datos

**A partir de valores literales:**

```sql
INSERT INTO myschema.mytable (x, y, z) VALUES
('x1', 'y1', 1),
('x2', 'y2', 2);
```

**A partir de una consulta** (importantísimo para migraciones):

```sql
INSERT INTO destino (col1, col2)
SELECT a, b FROM origen WHERE condicion;
```

> 💡 Si no especificas las columnas, debes dar los valores en el orden EXACTO en que están definidas en la tabla. **Buena práctica:** siempre especifica las columnas.

### 3.7 DELETE — eliminación de datos

```sql
DELETE FROM products WHERE price = 10;
DELETE FROM products;  -- ⚠️ borra TODO sin WHERE
```

> 🚨 **El comando más peligroso del SQL:** `DELETE FROM tabla;` sin WHERE borra TODO. Siempre verifica con `SELECT * FROM tabla WHERE ...` primero.

### 3.8 UPDATE — modificación de datos

```sql
UPDATE products
SET price = 10
WHERE price = 5;

-- Actualizar usando expresiones:
UPDATE products
SET price = price * 1.10;

-- Múltiples columnas:
UPDATE products
SET price = 10, discount = 0.05
WHERE id = 1;
```

#### UPDATE con subconsulta correlacionada (patrón del examen Q10)

```sql
UPDATE usuario u
SET es_creador = TRUE
WHERE EXISTS (
    SELECT 1 FROM video v WHERE v.creador_id = u.id
)
OR EXISTS (
    SELECT 1 FROM suscripcion s WHERE s.creador_id = u.id
);
```

O usando `IN`:

```sql
UPDATE usuario
SET es_creador = TRUE
WHERE id IN (SELECT creador_id FROM video)
   OR id IN (SELECT creador_id FROM suscripcion);
```

### 3.9 Transacciones (BEGIN/COMMIT/ROLLBACK)

Aunque no aparece masivamente en las slides, **el examen Q10 dice "dentro de una sola transacción"**. Patrón:

```sql
BEGIN;

ALTER TABLE usuario ADD COLUMN es_creador BOOLEAN NOT NULL DEFAULT FALSE;
UPDATE usuario SET es_creador = TRUE
WHERE id IN (SELECT creador_id FROM video)
   OR id IN (SELECT creador_id FROM suscripcion);

COMMIT;
-- en caso de error: ROLLBACK;
```

**Propiedades ACID:**
- **A**tomicidad — todo o nada.
- **C**onsistencia — la BD pasa de un estado válido a otro válido.
- **I**solation — las transacciones concurrentes no interfieren.
- **D**urabilidad — al hacer COMMIT, el cambio sobrevive caídas.

---

## TEMA 4 — Normalización

### 4.1 Objetivos del diseño de bases de datos

Un buen diseño es independiente de:

1. **Hardware** — el modelo debe poder implementarse sobre cualquier infraestructura.
2. **DBMS** — el modelo no debe depender de PostgreSQL, MySQL o cualquier producto.
3. **Aplicación** — el diseño se preocupa por la **naturaleza de los datos**, no por cómo serán usados. *La teoría del diseño no tiene consideraciones de rendimiento.*

Esto significa: cuando diseñas formalmente, NO debes pensar "esto se va a consultar mucho, lo hago redundante para que sea rápido". Eso es desnormalizar y se hace **DESPUÉS** del modelo formal, solo si es necesario.

### 4.2 ¿Qué es la normalización?

**Normalización** = proceso de llevar las **relvars** de una BD a **formas (estructuras) normales o canónicas**.

**¿Por qué importan las formas normales?**

1. **Arreglan fallas lógicas** del modelo.
2. **Evitan redundancia** (un mismo dato repetido en varios lugares).
3. **Eliminan las anomalías** de inserción, borrado y modificación.

### 4.3 Las tres anomalías (memorízalas)

Considera esta tabla MAL diseñada:

```
Profesores
rfc              | nombre          | area_investigacion | edificio
PERA811016B3A    | Juan Pérez      | Computación        | C
MALO811016B3A    | Karen Martínez  | Derecho            | D
```

donde la regla es "el área determina el edificio".

| Anomalía | Qué pasa | Ejemplo |
|---|---|---|
| **Inserción** | No puedes registrar información sin tener otra. | No puedes registrar un edificio nuevo sin tener un profesor en esa área. |
| **Borrado** | Borrar una tupla elimina información que querías conservar. | Si borras al único profesor de "Derecho", desaparece el edificio "D". |
| **Modificación** | Cambiar un dato requiere muchas actualizaciones simultáneas. | Cambiar el edificio de "Computación" implica actualizar muchas tuplas; si te saltas una, queda inconsistente. |

**La solución es descomponer:**

```
Profesores: (rfc, nombre, area_investigacion)
Edificios:  (area_investigacion, edificio)
```

### 4.4 Descomposición sin pérdida

La descomposición es la herramienta básica de la normalización. **Reglas:**

1. Cada tabla resultante debe ser una **proyección** de la original.
2. **No debe perderse información** — al hacer JOIN de las tablas resultantes, debes poder reconstruir la original.

> ⚠️ **Trampa:** existen descomposiciones CON pérdida; por eso necesitamos los **teoremas de Heath y Fagin**, que garantizan cuándo una descomposición es sin pérdida.

### 4.5 Jerarquía de formas normales

```
       5FN
        ↑
       4FN
        ↑
       FNBC  (Forma Normal de Boyce-Codd)
        ↑
       3FN
        ↑
       2FN
        ↑
       1FN
```

**Siempre se puede llegar a 5FN.** Para este curso el objetivo final es **4FN**.

### 4.6 Definiciones formales preliminares

- **Tupla:** `(a₁, a₂, ..., aₙ)` — secuencia ordenada de elementos.
- **Encabezado (E):** conjunto de nombres de atributos.
- **Tupla con encabezado:** serie de pares `(A, v)` donde A es atributo del encabezado y v su valor.
- **Relación r:** par ordenado `(E, e)` donde E es el encabezado y e el conjunto de tuplas (cuerpo).
- **Variable de relación (relvar) R:** una variable con un encabezado fijo. Puedes asignarle relaciones siempre que (a) tengan el mismo encabezado y (b) cumplan las restricciones declaradas en R.

**Propiedades formales de las relaciones:**
1. **No hay orden** entre tuplas (arriba-abajo).
2. **No hay orden** entre atributos (izquierda-derecha).
3. **No hay tuplas duplicadas.**
4. Cada celda contiene **un único valor** del tipo aplicable.
5. Todos los atributos son **regulares** (nombre único, sin comportamiento especial).

> ⚠️ **SQL relaja estas reglas:** SQL permite duplicados (bag semantics), por eso existe `DISTINCT`. Cuando piensas "teóricamente", no hay duplicados; cuando piensas "SQL", sí los hay.

### 4.7 Proyecciones (πXR)

Sea `r = (E, e)` una relación y `X ⊆ E`. La **proyección de r en X**, denotada `πX r`, es la relación que conserva solo los atributos de X (eliminando duplicados).

> 💡 En SQL: `SELECT DISTINCT X FROM r` — equivalente a la proyección formal.

### 4.8 Dependencias funcionales (DF)

**Definición:** sean `X, Y ⊆ E` el encabezado de una relvar R. Existe la DF `X → Y` (léase "X determina funcionalmente a Y") si y solo si para cualquier par de tuplas `t₁, t₂` en R:

> Si `t₁` y `t₂` coinciden en X, también coinciden en Y.

Formalmente: `Π_X(t₁) = Π_X(t₂) ⇒ Π_Y(t₁) = Π_Y(t₂)`.

**Ejemplos:**
- `{CIUDAD} → {PAIS}` — Conocer la ciudad determina el país.
- `{RFC} → {NOMBRE}` — Conocer el RFC determina el nombre.

**Distinción CRUCIAL:**
- DF que se **mantiene en una RELACIÓN** (instancia particular) — puede ser accidental.
- DF que se **mantiene en una RELVAR** (definición) — es una restricción semántica para TODAS las relaciones que se le pueden asignar.

Cuando hablamos de "DFs del esquema", nos referimos a las que se mantienen en la relvar.

### 4.9 DF triviales (definición operativa)

**Teorema:** una DF `X → Y` es **trivial** ⟺ `Y ⊆ X`.

**Ejemplos:**
- `{id, fecha} → {fecha, id}` — trivial (los del lado derecho ya están del lado izquierdo).
- `{suscriptor_id, creador_id} → {creador_id}` — trivial.
- `{id, fecha_creacion, contenido} → {contenido, id}` — trivial.
- `{correo} → {nombre, apellido}` — NO trivial (nombre y apellido no están en correo).

> 🔥 **Esto cae literal en el examen Q5 inciso i, ii, iii, iv.** Memoriza la regla.

### 4.10 Irreductibilidad de una DF

`X → Y` es **irreductible** en R si y solo si:
- Se mantiene en R, **Y**
- No se mantiene en R para ningún subconjunto propio `X⁻ ⊂ X`.

Es decir: **no le puedes quitar nada al lado izquierdo y que siga determinando Y.**

### 4.11 Llaves (definiciones formales)

- **Súper llave (SK)** de R: subconjunto `SK ⊆ E` tal que `SK → E` se mantiene.
- **Llave (K)** de R: subconjunto `K ⊆ E` tal que `K → E` es **irreductible**.

En cristiano:
- **SK** = identificador único (puede tener atributos "de más").
- **K** = identificador único mínimo (no le puedes quitar nada).

**Toda llave es súper llave; no toda súper llave es llave.**

### 4.12 DFs implicadas por las llaves

**Teorema:** una DF `F` se mantiene en R y está implicada por las llaves de R ⟺ `F` es una restricción de **súper llave**.

**En cristiano:** si tomas cualquier súper llave SK y le asignas cualquier subconjunto del encabezado, eso es una DF "implicada por las llaves".

Estas DFs son las que "vienen gratis" por el diseño: no rompen ninguna forma normal, son las que **DEBE** haber.

### 4.13 Cierre de atributos (X⁺)

Dado X ⊆ E y un conjunto F de DFs, el **cierre de X bajo F**, `X⁺`, es el conjunto de todos los atributos que se pueden determinar funcionalmente desde X usando F.

**Algoritmo para calcular X⁺:**

1. Empieza con `result = X`.
2. Por cada DF `A → B` en F, si `A ⊆ result`, agrega `B` a `result`.
3. Repite hasta que `result` no cambie.

**Uso:** para saber si X es súper llave, calcula X⁺. Si X⁺ = E, entonces X es súper llave.

### 4.14 Forma Normal de Boyce-Codd (FNBC)

**Definición formal:** R está en FNBC ⟺ toda DF no trivial de R está implicada por las llaves de R.

**Equivalentemente:** R está en FNBC ⟺ para toda DF no trivial `X → Y` que se mantiene en R, X es una **súper llave** de R.

**Versión práctica (la que usas en el examen):**

> *"Las únicas DF que se mantienen en una relvar en FNBC son triviales o bien son 'flechas que salen de súper llaves'."*

**Cómo verificar:**
1. Lista todas las DFs no triviales.
2. Para cada `X → Y`, verifica si X es súper llave (calcula X⁺ y mira si X⁺ = E).
3. Si TODAS las DFs no triviales tienen lado izquierdo súper llave → FNBC. Si alguna no → NO está en FNBC.

### 4.15 Teorema de Heath — herramienta para descomponer

**Teorema:** sea E el encabezado de una relvar R y sean X, Y, Z subconjuntos disjuntos de E tales que `X ∪ Y ∪ Z = E`. Si R está sujeta a la DF `X → Y`, entonces R se puede **descomponer sin pérdida** en:

- `π(X∪Y) R` (proyección con X y Y)
- `π(X∪Z) R` (proyección con X y Z, donde Z es "el resto")

**Intuición:** si X determina Y, separa Y a una tabla aparte, dejando X como FK.

### 4.16 Axiomas de Armstrong

Reglas de inferencia para DFs (sistema **completo y consistente**):

| Regla | Inferencia |
|---|---|
| Reflexividad | `Y ⊆ X ⇒ X → Y` |
| Aumentación | `X → Y ⇒ XZ → YZ` |
| Transitividad | `X → Y ∧ Y → Z ⇒ X → Z` |

**Reglas derivadas útiles:**

| Regla | Inferencia |
|---|---|
| Autodeterminación | `X → X` |
| Unión | `X → Y ∧ X → Z ⇒ X → YZ` |
| Composición | `X → Y ∧ Z → W ⇒ XZ → YW` |
| Descomposición | `X → YZ ⇒ X → Y ∧ X → Z` |

### 4.17 Dependencias multivaluadas (DMV)

**Definición:** sea E un encabezado. Una **DMV** es una expresión `X ↠ Y` (léase "X multidetermina a Y"), donde X (determinante) y Y (dependiente) son subconjuntos de E.

**Definición en relaciones:** sea r una relación con encabezado E, sea `M: X ↠ Y` una DMV, y sea `Z = E - XY`. Entonces:

`r = πXY r ⋈ πXZ r ⇒ r satisface M`

(Si r se puede reconstruir uniendo `πXY r` y `πXZ r`, entonces M se mantiene en r.)

**Las DMVs vienen en pares:** si X, Y, Z son disjuntos y `E = XYZ`, entonces `X ↠ Y ⟺ X ↠ Z`. Por eso se escriben `X ↠ Y | Z`.

**Otra caracterización (la operacional):** para toda par de tuplas `t₁, t₂` que coincidan en X, debe existir una tupla `t₃` que combine los valores de Y de `t₁` con los valores de Z de `t₂` (y otra que combine al revés). Es decir, hay independencia entre Y y Z una vez fijada X.

### 4.18 DMVs triviales (teorema operativo)

**Teorema:** `X ↠ Y` es **trivial** ⟺ `Y ⊆ X` **O** `XY = E`.

**Ejemplos en el contexto del ERD de YouTube:**
- `{usuario_id} ↠ {dispositivo_reproduccion}` con respecto a `E_reproduccion = {id, video_id, usuario_id, fecha_reproduccion, dispositivo_reproduccion}`. 
  - ¿`Y ⊆ X`? `{dispositivo_reproduccion} ⊆ {usuario_id}`? **NO**.
  - ¿`XY = E`? `{usuario_id, dispositivo_reproduccion} = E_reproduccion`? **NO** (faltan id, video_id, fecha).
  - → **NO es trivial.**
- `{suscriptor_id} ↠ {id, creador_id}` con respecto a `E_suscripcion = {id, suscriptor_id, creador_id}`.
  - ¿`Y ⊆ X`? `{id, creador_id} ⊆ {suscriptor_id}`? **NO**.
  - ¿`XY = E`? `{suscriptor_id, id, creador_id} = E_suscripcion`? **SÍ**.
  - → **SÍ es trivial.**

### 4.19 Cuarta forma normal (4FN)

**Definición:** R está en 4FN ⟺ toda DMV no trivial de R está implicada por las llaves de R.

**Teorema operativo de DMVs implicadas por llaves:** `M: X ↠ Y` está implicada por las llaves de R ⟺ X es **súper llave** de R.

**En cristiano:** R está en 4FN si y solo si toda DMV no trivial sale de una súper llave.

**Intuición:** "4FN trata sobre la separación de información independiente." Si dentro de una tabla tienes dos "tipos" de información que no se relacionan entre sí pero ambos cuelgan de la misma llave, debes separarlas.

### 4.20 Teorema de Fagin (descomposición sin pérdida para DMV)

**Teorema:** R se puede descomponer sin pérdida en `πXY R` y `πXZ R` ⟺ la DMV `X ↠ Y | Z` se mantiene en R.

### 4.21 Axiomas de DMVs

| Regla | Inferencia |
|---|---|
| Reflexividad (DMV) | `Y ⊆ X ⇒ X ↠ Y` |
| Aumentación (DMV) | `X ↠ Y ∧ Z ⊆ W ⇒ XW ↠ YZ` |
| Replicación | `X → Y ⇒ X ↠ Y` (toda DF es DMV) |
| Transitividad (DMV) | `X ↠ Y ∧ Y ↠ Z ⇒ X → (Z - Y)` |

> 🔑 **Implicación importante:** **Toda DF es una DMV** (axioma de replicación). Por lo tanto, si una relvar está en 4FN, también está en FNBC, pero NO al revés.

### 4.22 Errores conceptuales comunes en normalización

1. **Confundir "trivial" con "obvio".** Una DF puede ser obvia (por ejemplo, "todos los alumnos tienen RFC") pero no ser trivial formalmente.
2. **Pensar que más tablas siempre es mejor.** El objetivo NO es maximizar tablas; es eliminar redundancia y anomalías.
3. **Confundir SK con K.** Llave = mínima. Súper llave = puede tener atributos de sobra.
4. **Aplicar reglas SQL al modelo formal.** Las relaciones puras no tienen orden ni duplicados, pero las tablas SQL sí.
5. **Pensar que una FK rompe FNBC.** No tiene nada que ver. FNBC habla de DFs intra-tabla, no inter-tabla.
6. **Asumir que la descomposición es siempre sin pérdida.** Necesitas Heath (para DF) o Fagin (para DMV).

### 4.23 Cómo "demostrar" 4FN en un examen (estrategia)

Cuando te dan un encabezado E y un conjunto de DFs/DMVs:

1. **Identifica todas las llaves** (calcula cierres).
2. **Listar TODAS las DFs y DMVs no triviales** (incluyendo las implicadas por Armstrong).
3. Para cada DF no trivial `X → Y`: verifica si X es súper llave.
4. Para cada DMV no trivial `X ↠ Y`: verifica si X es súper llave.
5. Si TODAS pasan → 4FN. Si alguna NO → no está en 4FN.

### 4.24 Caso del examen Q3 — "uuid en video"

Te dan `E_video = {id, creador_id, titulo, descripcion, fecha_creacion, duracion}` con DFs:
- `{id} → E_video`
- `{uuid} → {creador_id, titulo, descripcion, fecha_creacion, duracion}`
- `{uuid} → {id}`

**Análisis:**

- `id` es llave (lo dice la primera DF).
- `uuid` también es llave (porque `{uuid} → {id}` y por transitividad `{uuid} → E_video`).
- Llaves = `{id}`, `{uuid}`.
- DFs no triviales:
  - `{id} → todo` → lado izquierdo es llave (SK) → OK.
  - `{uuid} → todo` → lado izquierdo es llave (SK) → OK.

Como **toda DF no trivial tiene lado izquierdo súper llave**, la relvar está en FNBC. Y como toda DF es DMV, todas las DMVs no triviales también salen de súper llaves, por lo que está en **4FN**.

**Respuesta: SÍ continúa en 4FN.**

> 🔥 Este patrón cae siempre: te dan un cambio al esquema y te preguntan si rompe la forma normal. La estrategia mental:
> 1. Identifica las llaves DESPUÉS del cambio.
> 2. Verifica las DFs/DMVs nuevas.
> 3. Si todas salen de súper llaves → la forma normal se conserva.

---

# 🚦 ANÁLISIS PROFUNDO DEL ERD — Fotomultas CDMX

Este ERD modela el servicio de **foto multas de la Ciudad de México**. Es usado por una API REST que registra automáticamente infracciones detectadas por cámaras y por un servicio web donde ciudadanos y gobierno gestionan adeudos.

## Esquema completo de tablas

### Tabla `infraccion`
```
id              bigint            -- PK
fecha           timestamp
tipo            varchar(100)
importe         numeric(10,2)
vehiculo_id     bigint            -- FK → vehiculo.id
camara_id       bigint            -- FK → camara.id
```
**Representa:** una multa emitida a un vehículo en un momento dado, detectada por una cámara específica.

### Tabla `camara`
```
id              bigint            -- PK
tipo            varchar(100)
activa          boolean
alcaldia        varchar(100)
```
**Representa:** una cámara de vigilancia ubicada en una alcaldía, con tipo y estado.

### Tabla `vehiculo`
```
id              bigint            -- PK
placa           varchar(20)
marca           varchar(100)
anio            smallint
color           varchar(20)
propietario_id  bigint            -- FK → propietario.id
```
**Representa:** un vehículo (auto, moto, camión…) manejado por algún ciudadano. Tiene un propietario.

### Tabla `propietario`
```
id              bigint            -- PK
nombre          varchar(300)
apellido        varchar(300)
correo          varchar(254)
telefono        varchar(15)
```
**Representa:** el dueño de uno o más vehículos. NO necesariamente quien manejó al momento de la infracción.

### Tabla `pago`
```
id              bigint            -- PK
fecha           timestamp
importe         numeric(10,2)
infraccion_id   bigint            -- FK → infraccion.id
acreedor_id     bigint            -- FK → propietario.id
```
**Representa:** un pago (total o parcial) de una infracción, efectuado por algún propietario (no necesariamente el dueño del vehículo).

## Relaciones del ERD

| Relación | Cardinalidad | Interpretación |
|---|---|---|
| `propietario` ↔ `vehiculo` (vía `vehiculo.propietario_id`) | **1 : 0..N** | Un propietario tiene **0 o más vehículos**; un vehículo tiene **exactamente 1 propietario obligatorio**. |
| `vehiculo` ↔ `infraccion` (vía `infraccion.vehiculo_id`) | **1 : 0..N** | Un vehículo tiene **0 o más infracciones**; una infracción está asociada a **exactamente 1 vehículo obligatorio**. |
| `camara` ↔ `infraccion` (vía `infraccion.camara_id`) | **1 : 0..N** | Una cámara puede haber detectado **0 o más infracciones**; una infracción se detectó por **exactamente 1 cámara obligatoria**. |
| `infraccion` ↔ `pago` (vía `pago.infraccion_id`) | **1 : 0..N** | Una infracción puede tener **0 o más pagos** (pagos parciales); un pago corresponde a **exactamente 1 infracción obligatoria**. |
| `propietario` ↔ `pago` (vía `pago.acreedor_id`) | **1 : 0..N** | Un propietario puede haber efectuado **0 o más pagos**; un pago tiene **exactamente 1 acreedor obligatorio**. |

## Llaves foráneas (resumen)

| Tabla origen | Columna FK | Tabla destino | Columna destino |
|---|---|---|---|
| `vehiculo` | `propietario_id` | `propietario` | `id` |
| `infraccion` | `vehiculo_id` | `vehiculo` | `id` |
| `infraccion` | `camara_id` | `camara` | `id` |
| `pago` | `infraccion_id` | `infraccion` | `id` |
| `pago` | `acreedor_id` | `propietario` | `id` |

## Observaciones críticas del diseño

### 1. No hay tabla pivote N:M
Todas las relaciones son **1 a N**, no hay muchos-a-muchos. Por lo tanto, **no necesitas tabla pivote**.

### 2. `acreedor_id` es interesante
El propietario que **paga** una multa puede ser distinto del propietario del **vehículo**. Por ejemplo: Juan tiene un coche, Pedro le presta plata y paga la multa por él. Esto crea un caso muy típico de pregunta de examen: "¿quién paga cada multa y a qué vehículo corresponde?".

### 3. Cámaras desactivadas
La columna `activa` en `camara` permite "apagar" una cámara sin borrarla, conservando histórico de infracciones detectadas por ella. Esto es **buena práctica**: el borrado lógico (`soft delete`) en lugar de físico.

### 4. Falta auditoría
No hay `fecha_creacion` ni `fecha_actualizacion` en las entidades. En diseño productivo se suelen agregar (en este caso, `infraccion.fecha` cumple parcialmente esa función).

### 5. Posible normalización adicional
- La columna `alcaldia` en `camara` es un `varchar`. Podría normalizarse a una tabla `alcaldia` separada (para asegurar consistencia y permitir agregar atributos como población, código postal, etc.).
- `tipo` en `infraccion` y `camara` también podrían ser FKs a tablas catálogo (`tipo_infraccion`, `tipo_camara`).

## Patrones de queries que probablemente caerán sobre este ERD

### Patrón 1: Listar infracciones de un vehículo
```sql
SELECT i.fecha, i.tipo, i.importe
FROM infraccion i
WHERE i.vehiculo_id = X
ORDER BY i.fecha DESC;
```

### Patrón 2: Infracciones con datos del propietario (JOIN multinivel)
```sql
SELECT i.fecha, i.tipo, i.importe, p.nombre, p.apellido
FROM infraccion i
JOIN vehiculo v ON v.id = i.vehiculo_id
JOIN propietario p ON p.id = v.propietario_id;
```

### Patrón 3: Adeudo total por propietario
```sql
SELECT p.id, p.nombre, p.apellido,
       SUM(i.importe) - COALESCE(SUM(pa.importe), 0) AS adeudo
FROM propietario p
JOIN vehiculo v ON v.propietario_id = p.id
JOIN infraccion i ON i.vehiculo_id = v.id
LEFT JOIN pago pa ON pa.infraccion_id = i.id
GROUP BY p.id, p.nombre, p.apellido;
```

### Patrón 4: Cámaras más activas (más infracciones)
```sql
SELECT c.id, c.alcaldia, COUNT(*) AS n_infracciones
FROM camara c
JOIN infraccion i ON i.camara_id = c.id
WHERE c.activa = TRUE
GROUP BY c.id, c.alcaldia
ORDER BY n_infracciones DESC
LIMIT 10;
```

### Patrón 5: Propietarios morosos (con multas sin pagar)
```sql
SELECT DISTINCT p.id, p.nombre, p.apellido
FROM propietario p
JOIN vehiculo v ON v.propietario_id = p.id
JOIN infraccion i ON i.vehiculo_id = v.id
WHERE NOT EXISTS (
    SELECT 1 FROM pago pa WHERE pa.infraccion_id = i.id
);
```

### Patrón 6: Cuántos pagos parciales tiene cada infracción
```sql
SELECT i.id, i.tipo,
       COUNT(p.id) AS n_pagos,
       SUM(p.importe) AS total_pagado,
       i.importe - COALESCE(SUM(p.importe), 0) AS saldo_pendiente
FROM infraccion i
LEFT JOIN pago p ON p.infraccion_id = i.id
GROUP BY i.id, i.tipo, i.importe;
```

### Patrón 7: Infracciones por alcaldía
```sql
SELECT c.alcaldia, COUNT(*) AS n
FROM infraccion i
JOIN camara c ON c.id = i.camara_id
GROUP BY c.alcaldia
ORDER BY n DESC;
```

### Patrón 8: Discrepancia (alguien paga la multa de otro)
```sql
SELECT i.id AS infraccion, v.placa,
       p_dueno.nombre AS dueno_vehiculo,
       p_pagador.nombre AS pagador
FROM infraccion i
JOIN vehiculo v ON v.id = i.vehiculo_id
JOIN propietario p_dueno ON p_dueno.id = v.propietario_id
JOIN pago pa ON pa.infraccion_id = i.id
JOIN propietario p_pagador ON p_pagador.id = pa.acreedor_id
WHERE p_dueno.id <> p_pagador.id;
```

## Lugares donde suelen salir preguntas difíciles

1. **El doble rol del `propietario`**: dueño de vehículo VS pagador (acreedor) de multa. Cualquier pregunta que pida distinguir entre los dos será trampa para muchos.
2. **El `LEFT JOIN` necesario** entre `infraccion` y `pago` para no perder las infracciones sin pagos.
3. **El `COALESCE(SUM(...), 0)`** para evitar que NULL contamine las restas/sumas finales.
4. **Diferencia entre `COUNT(*)` y `COUNT(pa.id)`** en LEFT JOINs (el primero cuenta filas, incluso las que tienen NULLs; el segundo solo cuenta las no nulas).

---

## 🧷 Tablas rápidas de referencia (cheat sheet)

### Cheat sheet — SQL completo en una página

| Acción | Sintaxis típica |
|---|---|
| Crear tabla | `CREATE TABLE t (c TIPO, ...);` |
| Crear con PK compuesta | `CREATE TABLE t (..., PRIMARY KEY (c1, c2));` |
| Agregar columna | `ALTER TABLE t ADD COLUMN c TIPO;` |
| Quitar columna | `ALTER TABLE t DROP COLUMN c;` |
| Renombrar tabla | `ALTER TABLE t RENAME TO t2;` |
| Renombrar columna | `ALTER TABLE t RENAME COLUMN c TO c2;` |
| Agregar PK | `ALTER TABLE t ADD PRIMARY KEY (c);` |
| Agregar FK con cascade | `ALTER TABLE t ADD FOREIGN KEY (c) REFERENCES t2(id) ON DELETE CASCADE;` |
| Default | `ALTER TABLE t ALTER COLUMN c SET DEFAULT v;` |
| Insertar valores | `INSERT INTO t (c1, c2) VALUES (v1, v2);` |
| Insertar desde query | `INSERT INTO t (c1) SELECT c FROM t2;` |
| Actualizar | `UPDATE t SET c = v WHERE …;` |
| Borrar | `DELETE FROM t WHERE …;` |
| Top N | `SELECT … ORDER BY c DESC LIMIT N;` |
| Únicos | `SELECT DISTINCT c FROM t;` |
| Conteo por grupo | `SELECT k, COUNT(*) FROM t GROUP BY k;` |
| Filtro de grupo | `… GROUP BY k HAVING COUNT(*) > 5;` |
| Subconsulta IN | `… WHERE id IN (SELECT id FROM t2);` |
| EXISTS | `… WHERE EXISTS (SELECT 1 FROM t2 WHERE t2.id = t.id);` |
| Acumulado por mes | `SUM(c) OVER (PARTITION BY EXTRACT(MONTH FROM f) ORDER BY f ROWS UNBOUNDED PRECEDING)` |

### Cheat sheet — Lectura rápida de cardinalidad (crow's foot)

```
||  → uno y solo uno
o|  → cero o uno
}|  → uno o muchos
o<  → cero o muchos
```

### Cheat sheet — Formas normales

| Forma | Condición |
|---|---|
| **1FN** | Cada celda contiene un único valor atómico (no listas, no anidados). |
| **2FN** | 1FN + no hay dependencias parciales (DF cuyo lado izquierdo es un subconjunto propio de la PK). |
| **3FN** | 2FN + no hay dependencias transitivas no implicadas por las llaves. |
| **FNBC** | Toda DF no trivial sale de una súper llave. |
| **4FN** | FNBC + toda DMV no trivial sale de una súper llave. |
| **5FN** | 4FN + toda dependencia de unión está implicada por las llaves. |

---

# 🧪 PARTE 2 — EJERCICIOS RESUELTOS (con keywords)

> 💡 Cada ejercicio tiene **keywords masivas** para que puedas buscar con Ctrl+F todos los del mismo tipo. Por ejemplo: si quieres practicar GROUP BY con HAVING, busca `GROUP BY HAVING` y aparecerán todos. Si quieres ejercicios MUY difíciles, busca `MUY difícil`.

---

## BLOQUE A — Ejercicios conceptuales

### Ejercicio A1 — Diferencia entre BD y DBMS

**Keywords para buscar:** `conceptual`, `definición`, `DBMS`, `base de datos`, `fácil`, `Tema 1`, `introducción`

**Tipo de pregunta:** conceptual

**Dificultad:** fácil

**Patrones relacionados:**
- Características de un sistema de BD ideal.
- Ejemplos de DBMS.

**Trampas típicas:**
- Confundir BD con DBMS (la BD es la colección de datos; el DBMS es el software que la administra).

**Enunciado:**
Explica la diferencia entre "base de datos" y "DBMS". Da dos ejemplos de DBMS relacionales y dos no relacionales.

---

**Solución paso a paso:**

1. **Base de datos:** es una **colección organizada de información relacionada**. Es el "qué", el contenido y su estructura. No es ejecutable por sí misma.
2. **DBMS (Database Management System):** es un **software** que provee almacenamiento y acceso eficiente, confiable, conveniente y multiusuario a datos masivos y persistentes. Es el "cómo", la pieza que ejecuta operaciones sobre la BD.
3. La diferencia clave: **una BD vive dentro de un DBMS**. Sin DBMS, una BD es solo archivos en disco; sin BD, un DBMS es un motor vacío.

**Respuesta final:**
- BD = la colección de datos estructurados; DBMS = el software que gestiona esa colección.
- **Relacionales:** PostgreSQL, MySQL, Oracle, SQL Server, SQLite.
- **No relacionales:** MongoDB (documental), Cassandra (columnar), Redis (clave-valor), Neo4j (grafos).

---

### Ejercicio A2 — DDL vs DML vs DCL

**Keywords para buscar:** `DDL`, `DML`, `DCL`, `lenguajes SQL`, `conceptual`, `fácil`, `Tema 1`, `Tema 3`

**Tipo de pregunta:** conceptual

**Dificultad:** fácil

**Patrones relacionados:** comandos CREATE, INSERT, GRANT.

**Trampas típicas:**
- Mucha gente confunde `TRUNCATE` (DDL) con `DELETE` (DML).
- `SELECT` es DML, no DDL.

**Enunciado:**
Clasifica los siguientes comandos como DDL, DML o DCL: `CREATE TABLE`, `INSERT INTO`, `GRANT`, `ALTER TABLE`, `DELETE`, `REVOKE`, `SELECT`, `DROP TABLE`, `UPDATE`, `TRUNCATE`.

---

**Solución paso a paso:**

| Comando | Categoría | Razón |
|---|---|---|
| `CREATE TABLE` | DDL | Define estructura. |
| `INSERT INTO` | DML | Agrega datos. |
| `GRANT` | DCL | Otorga privilegios. |
| `ALTER TABLE` | DDL | Modifica estructura. |
| `DELETE` | DML | Borra datos (no la tabla). |
| `REVOKE` | DCL | Quita privilegios. |
| `SELECT` | DML | Lee datos. |
| `DROP TABLE` | DDL | Elimina la estructura completa. |
| `UPDATE` | DML | Modifica datos. |
| `TRUNCATE` | DDL | Vacía la tabla pero conserva el esquema; técnicamente es DDL porque opera sobre la estructura (resetea el rowstore). |

**Respuesta final:**
- **DDL:** CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE.
- **DML:** INSERT, DELETE, SELECT, UPDATE.
- **DCL:** GRANT, REVOKE.

---

### Ejercicio A3 — Esquema vs datos

**Keywords para buscar:** `esquema`, `datos`, `conceptual`, `fácil`, `Tema 1`, `definición`

**Tipo de pregunta:** conceptual

**Dificultad:** fácil

**Patrones relacionados:** modelado de bases de datos.

**Trampas típicas:**
- Confundir "esquema" con "schema de PostgreSQL" (que es un namespace lógico).

**Enunciado:**
Define qué es el esquema y qué son los datos. Explica por qué se separa DDL de DML basándote en esta distinción.

---

**Solución paso a paso:**

1. **Esquema:** estructura formal de la BD — nombres de relaciones, nombres y tipos de atributos, restricciones (PK, FK, CHECK, etc.).
2. **Datos:** las tuplas concretas que pueblan las relaciones en un momento dado.
3. **El esquema cambia raramente** (cuando hay migraciones); los **datos cambian constantemente** (cada transacción).
4. Por esa diferencia de frecuencia y propósito, los lenguajes se dividen:
   - **DDL** = manipula el esquema (raramente).
   - **DML** = manipula los datos (constantemente).
5. **Beneficio:** los privilegios pueden separarse (un usuario de aplicación puede tener permisos DML pero no DDL, evitando que accidentalmente borre la tabla).

**Respuesta final:**
- **Esquema** = estructura. **Datos** = contenido.
- Se separan DDL/DML porque tienen frecuencias, propósitos y necesidades de control distintos.

---

### Ejercicio A4 — ¿Por qué normalizar?

**Keywords para buscar:** `normalización`, `anomalías`, `inserción`, `borrado`, `modificación`, `redundancia`, `conceptual`, `media`, `Tema 4`

**Tipo de pregunta:** conceptual

**Dificultad:** media

**Patrones relacionados:** anomalías; FNBC; 4FN.

**Trampas típicas:**
- Decir "para que la BD sea más rápida" → es lo CONTRARIO; normalizar puede hacer más lentas algunas queries por requerir JOINs.
- Olvidar que normalizar elimina redundancia, no la minimiza.

**Enunciado:**
Explica las **3 anomalías** que justifican normalizar una base de datos y da un ejemplo de cada una usando la tabla `Profesores(rfc, nombre, area_investigacion, edificio)` donde el área determina el edificio.

---

**Solución paso a paso:**

1. **Anomalía de inserción:** *no puedes registrar un dato sin tener otro*. Si quieres dar de alta un nuevo edificio "F" para el área "Filosofía", **no puedes** hasta que haya un profesor en esa área. La tupla `(NULL, NULL, Filosofía, F)` no es válida (RFC y nombre serían NULL en una PK).
2. **Anomalía de borrado:** *borrar una tupla elimina información que querías conservar*. Si "Karen Martínez López" era la única profesora del área "Derecho" y la borras, **desaparece la información de que el área Derecho está en el edificio D**.
3. **Anomalía de modificación:** *cambiar un dato requiere muchas actualizaciones*. Si hay 50 profesores del área "Computación" y cambias el edificio de "C" a "C2", **debes actualizar 50 filas**. Si te saltas una, queda inconsistente (50 dicen "C2", 1 dice "C").

**La razón fundamental:** la tabla mezcla dos hechos independientes — "el profesor X trabaja en el área Y" y "el área Y está en el edificio Z" — en una misma relvar.

**Respuesta final:**
- Las 3 anomalías son inserción, borrado y modificación, todas causadas por la redundancia que surge de mezclar dos hechos independientes en una misma tabla.
- La solución es descomponer en `Profesores(rfc, nombre, area_id)` y `Areas(area_id, edificio)`.

---

### Ejercicio A5 — Llave artificial vs llave natural (Pregunta 2 del examen)

**Keywords para buscar:** `llave artificial`, `llave natural`, `surrogate key`, `id`, `correo`, `PK`, `primary key`, `conceptual`, `difícil`, `examen difícil`, `examen tipo final`

**Tipo de pregunta:** conceptual

**Dificultad:** difícil

**Patrones relacionados:** PK, UNIQUE, FK.

**Trampas típicas:**
- Decir solo "porque el correo cambia" — el profe quiere argumentos ingenieriles más profundos.
- Olvidar el tema de **performance de joins** (los ids son más pequeños que los strings).

**Enunciado:**
Una BD tiene la restricción `UNIQUE` sobre `usuario.correo`. ¿Es conveniente agregar un identificador artificial `usuario.id` en lugar de usar `usuario.correo` como PK? Argumenta en términos ingenieriles.

---

**Solución paso a paso:**

1. **Estabilidad del valor:**
   - El `correo` puede cambiar (el usuario edita su email).
   - Si `correo` es PK y otras tablas lo usan como FK, **un solo cambio requiere actualizar TODAS las FKs** referenciando ese correo.
   - Con `id` BIGINT inmutable, el valor nunca cambia, las FKs son estables.
2. **Tamaño y performance:**
   - `varchar(254)` (longitud máxima de correo según RFC 5321) ocupa hasta 254 bytes en cada índice.
   - `bigint` ocupa 8 bytes.
   - Los JOINs comparan PK con FK: **comparar 8 bytes es mucho más rápido que comparar hasta 254 bytes**.
   - Los índices son significativamente más pequeños → menos memoria, menos I/O.
3. **Privacidad / exposición:**
   - Si `correo` es PK, suele exponerse en URLs y APIs (`/usuarios/juan@gmail.com`), filtrando información personal.
   - Un `id` numérico no expone PII (información personal identificable).
4. **Evolución del esquema:**
   - Si en el futuro decides cambiar la regla del correo (permitir múltiples correos por usuario), con `id` la migración es trivial; con `correo` como PK es un infierno.
5. **Codd y la teoría:** una llave debe identificar unívocamente, pero el modelo NO requiere que sea "significativa". Las llaves artificiales son perfectamente válidas y suelen ser la elección de los DBMS modernos.

**Respuesta final:**
**SÍ es conveniente** agregar el id artificial. Razones principales:
1. **Estabilidad**: el id no cambia; el correo sí.
2. **Performance**: comparar bigint en JOINs es mucho más rápido que comparar varchar.
3. **Tamaño de índices**: 8 bytes vs hasta 254.
4. **Privacidad**: no exponer PII en URLs/APIs.
5. **Evolución del esquema**: cambiar la regla sobre correo no requiere migrar FKs.

Mantener `UNIQUE` en correo asegura que sigue siendo único, pero el id es el identificador "canónico" para joins y referencias.

---

### Ejercicio A6 — Por qué SQL es declarativo

**Keywords para buscar:** `SQL`, `declarativo`, `imperativo`, `optimizador`, `conceptual`, `media`, `Tema 2`

**Tipo de pregunta:** conceptual

**Dificultad:** media

**Patrones relacionados:** plan de ejecución; mecánica de consultas.

**Trampas típicas:**
- Decir que "declarativo" significa "fácil" — no, significa "describes el qué, no el cómo".

**Enunciado:**
Explica qué significa que SQL sea declarativo y qué implicaciones tiene para el programador y el DBMS.

---

**Solución paso a paso:**

1. **Declarativo** = el usuario **describe** el resultado deseado, no las instrucciones de cómo obtenerlo.
2. Esto contrasta con lenguajes **imperativos** (Python, Java) donde tú escribes los pasos: "abre el archivo, recorre las filas, filtra, ordena…".
3. En SQL escribes `SELECT * FROM t WHERE x > 10 ORDER BY y;` y el **optimizador del DBMS** decide:
   - ¿Uso un índice o escaneo completo?
   - ¿Hago hash join o nested loop join?
   - ¿En qué orden aplico los predicados?
4. **Implicaciones positivas:**
   - El programador se enfoca en la lógica de negocio, no en la implementación física.
   - El optimizador puede mejorar consultas sin cambiar el código.
   - Portabilidad entre DBMSs (en cierta medida).
5. **Implicaciones negativas:**
   - El programador pierde control sobre el plan de ejecución (a veces el optimizador toma decisiones malas).
   - Debugging del performance requiere conocer `EXPLAIN` y entender el plan.

**Respuesta final:**
- "Declarativo" = describes el qué (el resultado deseado), no el cómo (los pasos).
- El optimizador del DBMS construye el plan de ejecución.
- Ventajas: separación de capas, portabilidad, optimización automática.
- Desventajas: menor control fino sobre la ejecución.

---

### Ejercicio A7 — Cerradura del álgebra relacional

**Keywords para buscar:** `cerradura`, `closure`, `álgebra relacional`, `subconsulta`, `conceptual`, `media`, `Tema 2`

**Tipo de pregunta:** conceptual

**Dificultad:** media

**Patrones relacionados:** subconsultas; CTEs.

**Trampas típicas:**
- Confundir "cerradura" con "encerrar entre paréntesis".

**Enunciado:**
Explica qué significa la propiedad de **cerradura** en SQL y cómo se relaciona con las subconsultas.

---

**Solución paso a paso:**

1. **Cerradura** = "el resultado de toda operación es del mismo tipo que sus operandos".
2. En SQL: el resultado de una consulta es **siempre una tabla** (relación). Aunque sea de una sola fila y una sola columna, conceptualmente sigue siendo una tabla.
3. Como cada consulta produce una tabla, esa tabla puede ser **input de otra consulta** → eso permite anidar:
   - Subconsultas en `FROM`: `SELECT * FROM (SELECT … FROM t) AS sub`.
   - Subconsultas en `WHERE`: `WHERE x IN (SELECT y FROM t2)`.
   - Subconsultas en `SELECT`: `SELECT (SELECT MAX(c) FROM t2) AS m`.
4. **Sin cerradura** no se podrían anidar consultas, ni hacer CTEs, ni operaciones de conjuntos (UNION, etc.).

**Respuesta final:**
La cerradura garantiza que toda operación SQL produce una relación, lo que permite **anidar consultas indefinidamente** y combinarlas con UNION, JOIN, etc.

---

### Ejercicio A8 — Cardinalidad vs opcionalidad

**Keywords para buscar:** `cardinalidad`, `opcionalidad`, `obligatoria`, `opcional`, `crow's foot`, `conceptual`, `media`, `Tema 1`, `ERD`

**Tipo de pregunta:** conceptual / ERD

**Dificultad:** media

**Patrones relacionados:** Pregunta 1 del examen práctica.

**Trampas típicas:**
- Confundir las dos (cardinalidad = máximo; opcionalidad = mínimo).

**Enunciado:**
Define **cardinalidad** y **opcionalidad** en el contexto de un ERD. Da ejemplos usando la notación crow's foot para una relación 1:N obligatoria.

---

**Solución paso a paso:**

1. **Cardinalidad** = el **máximo número** de instancias de una entidad que se relacionan con una instancia de la otra entidad (1 o muchos).
2. **Opcionalidad** = el **mínimo número** de instancias relacionadas (0 o al menos 1).
3. Notación crow's foot, ejemplo: `Propietario ||---o<  Vehiculo`
   - Del lado del propietario: `||` → cardinalidad = 1, opcionalidad = obligatoria. Un vehículo tiene **exactamente 1 propietario obligatorio**.
   - Del lado del vehículo: `o<` → cardinalidad = muchos, opcionalidad = opcional. Un propietario tiene **0 o muchos vehículos**.

**Respuesta final:**
- Cardinalidad = máximo (1 o N).
- Opcionalidad = mínimo (0 o 1).
- Crow's foot:
  - `||` = uno y obligatorio.
  - `o|` = cero o uno (opcional, máximo uno).
  - `}|` = uno o muchos (obligatorio, sin tope).
  - `o<` = cero o muchos (opcional, sin tope).

---

### Ejercicio A9 — Orden sintáctico vs orden de ejecución

**Keywords para buscar:** `orden de ejecución`, `orden sintáctico`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `SELECT`, `ORDER BY`, `conceptual`, `media`, `Tema 2`, `examen difícil`

**Tipo de pregunta:** conceptual

**Dificultad:** media

**Patrones relacionados:** alias en SELECT; WHERE vs HAVING.

**Trampas típicas:**
- Intentar usar un alias del SELECT dentro del WHERE → no funciona porque WHERE se ejecuta antes que SELECT.

**Enunciado:**
Indica el orden sintáctico y el orden de ejecución de las cláusulas SELECT, FROM, WHERE, GROUP BY, HAVING, ORDER BY. Explica por qué no puedes usar un alias del SELECT en el WHERE.

---

**Solución paso a paso:**

**Orden sintáctico (cómo lo escribes):**
1. SELECT
2. FROM
3. WHERE
4. GROUP BY
5. HAVING
6. ORDER BY

**Orden de ejecución (cómo se procesa):**
1. FROM (con sus JOINs)
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY

**Por qué no funciona el alias:**
- Defines un alias en SELECT: `SELECT a + b AS suma FROM t WHERE suma > 10;`.
- Pero `WHERE` se ejecuta ANTES que `SELECT` → en el momento que evalúa el `WHERE`, el alias `suma` aún no existe.
- **Solución:** repetir la expresión: `WHERE a + b > 10`. O usar una subconsulta/CTE.

**Por qué SÍ se puede usar el alias en `ORDER BY`:**
- `ORDER BY` se ejecuta DESPUÉS del SELECT, por lo que el alias ya existe.

**Respuesta final:**
- Sintaxis: SELECT-FROM-WHERE-GROUP BY-HAVING-ORDER BY.
- Ejecución: FROM-WHERE-GROUP BY-HAVING-SELECT-ORDER BY.
- No se puede usar alias del SELECT en WHERE porque WHERE se ejecuta antes que SELECT.

---

### Ejercicio A10 — Diferencia entre llave y súper llave

**Keywords para buscar:** `súper llave`, `llave`, `key`, `superkey`, `irreductible`, `conceptual`, `difícil`, `Tema 4`, `normalización`

**Tipo de pregunta:** conceptual / normalización

**Dificultad:** difícil

**Patrones relacionados:** PK, FNBC, dependencias funcionales.

**Trampas típicas:**
- Pensar que toda súper llave es llave.
- Olvidar que la llave es la mínima irreductible.

**Enunciado:**
Define **súper llave** y **llave** en términos de dependencias funcionales. Da un ejemplo donde un conjunto sea súper llave pero NO llave.

---

**Solución paso a paso:**

1. **Súper llave (SK):** subconjunto SK del encabezado E tal que la DF `SK → E` se mantiene en R. Es decir, conociendo SK puedes determinar TODAS las columnas.
2. **Llave (K):** subconjunto K tal que `K → E` es **irreductible**. Es decir, conociendo K puedes determinar todo, **PERO si quitas cualquier atributo, ya no lo logras**.

**Ejemplo:** Tabla `Usuario(id, correo, nombre, apellido)` con DFs:
- `{id} → {correo, nombre, apellido}` (id es llave)
- `{correo} → {id, nombre, apellido}` (correo también es llave)

- `{id}` es llave (irreductible — no puedes quitarle nada).
- `{id, correo}` es **súper llave pero no llave** — porque sí determina todo, pero le sobra `correo` (con solo `id` ya determinas todo).
- `{id, correo, nombre}` también es súper llave no-llave (le sobran `correo` y `nombre`).

**Toda llave es súper llave, pero no toda súper llave es llave.**

**Respuesta final:**
- **Súper llave:** identifica unívocamente, puede tener atributos de más.
- **Llave:** súper llave **mínima** (irreductible).
- Ejemplo: en `Usuario(id, correo, ...)` con `{id}` y `{correo}` como llaves: `{id, correo}` es súper llave pero NO llave porque se puede reducir.

---
## BLOQUE B — Ejercicios de ERD y cardinalidad

### Ejercicio B1 — Llaves foráneas e interpretación de cardinalidad (ERD Fotomultas)

**Keywords para buscar:** `ERD`, `fotomultas`, `llaves foráneas`, `FK`, `cardinalidad`, `uno a muchos`, `media`, `infraccion`, `vehiculo`, `camara`, `propietario`, `pago`

**Tipo de pregunta:** ERD

**Dificultad:** media

**Patrones relacionados:** Pregunta 1 del examen práctica (sobre YouTube).

**Trampas típicas:**
- Olvidar la FK de `pago.acreedor_id` (que también apunta a `propietario`).
- Confundir el lado obligatorio con el opcional.

**Enunciado:**
Para el ERD de Fotomultas, lista TODAS las llaves foráneas e indica la cardinalidad y obligatoriedad de cada relación.

---

**Solución paso a paso:**

**FKs:**
1. `vehiculo.propietario_id → propietario.id`
2. `infraccion.vehiculo_id → vehiculo.id`
3. `infraccion.camara_id → camara.id`
4. `pago.infraccion_id → infraccion.id`
5. `pago.acreedor_id → propietario.id`

**Relaciones y cardinalidad:**

1. `propietario` ↔ `vehiculo`:
   - Cardinalidad: 1:N.
   - Lado propietario: obligatorio (un vehículo siempre tiene exactamente 1 propietario).
   - Lado vehículo: opcional (un propietario puede tener 0 o muchos vehículos).
2. `vehiculo` ↔ `infraccion`:
   - 1:N. Vehículo lado obligatorio (toda infracción está asociada a 1 vehículo); infracción lado opcional (un vehículo puede tener 0 o muchas infracciones).
3. `camara` ↔ `infraccion`:
   - 1:N. Cámara lado obligatorio; infracción lado opcional.
4. `infraccion` ↔ `pago`:
   - 1:N. Infracción lado obligatorio (todo pago referencia una infracción); pago lado opcional (una infracción puede tener 0 pagos si no se ha pagado, o muchos si hay pagos parciales).
5. `propietario` ↔ `pago` (vía acreedor_id):
   - 1:N. Propietario lado obligatorio (todo pago tiene un acreedor); pago lado opcional.

**Respuesta final:**
5 FKs, todas relaciones 1:N. Ver tabla arriba para detalle de obligatoriedad.

---

### Ejercicio B2 — Reconocer una tabla pivote en un ERD

**Keywords para buscar:** `tabla pivote`, `pivot`, `muchos a muchos`, `N a M`, `N:M`, `ERD`, `media`, `Tema 1`

**Tipo de pregunta:** ERD / conceptual

**Dificultad:** media

**Patrones relacionados:** tabla `suscripcion` en YouTube, tabla `alumno_clase`.

**Trampas típicas:**
- Pensar que cualquier tabla con 2 FKs es pivote.

**Enunciado:**
¿Es la tabla `pago` del ERD de Fotomultas una tabla pivote? Justifica.

---

**Solución paso a paso:**

1. Una **tabla pivote** es la que resuelve una relación **muchos a muchos (N:M)** entre dos entidades, **sin tener atributos propios significativos** más allá de las dos FKs (o con pocos atributos sumando contexto).
2. `pago` tiene 2 FKs (`infraccion_id`, `acreedor_id`), pero también tiene atributos **propios**: `id`, `fecha`, `importe`.
3. **¿Hay relación N:M entre infraccion y propietario?** Sí, hay una conexión indirecta: una infracción puede ser pagada por muchos propietarios (poco realista pero posible legalmente) y un propietario puede pagar muchas infracciones.
4. **PERO** la entidad `pago` tiene **identidad propia** — cada pago es un evento individual con fecha, monto, etc. Por eso `pago` es una **entidad por derecho propio**, no solo una tabla pivote.

**Respuesta final:**
**Pago NO es una tabla pivote pura.** Aunque conecta infracción con propietario (acreedor), tiene atributos propios significativos (fecha, importe) que le dan identidad de entidad. Es lo que se llama una **entidad asociativa**: una tabla que resuelve una N:M y al mismo tiempo tiene datos propios.

---

### Ejercicio B3 — ¿Por qué la FK lleva el "_id"?

**Keywords para buscar:** `convención`, `_id`, `naming`, `FK`, `conceptual`, `fácil`, `media`

**Tipo de pregunta:** conceptual / ERD

**Dificultad:** fácil-media

**Patrones relacionados:** convenciones de naming en bases de datos.

**Trampas típicas:** confundir con la PK.

**Enunciado:**
En el ERD de Fotomultas, `vehiculo.propietario_id` referencia a `propietario.id`. ¿Por qué se llama `propietario_id` y no simplemente `propietario`? ¿Qué problemas evita esta convención?

---

**Solución paso a paso:**

1. La columna `vehiculo.propietario_id` almacena el **id** del propietario, NO al propietario entero. Es solo un puntero (FK).
2. La convención `<entidad>_id` deja explícito que es una FK y no un atributo conceptual de la entidad.
3. Si se llamara `propietario` (sin `_id`), confundiría:
   - ¿Es el nombre del propietario?
   - ¿Es el objeto entero?
   - ¿Es un id numérico?
4. Esta convención también ayuda al **NATURAL JOIN**: si dos tablas comparten `propietario_id`, el NATURAL JOIN funciona automáticamente.

**Respuesta final:**
- La columna almacena el `id` del propietario, no el propietario completo. La convención `_id` lo hace explícito.
- Evita ambigüedad y facilita JOINs.
- También facilita migraciones futuras (cambiar el tipo del id no requiere renombrar columnas en todos lados).

---

### Ejercicio B4 — Diferencia entre `propietario_id` y `acreedor_id`

**Keywords para buscar:** `propietario_id`, `acreedor_id`, `FK`, `múltiples FKs misma tabla`, `media`, `difícil`, `fotomultas`, `pago`, `vehiculo`

**Tipo de pregunta:** ERD / conceptual

**Dificultad:** media-difícil

**Patrones relacionados:** relaciones múltiples entre las mismas entidades.

**Trampas típicas:**
- Asumir que el dueño del vehículo es siempre quien paga la multa.
- Olvidar este caso al hacer queries.

**Enunciado:**
En el ERD de Fotomultas, ¿por qué `pago` tiene `acreedor_id` que también apunta a `propietario` cuando ya existe `vehiculo.propietario_id`? Da un caso real donde estos dos sean distintos.

---

**Solución paso a paso:**

1. `vehiculo.propietario_id` indica **quién es dueño** del vehículo (FK de vehículo a propietario).
2. `pago.acreedor_id` indica **quién pagó** la multa (FK de pago a propietario).
3. **NO son necesariamente la misma persona.**
4. Casos reales:
   - **Caso 1:** Juan le presta su auto a María. María comete una infracción. Como María es quien manejaba, ella paga la multa, no Juan (aunque el vehículo le pertenece a Juan).
   - **Caso 2:** El papá paga la multa de su hijo aunque el coche esté a nombre del hijo.
   - **Caso 3:** Una empresa con flota de autos — los autos pertenecen a la empresa, pero un empleado puede pagar de su bolsillo.
5. Para queries: cualquier consulta que combine "dueño de vehículo" con "pagador de multa" debe hacer dos JOINs separados a la tabla `propietario` con **alias distintos**, p.ej.:
   ```sql
   JOIN propietario p_dueno ON p_dueno.id = v.propietario_id
   JOIN propietario p_pagador ON p_pagador.id = pa.acreedor_id
   ```

**Respuesta final:**
- `propietario_id` = dueño del vehículo. `acreedor_id` = quien paga la multa.
- Pueden ser distintos cuando una persona paga la multa de otra (préstamo de auto, padres-hijos, empresas, etc.).
- En queries con ambos, hacer 2 JOINs con alias diferentes a `propietario`.

---

### Ejercicio B5 — Detectar errores en un ERD propuesto

**Keywords para buscar:** `ERD`, `debugging`, `errores`, `FK`, `cardinalidad`, `examen difícil`, `MUY difícil`, `Tema 1`

**Tipo de pregunta:** ERD / debugging

**Dificultad:** difícil

**Patrones relacionados:** verificación de un diseño.

**Trampas típicas:**
- No revisar si las relaciones tienen sentido semántico.

**Enunciado:**
Un alumno propone añadir al ERD de Fotomultas una tabla `multa_compartida(infraccion_id, propietario_id, porcentaje)` para que dos personas puedan dividirse una multa. ¿Está bien diseñada esta tabla? Encuentra al menos **3 problemas**.

---

**Solución paso a paso:**

**Problemas detectados:**

1. **No hay PK explícita.** Si `(infraccion_id, propietario_id)` es PK compuesta, hay que declararla. Si NO lo es, dos filas con el mismo par serían posibles → inconsistencia. **Fix:** `PRIMARY KEY (infraccion_id, propietario_id)`.
2. **No hay CHECK sobre porcentaje.** Podrías tener `porcentaje = -50` o `porcentaje = 200`. **Fix:** `CHECK (porcentaje >= 0 AND porcentaje <= 100)`.
3. **No se garantiza que los porcentajes sumen 100 por infracción.** Con el diseño actual, una infracción podría tener dos filas que sumen 80%, dejando 20% sin asignar; o sumar 130%. **Fix:** difícil de hacer con CHECK simple — requiere un trigger o constraint a nivel de tabla con subquery (compleja en PostgreSQL clásico).
4. **No hay FKs declaradas.** Si la columna `infraccion_id` apunta a `infraccion`, debe ser `FOREIGN KEY (infraccion_id) REFERENCES infraccion(id)`. Lo mismo con `propietario_id`.
5. **No define qué pasa al borrar la infracción.** ¿Se borran las multas compartidas? Si no se define `ON DELETE`, queda en `NO ACTION` → fallaría borrar la infracción si hay multa_compartida.
6. **Tipo de `porcentaje` no está especificado.** Debe ser `NUMERIC(5,2)` o similar para permitir decimales.
7. **Conflicto con `pago`.** Ya existe `pago` con `acreedor_id`. ¿Cuál es la fuente de verdad de quién debe qué? Sin reglas claras, hay inconsistencias.

**Respuesta final:**
Al menos 7 problemas: falta PK, falta CHECK en porcentaje, no se garantiza suma = 100, faltan FKs, falta ON DELETE, tipo no especificado, y posible conflicto semántico con `pago`. **Mal diseño.**

---

### Ejercicio B6 — Convertir ERD a CREATE TABLE (Fotomultas)

**Keywords para buscar:** `CREATE TABLE`, `ERD a SQL`, `FOREIGN KEY`, `PRIMARY KEY`, `fotomultas`, `media`, `DDL`

**Tipo de pregunta:** ERD a DDL

**Dificultad:** media

**Patrones relacionados:** Pregunta 11 del examen práctica.

**Trampas típicas:**
- Olvidar el `NOT NULL` en las FKs obligatorias.
- Olvidar el orden de creación (las tablas referenciadas deben crearse antes).

**Enunciado:**
Escribe los `CREATE TABLE` para las 5 tablas del ERD de Fotomultas en el orden correcto, respetando PKs, FKs, tipos y restricciones NOT NULL donde la cardinalidad es obligatoria.

---

**Solución paso a paso:**

**Orden de creación** (las que NO referencian a nadie van primero):
1. `propietario` (no referencia a nadie).
2. `camara` (no referencia a nadie).
3. `vehiculo` (referencia a propietario).
4. `infraccion` (referencia a vehiculo y camara).
5. `pago` (referencia a infraccion y propietario).

```sql
CREATE TABLE propietario (
    id BIGSERIAL PRIMARY KEY,
    nombre VARCHAR(300) NOT NULL,
    apellido VARCHAR(300) NOT NULL,
    correo VARCHAR(254),
    telefono VARCHAR(15)
);

CREATE TABLE camara (
    id BIGSERIAL PRIMARY KEY,
    tipo VARCHAR(100) NOT NULL,
    activa BOOLEAN NOT NULL DEFAULT TRUE,
    alcaldia VARCHAR(100) NOT NULL
);

CREATE TABLE vehiculo (
    id BIGSERIAL PRIMARY KEY,
    placa VARCHAR(20) NOT NULL,
    marca VARCHAR(100) NOT NULL,
    anio SMALLINT NOT NULL,
    color VARCHAR(20),
    propietario_id BIGINT NOT NULL,
    FOREIGN KEY (propietario_id) REFERENCES propietario(id)
);

CREATE TABLE infraccion (
    id BIGSERIAL PRIMARY KEY,
    fecha TIMESTAMP NOT NULL DEFAULT NOW(),
    tipo VARCHAR(100) NOT NULL,
    importe NUMERIC(10,2) NOT NULL CHECK (importe > 0),
    vehiculo_id BIGINT NOT NULL,
    camara_id BIGINT NOT NULL,
    FOREIGN KEY (vehiculo_id) REFERENCES vehiculo(id),
    FOREIGN KEY (camara_id) REFERENCES camara(id)
);

CREATE TABLE pago (
    id BIGSERIAL PRIMARY KEY,
    fecha TIMESTAMP NOT NULL DEFAULT NOW(),
    importe NUMERIC(10,2) NOT NULL CHECK (importe > 0),
    infraccion_id BIGINT NOT NULL,
    acreedor_id BIGINT NOT NULL,
    FOREIGN KEY (infraccion_id) REFERENCES infraccion(id),
    FOREIGN KEY (acreedor_id) REFERENCES propietario(id)
);
```

**Respuesta final:**
Ver código arriba. Notar: el orden importa (no puedes referenciar una tabla que aún no existe), todas las FKs son `NOT NULL` porque la cardinalidad obligatoria del ERD lo exige, y se añadieron CHECKs y defaults razonables.

---

### Ejercicio B7 — Ciclo de FKs

**Keywords para buscar:** `ciclo FK`, `referencia circular`, `ERD`, `conceptual`, `difícil`, `MUY difícil`

**Tipo de pregunta:** conceptual / ERD

**Dificultad:** difícil

**Patrones relacionados:** integridad referencial avanzada.

**Trampas típicas:**
- Pensar que un ciclo es imposible (sí es posible pero requiere FKs nulleables al inicio).

**Enunciado:**
Imagina que añades a Fotomultas la regla: "cada cámara tiene un propietario responsable" (`camara.responsable_id → propietario.id`) y "cada propietario tiene una cámara asignada como su preferida" (`propietario.camara_preferida_id → camara.id`). ¿Qué problema tiene este diseño?

---

**Solución paso a paso:**

1. Se forma un **ciclo de referencias**: camara → propietario → camara.
2. **Problema 1 — inserción inicial:** no puedes insertar una cámara sin propietario, y no puedes insertar un propietario sin cámara. Bloqueo mutuo.
3. **Solución parcial:** una de las dos FKs debe permitir NULL al menos durante la inserción inicial.
4. **Problema 2 — borrado:** no puedes borrar una cámara sin antes desligar a sus propietarios (y viceversa). Con `ON DELETE CASCADE` en ambas direcciones, podrías generar borrados en cadena infinitos.
5. **Buena práctica:** evitar ciclos. Si conceptualmente son necesarios, hacer una FK nulleable y usar transacciones para garantizar consistencia.

**Respuesta final:**
- El ciclo de FKs **bloquea la inserción inicial** porque cada lado requiere que el otro exista primero.
- Solución: al menos una FK debe permitir NULL inicialmente, o usar `DEFERRABLE INITIALLY DEFERRED` constraints (PostgreSQL avanzado), o repensar el modelo.

---
## BLOQUE C — JOINs y consultas básicas

### Ejercicio C1 — INNER JOIN simple (Fotomultas)

**Keywords para buscar:** `INNER JOIN`, `JOIN`, `SQL`, `fácil`, `fotomultas`, `infraccion`, `vehiculo`

**Tipo de pregunta:** SQL

**Dificultad:** fácil

**Patrones relacionados:** Pregunta 6 del examen práctica.

**Trampas típicas:**
- Olvidar el alias de las tablas en JOINs largos.

**Enunciado:**
Lista todas las infracciones junto con la placa del vehículo correspondiente. Columnas resultantes: `fecha`, `tipo`, `importe`, `placa`.

---

**Solución paso a paso:**

1. Necesito columnas de `infraccion` (fecha, tipo, importe) y `vehiculo` (placa).
2. La relación entre ambas es vía `infraccion.vehiculo_id = vehiculo.id`.
3. Como toda infracción TIENE un vehículo obligatorio, basta un INNER JOIN.

```sql
SELECT i.fecha, i.tipo, i.importe, v.placa
FROM infraccion i
JOIN vehiculo v ON v.id = i.vehiculo_id;
```

**Respuesta final:**
```sql
SELECT i.fecha, i.tipo, i.importe, v.placa
FROM infraccion i
JOIN vehiculo v ON v.id = i.vehiculo_id;
```

---

### Ejercicio C2 — JOIN multinivel (3 tablas)

**Keywords para buscar:** `JOIN multinivel`, `JOIN`, `múltiples JOINs`, `media`, `fotomultas`, `infraccion`, `vehiculo`, `propietario`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Patrones relacionados:** Pregunta 6 del examen.

**Trampas típicas:**
- Confundir el orden de los JOINs.
- Olvidar que el `ON` es por la FK (no por id literal).

**Enunciado:**
Lista las infracciones de la última semana, con el nombre y apellido del **dueño** del vehículo. Columnas: `fecha`, `tipo`, `importe`, `nombre`, `apellido`.

---

**Solución paso a paso:**

1. Empezar de la tabla más restrictiva (que tiene el filtro de fecha): `infraccion`.
2. Necesito el `propietario`, pero `infraccion` no tiene FK directa a `propietario` → debo pasar por `vehiculo`.
3. Cadena: `infraccion` → `vehiculo` → `propietario`.
4. Filtro de fecha: `i.fecha >= NOW() - INTERVAL '7 days'` (sintaxis PostgreSQL).

```sql
SELECT i.fecha, i.tipo, i.importe, p.nombre, p.apellido
FROM infraccion i
JOIN vehiculo v ON v.id = i.vehiculo_id
JOIN propietario p ON p.id = v.propietario_id
WHERE i.fecha >= NOW() - INTERVAL '7 days';
```

**Respuesta final:**
```sql
SELECT i.fecha, i.tipo, i.importe, p.nombre, p.apellido
FROM infraccion i
JOIN vehiculo v ON v.id = i.vehiculo_id
JOIN propietario p ON p.id = v.propietario_id
WHERE i.fecha >= NOW() - INTERVAL '7 days';
```

---

### Ejercicio C3 — LEFT JOIN para no perder filas

**Keywords para buscar:** `LEFT JOIN`, `OUTER JOIN`, `incluir sin match`, `media`, `fotomultas`, `infraccion`, `pago`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Patrones relacionados:** infracciones con o sin pagos.

**Trampas típicas:**
- Usar INNER JOIN cuando debería ser LEFT y perder las infracciones sin pagos.
- Olvidar `COALESCE` cuando se hace `SUM(pago.importe)` y hay infracciones sin pagos.

**Enunciado:**
Lista TODAS las infracciones (incluso las que no tienen pagos) con la suma total pagada. Columnas: `infraccion_id`, `importe_multa`, `total_pagado`.

---

**Solución paso a paso:**

1. `infraccion` es la "tabla maestra" — quiero TODAS sus filas.
2. `pago` es opcional — algunas infracciones no tienen pagos.
3. Por eso uso `LEFT JOIN` con infraccion del lado izquierdo.
4. `SUM(p.importe)` será NULL si no hay pagos → uso `COALESCE` para convertirlo a 0.
5. Necesito agrupar por infraccion para sumar.

```sql
SELECT i.id AS infraccion_id,
       i.importe AS importe_multa,
       COALESCE(SUM(p.importe), 0) AS total_pagado
FROM infraccion i
LEFT JOIN pago p ON p.infraccion_id = i.id
GROUP BY i.id, i.importe;
```

**Respuesta final:**
```sql
SELECT i.id AS infraccion_id,
       i.importe AS importe_multa,
       COALESCE(SUM(p.importe), 0) AS total_pagado
FROM infraccion i
LEFT JOIN pago p ON p.infraccion_id = i.id
GROUP BY i.id, i.importe;
```

---

### Ejercicio C4 — Two-alias JOIN a la misma tabla

**Keywords para buscar:** `dos alias`, `self join`, `alias mismo tabla`, `propietario_id`, `acreedor_id`, `JOIN`, `difícil`, `examen difícil`, `fotomultas`

**Tipo de pregunta:** SQL

**Dificultad:** difícil

**Patrones relacionados:** caso clásico de FKs múltiples a la misma tabla.

**Trampas típicas:**
- Usar un solo JOIN a propietario → confusión entre dueño y pagador.

**Enunciado:**
Lista los pagos donde el **dueño** del vehículo es **distinto** del **pagador** de la multa. Columnas: `pago_id`, `placa`, `nombre_dueno`, `nombre_pagador`.

---

**Solución paso a paso:**

1. Necesito unir `pago → infraccion → vehiculo → propietario(dueno)` Y `pago → propietario(pagador)`.
2. Como `propietario` aparece DOS veces con roles diferentes, uso **dos alias**: `p_dueno` y `p_pagador`.
3. El filtro: `p_dueno.id <> p_pagador.id`.

```sql
SELECT pa.id AS pago_id,
       v.placa,
       p_dueno.nombre AS nombre_dueno,
       p_pagador.nombre AS nombre_pagador
FROM pago pa
JOIN infraccion i ON i.id = pa.infraccion_id
JOIN vehiculo v ON v.id = i.vehiculo_id
JOIN propietario p_dueno ON p_dueno.id = v.propietario_id
JOIN propietario p_pagador ON p_pagador.id = pa.acreedor_id
WHERE p_dueno.id <> p_pagador.id;
```

**Respuesta final:** ver código arriba.

---

### Ejercicio C5 — FULL OUTER JOIN — Cámaras y sus infracciones

**Keywords para buscar:** `FULL OUTER JOIN`, `FULL JOIN`, `JOIN`, `difícil`, `fotomultas`, `camara`, `infraccion`

**Tipo de pregunta:** SQL

**Dificultad:** difícil

**Patrones relacionados:** distinguir LEFT vs RIGHT vs FULL.

**Trampas típicas:** confundir si la pregunta requiere LEFT o FULL.

**Enunciado:**
Quiero un reporte que muestre:
- Cámaras sin infracciones (para detectar fallas).
- Infracciones huérfanas si las hubiera (en caso de borrado mal hecho que dejó referencias inválidas... aunque idealmente la FK lo previene).

Combina ambas con un solo JOIN. Columnas: `camara_id`, `alcaldia`, `infraccion_id`.

---

**Solución paso a paso:**

1. Cámaras sin infracciones → LEFT JOIN con `cam` a la izquierda.
2. Infracciones huérfanas → RIGHT JOIN.
3. Para tener ambos lados → **FULL OUTER JOIN**.

```sql
SELECT c.id AS camara_id,
       c.alcaldia,
       i.id AS infraccion_id
FROM camara c
FULL OUTER JOIN infraccion i ON i.camara_id = c.id
WHERE c.id IS NULL OR i.id IS NULL;
```

El `WHERE` filtra solo los casos "sin pareja" (justo lo que pediste).

**Respuesta final:** ver código arriba.

---

### Ejercicio C6 — Producto cartesiano "deliberado"

**Keywords para buscar:** `CROSS JOIN`, `producto cartesiano`, `JOIN`, `combinaciones`, `media`, `Tema 2`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Patrones relacionados:** combinaciones programáticas.

**Trampas típicas:**
- Hacer un CROSS JOIN sin querer (omitir ON en INNER JOIN).

**Enunciado:**
Genera todas las combinaciones posibles de (alcaldía, tipo de cámara) que existen en la BD, aunque no haya cámaras con esa combinación específica.

---

**Solución paso a paso:**

1. Necesito las alcaldías únicas y los tipos únicos.
2. CROSS JOIN entre ambos sets genera el producto cartesiano.

```sql
SELECT a.alcaldia, t.tipo
FROM (SELECT DISTINCT alcaldia FROM camara) a
CROSS JOIN (SELECT DISTINCT tipo FROM camara) t;
```

**Respuesta final:** ver código.

---

### Ejercicio C7 — Reescribir un NATURAL JOIN inseguro

**Keywords para buscar:** `NATURAL JOIN`, `JOIN seguro`, `debugging`, `media`, `Tema 2`

**Tipo de pregunta:** SQL / debugging

**Dificultad:** media

**Patrones relacionados:** convenciones de naming.

**Trampas típicas:**
- Pensar que NATURAL JOIN es siempre bueno.

**Enunciado:**
Tienes el código `SELECT * FROM vehiculo NATURAL JOIN propietario;`. ¿Qué problema tiene? Reescribe con un JOIN explícito.

---

**Solución paso a paso:**

1. NATURAL JOIN une por columnas con el mismo nombre.
2. `vehiculo` tiene columnas: `id, placa, marca, anio, color, propietario_id`.
3. `propietario` tiene: `id, nombre, apellido, correo, telefono`.
4. La única columna con nombre común es `id`. ⚠️ Pero `vehiculo.id` y `propietario.id` representan cosas distintas (id del vehículo vs id del propietario).
5. NATURAL JOIN une por `id`, lo cual es **incorrecto**: termina uniendo el vehículo con id=5 al propietario con id=5, que no tienen relación.

**Reescritura correcta:**
```sql
SELECT *
FROM vehiculo v
JOIN propietario p ON p.id = v.propietario_id;
```

**Respuesta final:**
- NATURAL JOIN se basa en convención de nombres y aquí une por `id` (incorrecto).
- Reescribir con `ON v.propietario_id = p.id`.
- **Regla:** evitar NATURAL JOIN; preferir JOIN ON explícito.

---

### Ejercicio C8 — JOIN con condición compuesta

**Keywords para buscar:** `JOIN compuesto`, `ON múltiple`, `JOIN`, `media`, `difícil`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Patrones relacionados:** PK compuesta.

**Trampas típicas:**
- Olvidar todos los términos de la PK compuesta en el ON.

**Enunciado:**
Imagina que añades a Fotomultas una tabla `revision_camara(camara_id, fecha, resultado)` con PK compuesta `(camara_id, fecha)`. Si quieres unir cada cámara con su revisión más reciente, ¿cómo planteas el JOIN?

---

**Solución paso a paso:**

1. Para cada cámara, quiero la última revisión.
2. Estrategia 1: subquery que obtiene la fecha máxima por cámara, luego JOIN.

```sql
SELECT c.id, c.alcaldia, r.fecha, r.resultado
FROM camara c
JOIN revision_camara r ON r.camara_id = c.id
WHERE r.fecha = (
    SELECT MAX(fecha) FROM revision_camara r2 WHERE r2.camara_id = c.id
);
```

2. Estrategia 2: usar función de ventana.

```sql
SELECT *
FROM (
    SELECT c.id, c.alcaldia, r.fecha, r.resultado,
           ROW_NUMBER() OVER (PARTITION BY c.id ORDER BY r.fecha DESC) AS rn
    FROM camara c
    JOIN revision_camara r ON r.camara_id = c.id
) t
WHERE rn = 1;
```

**Respuesta final:** la solución más legible suele ser con `ROW_NUMBER() OVER (PARTITION BY ... ORDER BY ... DESC)` y filtrar `rn = 1`.

---

## BLOQUE D — Aggregation, GROUP BY, HAVING

### Ejercicio D1 — COUNT simple

**Keywords para buscar:** `COUNT`, `aggregation`, `fácil`, `fotomultas`, `infraccion`

**Tipo de pregunta:** SQL

**Dificultad:** fácil

**Patrones relacionados:** Pregunta 7 del examen.

**Trampas típicas:**
- `COUNT(*)` vs `COUNT(col)`.

**Enunciado:**
¿Cuántas infracciones se han registrado en total?

---

**Solución paso a paso:**

```sql
SELECT COUNT(*) AS total_infracciones FROM infraccion;
```

**Respuesta final:** `SELECT COUNT(*) FROM infraccion;`.

---

### Ejercicio D2 — Vehículos con más de 5 infracciones (GROUP BY + HAVING)

**Keywords para buscar:** `GROUP BY`, `HAVING`, `COUNT`, `JOIN`, `media`, `fotomultas`, `infraccion`, `vehiculo`, `aggregation`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Patrones relacionados:** Pregunta 7 del examen práctica (creadores con ≥50 suscriptores).

**Trampas típicas:**
- Poner el filtro `COUNT(...) > 5` en WHERE (no funciona).

**Enunciado:**
Lista las placas de vehículos que tienen **más de 5 infracciones**. Columnas: `placa`, `n_infracciones`.

---

**Solución paso a paso:**

1. Agrupo por vehículo (placa).
2. Cuento las infracciones de cada uno.
3. Filtro los grupos con más de 5 → HAVING.

```sql
SELECT v.placa, COUNT(*) AS n_infracciones
FROM vehiculo v
JOIN infraccion i ON i.vehiculo_id = v.id
GROUP BY v.id, v.placa
HAVING COUNT(*) > 5;
```

> 💡 Nota: agrupé por `v.id, v.placa` (no solo por placa) por si hay placas repetidas. En producción, `v.id` es siempre seguro.

**Respuesta final:** ver código arriba.

---

### Ejercicio D3 — Promedio por categoría con WHERE + GROUP BY

**Keywords para buscar:** `AVG`, `GROUP BY`, `WHERE`, `media`, `fotomultas`, `infraccion`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Patrones relacionados:** combinación WHERE + GROUP BY.

**Trampas típicas:** filtrar fechas en HAVING en lugar de WHERE.

**Enunciado:**
Promedio del importe de infracciones, agrupado por `tipo`, considerando solo infracciones del último año.

---

**Solución paso a paso:**

```sql
SELECT tipo, AVG(importe) AS promedio
FROM infraccion
WHERE fecha >= NOW() - INTERVAL '1 year'
GROUP BY tipo;
```

El filtro de fecha va en WHERE (es filtro por fila, no por grupo).

**Respuesta final:** código arriba.

---

### Ejercicio D4 — WHERE vs HAVING — debugging

**Keywords para buscar:** `WHERE vs HAVING`, `debugging`, `HAVING`, `GROUP BY`, `media`, `examen difícil`

**Tipo de pregunta:** SQL / debugging

**Dificultad:** media

**Patrones relacionados:** confusión clásica entre WHERE y HAVING.

**Trampas típicas:**
- El error de poner el filtro en el lugar incorrecto.

**Enunciado:**
La siguiente query da error. Encuéntralo y corrígelo:

```sql
SELECT tipo, COUNT(*)
FROM infraccion
WHERE COUNT(*) > 10
GROUP BY tipo;
```

---

**Solución paso a paso:**

1. El error: `WHERE COUNT(*) > 10`. **No puedes usar funciones agregadas en WHERE** porque WHERE se ejecuta ANTES del GROUP BY.
2. El filtro sobre el resultado de un agregado debe ir en HAVING.

**Corrección:**
```sql
SELECT tipo, COUNT(*)
FROM infraccion
GROUP BY tipo
HAVING COUNT(*) > 10;
```

**Respuesta final:**
Cambiar `WHERE COUNT(*) > 10` por `HAVING COUNT(*) > 10` (ubicarlo después del GROUP BY).

---

### Ejercicio D5 — Top N con LIMIT

**Keywords para buscar:** `LIMIT`, `ORDER BY`, `top N`, `SUM`, `aggregation`, `media`, `fotomultas`, `propietario`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Patrones relacionados:** Pregunta 8 del examen práctica.

**Trampas típicas:**
- Olvidar el ORDER BY antes del LIMIT → el resultado es no determinístico.

**Enunciado:**
Top 10 propietarios con mayor monto total de multas (sumando todas las infracciones de todos sus vehículos). Columnas: `nombre`, `apellido`, `total_multas`. Si hay empate en el puesto 10, no hay problema.

---

**Solución paso a paso:**

```sql
SELECT p.nombre, p.apellido, SUM(i.importe) AS total_multas
FROM propietario p
JOIN vehiculo v ON v.propietario_id = p.id
JOIN infraccion i ON i.vehiculo_id = v.id
GROUP BY p.id, p.nombre, p.apellido
ORDER BY total_multas DESC
LIMIT 10;
```

> 💡 La nota "no hay problema con empate en el puesto 10" es exactamente la consideración del examen Q8. Significa que `LIMIT 10` es suficiente (no necesitas `WITH TIES`).

**Respuesta final:** código arriba.

---

### Ejercicio D6 — COUNT(*) vs COUNT(col)

**Keywords para buscar:** `COUNT(*)`, `COUNT(col)`, `NULL`, `debugging`, `conceptual`, `media`, `examen difícil`

**Tipo de pregunta:** conceptual / SQL

**Dificultad:** media

**Patrones relacionados:** comportamiento de NULL.

**Trampas típicas:**
- Pensar que `COUNT(col)` = `COUNT(*)` siempre.

**Enunciado:**
Una tabla `usuario` tiene 100 filas, de las cuales 30 tienen `telefono = NULL`. ¿Qué regresa cada query?

```sql
-- A
SELECT COUNT(*) FROM usuario;

-- B
SELECT COUNT(telefono) FROM usuario;

-- C
SELECT COUNT(DISTINCT telefono) FROM usuario;
```

---

**Solución paso a paso:**

- A: `COUNT(*)` cuenta TODAS las filas, incluyendo las que tienen NULL en cualquier columna. → **100**.
- B: `COUNT(telefono)` cuenta filas donde telefono NO es NULL. → **70**.
- C: `COUNT(DISTINCT telefono)` cuenta valores distintos no-NULL. Si los 70 teléfonos son únicos → 70; si hay repetidos → menos. Sin más info, depende.

**Respuesta final:**
- A: 100
- B: 70
- C: depende — entre 1 y 70, según cuántos teléfonos repetidos haya.

---

### Ejercicio D7 — Tipo de cámara que más detecta

**Keywords para buscar:** `GROUP BY`, `ORDER BY DESC`, `LIMIT 1`, `tipo`, `media`, `fotomultas`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Patrones relacionados:** ranking simple.

**Trampas típicas:**
- Asumir que hay un solo tipo top (puede haber empates).

**Enunciado:**
¿Cuál es el tipo de cámara que ha detectado más infracciones?

---

**Solución paso a paso:**

```sql
SELECT c.tipo, COUNT(*) AS n
FROM camara c
JOIN infraccion i ON i.camara_id = c.id
GROUP BY c.tipo
ORDER BY n DESC
LIMIT 1;
```

> 💡 Si quieres manejar empates, usa `RANK()` o `DENSE_RANK()` (ver bloque F).

**Respuesta final:** código arriba.

---

### Ejercicio D8 — Multi-aggregation en una sola pasada

**Keywords para buscar:** `múltiples agregados`, `aggregation`, `GROUP BY`, `media`, `difícil`, `fotomultas`

**Tipo de pregunta:** SQL

**Dificultad:** media-difícil

**Patrones relacionados:** dashboards y reportes.

**Trampas típicas:**
- Hacer múltiples queries cuando una basta.

**Enunciado:**
Por cada alcaldía, calcula: número de cámaras activas, número de cámaras inactivas, número total de infracciones detectadas.

---

**Solución paso a paso:**

1. Empezamos en `camara`.
2. Para cámaras activas/inactivas → uso `COUNT(*) FILTER (WHERE activa = TRUE)` en PostgreSQL, o un `CASE WHEN`.
3. Para infracciones, LEFT JOIN.

```sql
SELECT c.alcaldia,
       COUNT(*) FILTER (WHERE c.activa = TRUE) AS camaras_activas,
       COUNT(*) FILTER (WHERE c.activa = FALSE) AS camaras_inactivas,
       COUNT(i.id) AS n_infracciones
FROM camara c
LEFT JOIN infraccion i ON i.camara_id = c.id
GROUP BY c.alcaldia;
```

Versión portable (sin FILTER):

```sql
SELECT c.alcaldia,
       SUM(CASE WHEN c.activa = TRUE THEN 1 ELSE 0 END) AS camaras_activas,
       SUM(CASE WHEN c.activa = FALSE THEN 1 ELSE 0 END) AS camaras_inactivas,
       COUNT(i.id) AS n_infracciones
FROM camara c
LEFT JOIN infraccion i ON i.camara_id = c.id
GROUP BY c.alcaldia;
```

> ⚠️ Trampa sutil: `COUNT(*) FILTER (...)` cuenta las filas de cámaras (con duplicados por el JOIN), pero `COUNT(i.id)` solo cuenta filas con infracciones reales (gracias a LEFT JOIN). Cuidado: si una cámara tiene 3 infracciones, aparecerá 3 veces en el JOIN, lo que **infla** el conteo de cámaras. Para evitarlo, usa `COUNT(DISTINCT c.id) FILTER (...)`.

**Versión corregida** (más segura):

```sql
SELECT c.alcaldia,
       COUNT(DISTINCT c.id) FILTER (WHERE c.activa = TRUE) AS camaras_activas,
       COUNT(DISTINCT c.id) FILTER (WHERE c.activa = FALSE) AS camaras_inactivas,
       COUNT(i.id) AS n_infracciones
FROM camara c
LEFT JOIN infraccion i ON i.camara_id = c.id
GROUP BY c.alcaldia;
```

**Respuesta final:** código corregido arriba. Lección: cuidado con duplicados en JOINs cuando se cuentan entidades.

---

---

# 🔷 BLOQUE E — Subconsultas, EXISTS, ANY/ALL, CTEs

---

## Ejercicio E1 — Propietarios con más de 3 infracciones (subconsulta vs JOIN)

**Keywords para buscar:** `subquery`, `subconsulta`, `IN`, `JOIN`, `GROUP BY`, `HAVING`, `propietario`, `infraccion`, `dos formas`, `examen ITAM`, `fácil`

**Tipo de pregunta:** SQL — dos formas válidas

**Dificultad:** fácil-media

**Patrones relacionados:**
- Subconsulta no correlacionada en `IN`
- Equivalencia con JOIN + GROUP BY

**Trampas típicas:**
- Olvidar `GROUP BY` dentro de la subconsulta.
- Comparar contra `vehiculo.propietario_id` directamente sin pasar por las infracciones.

**Enunciado:**
Lista nombre y apellido de los propietarios que tienen más de 3 infracciones acumuladas en sus vehículos.

---

**Solución paso a paso:**

Forma 1 — subconsulta en `IN`:

```sql
SELECT p.nombre, p.apellido
FROM propietario p
WHERE p.id IN (
  SELECT v.propietario_id
  FROM vehiculo v
  JOIN infraccion i ON i.vehiculo_id = v.id
  GROUP BY v.propietario_id
  HAVING COUNT(*) > 3
);
```

Forma 2 — JOIN directo:

```sql
SELECT p.nombre, p.apellido
FROM propietario p
JOIN vehiculo v ON v.propietario_id = p.id
JOIN infraccion i ON i.vehiculo_id = v.id
GROUP BY p.id, p.nombre, p.apellido
HAVING COUNT(*) > 3;
```

Ambas devuelven lo mismo. La subconsulta tiende a ser más legible cuando solo necesitas filtrar; el JOIN cuando además necesitas datos de las infracciones.

**Respuesta final:** ambas queries arriba.

---

## Ejercicio E2 — EXISTS vs IN (cámaras con al menos una infracción)

**Keywords para buscar:** `EXISTS`, `IN`, `subquery correlacionada`, `camara`, `infraccion`, `NULL safe`, `examen ITAM`, `media`

**Tipo de pregunta:** SQL conceptual

**Dificultad:** media

**Patrones relacionados:**
- EXISTS con subconsulta correlacionada.
- `IN` con subconsulta no correlacionada.
- Sensibilidad a NULLs.

**Trampas típicas:**
- `NOT IN` con NULLs internos da resultado vacío inesperadamente.
- Olvidar la correlación `i.camara_id = c.id` dentro de `EXISTS`.

**Enunciado:**
Lista los `id` de cámaras que tienen al menos una infracción asociada. Resuelve con `EXISTS` y luego con `IN`. Explica cuál es más segura ante NULLs.

---

**Solución paso a paso:**

Con `EXISTS` (correlacionada):

```sql
SELECT c.id
FROM camara c
WHERE EXISTS (
  SELECT 1
  FROM infraccion i
  WHERE i.camara_id = c.id
);
```

Con `IN` (no correlacionada):

```sql
SELECT c.id
FROM camara c
WHERE c.id IN (SELECT i.camara_id FROM infraccion i);
```

**Sobre NULLs:** si la versión fuera `NOT IN` y `infraccion.camara_id` tuviera al menos un NULL, **toda** la consulta devolvería vacío porque `x NOT IN (NULL, 1, 2)` evalúa a UNKNOWN. `NOT EXISTS` no tiene ese problema. Por eso `EXISTS`/`NOT EXISTS` es más seguro.

**Respuesta final:** ambas queries arriba; preferir `EXISTS` cuando haya posibilidad de NULL.

---

## Ejercicio E3 — NOT EXISTS: propietarios sin pagos

**Keywords para buscar:** `NOT EXISTS`, `propietario`, `pago`, `acreedor_id`, `anti-join`, `LEFT JOIN IS NULL`, `examen ITAM`, `media`

**Tipo de pregunta:** SQL — anti-join

**Dificultad:** media

**Patrones relacionados:**
- Patrón anti-join.
- Tres formas: `NOT EXISTS`, `LEFT JOIN ... WHERE IS NULL`, `NOT IN`.

**Trampas típicas:**
- Usar `NOT IN` con posibles NULLs.
- Olvidar que el FK a buscar es `pago.acreedor_id`, no `pago.propietario_id`.

**Enunciado:**
Lista los propietarios que **nunca** han hecho un pago (es decir, no aparecen como `acreedor_id` en `pago`).

---

**Solución paso a paso:**

Con `NOT EXISTS`:

```sql
SELECT p.id, p.nombre, p.apellido
FROM propietario p
WHERE NOT EXISTS (
  SELECT 1
  FROM pago pg
  WHERE pg.acreedor_id = p.id
);
```

Con `LEFT JOIN ... IS NULL`:

```sql
SELECT p.id, p.nombre, p.apellido
FROM propietario p
LEFT JOIN pago pg ON pg.acreedor_id = p.id
WHERE pg.id IS NULL;
```

**Respuesta final:** ambas válidas. `NOT EXISTS` es preferible por NULL-safety y suele ser más rápida en muchos motores.

---

## Ejercicio E4 — Subconsulta correlacionada en SELECT (campo calculado por fila)

**Keywords para buscar:** `subquery correlacionada`, `scalar subquery`, `SELECT con subquery`, `propietario`, `examen ITAM`, `media-difícil`

**Tipo de pregunta:** SQL — scalar correlacionada

**Dificultad:** media-difícil

**Patrones relacionados:**
- Subquery escalar en `SELECT`.
- Alternativa con LEFT JOIN + GROUP BY.

**Trampas típicas:**
- Si la subquery devuelve más de una fila, error en ejecución.
- Si no hay infracciones, la subquery devuelve NULL — hay que usar `COALESCE`.

**Enunciado:**
Para cada propietario, muestra su nombre y el **importe total** de infracciones registradas en cualquiera de sus vehículos. Resuelve con subquery escalar correlacionada.

---

**Solución paso a paso:**

```sql
SELECT p.id,
       p.nombre,
       p.apellido,
       COALESCE((
         SELECT SUM(i.importe)
         FROM infraccion i
         JOIN vehiculo v ON v.id = i.vehiculo_id
         WHERE v.propietario_id = p.id
       ), 0) AS total_infracciones
FROM propietario p;
```

Alternativa con LEFT JOIN + GROUP BY (suele ser más rápida en grandes volúmenes):

```sql
SELECT p.id, p.nombre, p.apellido,
       COALESCE(SUM(i.importe), 0) AS total_infracciones
FROM propietario p
LEFT JOIN vehiculo v ON v.propietario_id = p.id
LEFT JOIN infraccion i ON i.vehiculo_id = v.id
GROUP BY p.id, p.nombre, p.apellido;
```

**Respuesta final:** la subquery correlacionada da el mismo resultado; usar `COALESCE` para evitar NULLs.

---

## Ejercicio E5 — ANY / ALL (infracción más cara por tipo)

**Keywords para buscar:** `ANY`, `ALL`, `SOME`, `subquery`, `>= ALL`, `infraccion`, `tipo`, `máximo`, `examen ITAM`, `difícil`

**Tipo de pregunta:** SQL — cuantificadores

**Dificultad:** difícil

**Patrones relacionados:**
- `>= ALL(subquery)` ≡ máximo.
- Equivalencia con `MAX()` agrupado o window function.

**Trampas típicas:**
- `= ANY` ≡ `IN`, pero `<> ANY` **no** es `NOT IN`.
- `ALL` con subconsulta vacía devuelve TRUE; `ANY` con vacía devuelve FALSE.

**Enunciado:**
Por cada tipo de infracción, lista las infracciones cuyo `importe` sea igual al máximo de su tipo. Resuelve con `>= ALL`.

---

**Solución paso a paso:**

Una infracción `i` es la más cara de su tipo si su `importe` es **mayor o igual a todos** los importes de infracciones del mismo tipo:

```sql
SELECT i.*
FROM infraccion i
WHERE i.importe >= ALL (
  SELECT i2.importe
  FROM infraccion i2
  WHERE i2.tipo = i.tipo
);
```

Equivalente con `MAX` y JOIN:

```sql
SELECT i.*
FROM infraccion i
JOIN (
  SELECT tipo, MAX(importe) AS max_imp
  FROM infraccion
  GROUP BY tipo
) m ON m.tipo = i.tipo AND m.max_imp = i.importe;
```

Equivalente con window function:

```sql
SELECT *
FROM (
  SELECT i.*, MAX(importe) OVER (PARTITION BY tipo) AS max_imp
  FROM infraccion i
) t
WHERE importe = max_imp;
```

**Respuesta final:** las tres queries arriba. Conceptualmente: `>= ALL(subquery)` = máximo.

---

## Ejercicio E6 — CTE con WITH (vehículos más infractados)

**Keywords para buscar:** `CTE`, `WITH`, `subquery`, `GROUP BY`, `vehiculo`, `infraccion`, `top N`, `examen ITAM`, `media`

**Tipo de pregunta:** SQL — CTE

**Dificultad:** media

**Patrones relacionados:**
- CTE para legibilidad.
- Equivalente a subquery en `FROM`.

**Trampas típicas:**
- Pensar que la CTE persiste — solo vive durante la consulta.
- Olvidar nombrar columnas si hay aliases ambiguos.

**Enunciado:**
Usando una CTE, obtén los 5 vehículos con más infracciones, mostrando placa, marca y total de infracciones.

---

**Solución paso a paso:**

```sql
WITH conteo AS (
  SELECT i.vehiculo_id, COUNT(*) AS n
  FROM infraccion i
  GROUP BY i.vehiculo_id
)
SELECT v.placa, v.marca, c.n
FROM conteo c
JOIN vehiculo v ON v.id = c.vehiculo_id
ORDER BY c.n DESC
LIMIT 5;
```

**Respuesta final:** query arriba. Las CTEs no son obligatorias pero hacen la query muchísimo más legible cuando hay agregaciones que se reutilizan.

---

## Ejercicio E7 — CTE encadenadas (alcaldías + ranking)

**Keywords para buscar:** `CTE`, `WITH`, `múltiples CTEs`, `RANK`, `alcaldia`, `infraccion`, `window function`, `examen ITAM`, `difícil`

**Tipo de pregunta:** SQL — CTEs múltiples + window

**Dificultad:** difícil

**Patrones relacionados:**
- Encadenar CTEs.
- Combinar con window functions.

**Trampas típicas:**
- Pensar que la segunda CTE no puede referenciar la primera (sí puede).
- Olvidar el `OVER ()` en `RANK()`.

**Enunciado:**
Usando dos CTEs encadenadas:
1. Calcula el total de infracciones por alcaldía.
2. Asigna un ranking (1 = más infracciones).
3. Devuelve solo las top 3 alcaldías.

---

**Solución paso a paso:**

```sql
WITH por_alcaldia AS (
  SELECT c.alcaldia, COUNT(*) AS total
  FROM camara c
  JOIN infraccion i ON i.camara_id = c.id
  GROUP BY c.alcaldia
),
con_ranking AS (
  SELECT alcaldia, total,
         RANK() OVER (ORDER BY total DESC) AS rk
  FROM por_alcaldia
)
SELECT *
FROM con_ranking
WHERE rk <= 3;
```

**Respuesta final:** query arriba. `RANK()` se aplica sobre el resultado de la primera CTE; si quieres "top 3 sin empates" usa `ROW_NUMBER()`.

---

## Ejercicio E8 — EXISTS anidado: propietarios cuyos vehículos TODOS tienen infracción

**Keywords para buscar:** `NOT EXISTS`, `doble negación`, `división relacional`, `propietario`, `vehiculo`, `infraccion`, `examen ITAM`, `MUY difícil`, `trampa lógica`

**Tipo de pregunta:** SQL — división relacional

**Dificultad:** MUY difícil

**Patrones relacionados:**
- División relacional con doble `NOT EXISTS`.
- Universal cuantificado (∀) → `NOT EXISTS (... NOT EXISTS ...)`.

**Trampas típicas:**
- Hacerlo con un único EXISTS (solo prueba que **al menos uno** tiene infracción, no **todos**).
- Olvidar que el "para todo" en SQL se expresa como "no existe ninguno que no cumpla".

**Enunciado:**
Lista los propietarios cuyos **todos** sus vehículos tienen al menos una infracción registrada. (Si un propietario tiene 3 vehículos, los 3 deben tener infracciones).

---

**Solución paso a paso:**

Reformulación: "no existe ningún vehículo del propietario sin infracciones".

```sql
SELECT p.id, p.nombre, p.apellido
FROM propietario p
WHERE NOT EXISTS (
  SELECT 1
  FROM vehiculo v
  WHERE v.propietario_id = p.id
    AND NOT EXISTS (
      SELECT 1
      FROM infraccion i
      WHERE i.vehiculo_id = v.id
    )
);
```

> ⚠️ Cuidado con el caso límite: si un propietario no tiene vehículos, esta query lo incluye (vacíamente cumple "todos sus vehículos tienen infracción" porque no hay vehículos que falten). Para excluirlos, agrega `AND EXISTS (SELECT 1 FROM vehiculo v WHERE v.propietario_id = p.id)`.

Versión "al menos un vehículo y todos infractados":

```sql
SELECT p.id, p.nombre, p.apellido
FROM propietario p
WHERE EXISTS (SELECT 1 FROM vehiculo v WHERE v.propietario_id = p.id)
  AND NOT EXISTS (
    SELECT 1 FROM vehiculo v
    WHERE v.propietario_id = p.id
      AND NOT EXISTS (SELECT 1 FROM infraccion i WHERE i.vehiculo_id = v.id)
  );
```

Alternativa con COUNT (más intuitiva):

```sql
SELECT p.id, p.nombre, p.apellido
FROM propietario p
JOIN vehiculo v ON v.propietario_id = p.id
LEFT JOIN infraccion i ON i.vehiculo_id = v.id
GROUP BY p.id, p.nombre, p.apellido
HAVING COUNT(DISTINCT v.id) = COUNT(DISTINCT v.id) FILTER (WHERE i.id IS NOT NULL);
```

**Respuesta final:** la versión con doble `NOT EXISTS` (segunda) es la canónica de división relacional.

---

## Ejercicio E9 — CTE recursiva (camino de pagos en cadena, conceptual)

**Keywords para buscar:** `CTE recursiva`, `WITH RECURSIVE`, `UNION ALL`, `caso base`, `paso recursivo`, `examen ITAM`, `difícil`, `teórico`

**Tipo de pregunta:** SQL — recursión (conceptual)

**Dificultad:** difícil (conceptual)

**Patrones relacionados:**
- Estructura `WITH RECURSIVE cte AS (base UNION ALL paso) SELECT ...`.
- Recorridos de jerarquías.

**Trampas típicas:**
- Olvidar `UNION ALL` (debe ser ALL, no UNION).
- Olvidar condición de parada → bucle infinito.

**Enunciado:**
Supón que tienes una tabla `empleado(id, nombre, jefe_id)` donde `jefe_id` es FK a la misma tabla. Escribe una CTE recursiva que liste, dado un empleado raíz con id = 1, **todos** sus subordinados directos e indirectos.

---

**Solución paso a paso:**

```sql
WITH RECURSIVE descendientes AS (
  -- Caso base: el empleado raíz
  SELECT id, nombre, jefe_id, 0 AS nivel
  FROM empleado
  WHERE id = 1

  UNION ALL

  -- Paso recursivo: empleados cuyo jefe ya está en la CTE
  SELECT e.id, e.nombre, e.jefe_id, d.nivel + 1
  FROM empleado e
  JOIN descendientes d ON e.jefe_id = d.id
)
SELECT * FROM descendientes;
```

**Cómo razonarla:**
1. **Caso base:** el conjunto inicial (la raíz).
2. **Paso recursivo:** une el JOIN entre la tabla original y el conjunto acumulado hasta ese momento.
3. La recursión termina cuando el paso recursivo no genera filas nuevas.

**Respuesta final:** query arriba. Patrón general que también sirve para bills of materials, comentarios anidados, dependencias.

---

## Ejercicio E10 — IN vs JOIN: ¿pueden dar resultados diferentes?

**Keywords para buscar:** `IN vs JOIN`, `duplicados`, `DISTINCT`, `cardinalidad`, `subquery`, `conceptual`, `examen ITAM`, `media`, `trampa`

**Tipo de pregunta:** conceptual

**Dificultad:** media

**Patrones relacionados:**
- Subquery `IN` nunca duplica.
- JOIN puede duplicar si la tabla derecha tiene varios matches.

**Trampas típicas:**
- Reemplazar `IN` por JOIN sin agregar `DISTINCT` cuando hay 1:N.

**Enunciado:**
Considera estas dos queries sobre el ERD. ¿Pueden devolver resultados diferentes? Explica.

```sql
-- A
SELECT p.id, p.nombre
FROM propietario p
WHERE p.id IN (SELECT v.propietario_id FROM vehiculo v);

-- B
SELECT p.id, p.nombre
FROM propietario p
JOIN vehiculo v ON v.propietario_id = p.id;
```

---

**Solución paso a paso:**

- **A** devuelve cada propietario **una sola vez** si tiene al menos un vehículo (el `IN` no duplica).
- **B** devuelve un propietario **tantas veces como vehículos tenga**. Si Juan tiene 3 vehículos, aparece 3 veces.

Para que ambas sean equivalentes, **B** debe usar `DISTINCT`:

```sql
SELECT DISTINCT p.id, p.nombre
FROM propietario p
JOIN vehiculo v ON v.propietario_id = p.id;
```

**Respuesta final:** sí pueden diferir. `IN` deduplica implícitamente; el JOIN no. Es trampa clásica de examen.

---

# 🔷 BLOQUE F — Funciones de ventana

---

## Ejercicio F1 — ROW_NUMBER vs RANK vs DENSE_RANK

**Keywords para buscar:** `ROW_NUMBER`, `RANK`, `DENSE_RANK`, `window function`, `OVER`, `PARTITION BY`, `ORDER BY`, `empates`, `examen ITAM`, `fácil-media`

**Tipo de pregunta:** conceptual + SQL

**Dificultad:** fácil-media

**Patrones relacionados:**
- Diferencia entre las tres funciones de ranking.

**Trampas típicas:**
- Confundir RANK con DENSE_RANK.
- Olvidar `PARTITION BY` cuando se quiere ranking por grupo.

**Enunciado:**
Dado el siguiente conjunto de importes de infracciones del mismo tipo: 1000, 1000, 800, 700, 500. Calcula los valores de `ROW_NUMBER()`, `RANK()` y `DENSE_RANK()` ordenando por importe descendente.

---

**Solución paso a paso:**

| importe | ROW_NUMBER | RANK | DENSE_RANK |
|---|---|---|---|
| 1000 | 1 | 1 | 1 |
| 1000 | 2 | 1 | 1 |
| 800 | 3 | 3 | 2 |
| 700 | 4 | 4 | 3 |
| 500 | 5 | 5 | 4 |

Diferencias clave:
- **ROW_NUMBER:** numera secuencial, rompe empates arbitrariamente.
- **RANK:** mismos valores → misma posición; deja huecos (no hay 2 después de 1,1).
- **DENSE_RANK:** mismos valores → misma posición; NO deja huecos.

**Respuesta final:** tabla arriba.

---

## Ejercicio F2 — Top 1 por grupo (vehículo con infracción más cara por tipo)

**Keywords para buscar:** `top 1 por grupo`, `ROW_NUMBER`, `PARTITION BY`, `subquery`, `window function`, `examen ITAM`, `media-difícil`

**Tipo de pregunta:** SQL — top N por grupo

**Dificultad:** media-difícil

**Patrones relacionados:**
- Patrón clásico: `ROW_NUMBER() OVER (PARTITION BY g ORDER BY x DESC)` luego filtrar `WHERE rn = 1`.

**Trampas típicas:**
- Poner `WHERE rn = 1` directo: no se puede; tiene que ir en subquery o CTE porque el WHERE se evalúa antes de las window functions.

**Enunciado:**
Por cada tipo de infracción, devuelve el `vehiculo_id`, `importe` y `fecha` de la infracción más cara de ese tipo.

---

**Solución paso a paso:**

```sql
WITH ranked AS (
  SELECT i.vehiculo_id, i.tipo, i.importe, i.fecha,
         ROW_NUMBER() OVER (PARTITION BY i.tipo ORDER BY i.importe DESC) AS rn
  FROM infraccion i
)
SELECT vehiculo_id, tipo, importe, fecha
FROM ranked
WHERE rn = 1;
```

**Por qué necesita subquery/CTE:**
- Orden de ejecución: FROM → WHERE → GROUP BY → SELECT (con window) → ORDER BY.
- `ROW_NUMBER()` se calcula en el SELECT; no existe todavía cuando se evalúa WHERE.

**Si quieres incluir empates** (varios vehículos con el mismo importe máximo): cambia a `RANK()` y filtra `WHERE rk = 1`.

**Respuesta final:** query arriba.

---

## Ejercicio F3 — LAG y LEAD (variación de importe respecto a la anterior)

**Keywords para buscar:** `LAG`, `LEAD`, `window function`, `ORDER BY`, `serie temporal`, `diferencia respecto anterior`, `infraccion`, `examen ITAM`, `media`

**Tipo de pregunta:** SQL — LAG/LEAD

**Dificultad:** media

**Patrones relacionados:**
- Comparar fila actual con anterior/siguiente.
- Útil para diferencias, tasas de cambio, gaps temporales.

**Trampas típicas:**
- Olvidar que la primera fila tendrá NULL en LAG.

**Enunciado:**
Para cada vehículo, ordena sus infracciones cronológicamente y calcula la diferencia de importe respecto a la infracción anterior.

---

**Solución paso a paso:**

```sql
SELECT
  i.vehiculo_id,
  i.fecha,
  i.importe,
  LAG(i.importe) OVER (PARTITION BY i.vehiculo_id ORDER BY i.fecha) AS importe_anterior,
  i.importe - LAG(i.importe) OVER (PARTITION BY i.vehiculo_id ORDER BY i.fecha) AS variacion
FROM infraccion i;
```

- Para la **primera** infracción de cada vehículo, `LAG` devuelve NULL → `variacion` será NULL.
- Si quieres considerar la primera como 0, envuelve con `COALESCE(LAG(...), i.importe) AS importe_anterior`.

**Respuesta final:** query arriba.

---

## Ejercicio F4 — Acumulado mensual (estilo Q9 del examen YouTube)

**Keywords para buscar:** `SUM acumulado`, `running total`, `OVER ORDER BY`, `window frame`, `serie temporal`, `mes`, `acumulado`, `examen ITAM`, `difícil`, `Q9`

**Tipo de pregunta:** SQL — acumulado temporal

**Dificultad:** difícil

**Patrones relacionados:**
- `SUM(...) OVER (ORDER BY mes ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)`.
- Truncar fechas con `DATE_TRUNC`.
- Conteo por mes vs acumulado.

**Trampas típicas:**
- Olvidar el `ORDER BY` en `OVER` → la window se aplica a todo el conjunto.
- Confundir `ROWS` con `RANGE` (importante si hay empates en la columna de ordenamiento).

**Enunciado:**
Para cada mes, calcula:
1. El número de infracciones en ese mes.
2. El acumulado de infracciones desde el inicio del tiempo hasta ese mes inclusive.

---

**Solución paso a paso:**

Paso 1: agrupar por mes:

```sql
WITH por_mes AS (
  SELECT DATE_TRUNC('month', fecha) AS mes,
         COUNT(*) AS infracciones_mes
  FROM infraccion
  GROUP BY DATE_TRUNC('month', fecha)
)
SELECT mes,
       infracciones_mes,
       SUM(infracciones_mes) OVER (ORDER BY mes) AS acumulado
FROM por_mes
ORDER BY mes;
```

**Por qué funciona:**
- La CTE agrupa por mes → una fila por mes.
- La window `SUM(...) OVER (ORDER BY mes)` por defecto usa `RANGE UNBOUNDED PRECEDING AND CURRENT ROW`, así que suma todo desde el inicio hasta el mes actual.

**Respuesta final:** query arriba. Patrón idéntico al de Q9 del examen YouTube (acumulado de videos por mes).

---

## Ejercicio F5 — RANGE vs ROWS vs GROUPS con valores específicos

**Keywords para buscar:** `RANGE`, `ROWS`, `GROUPS`, `window frame`, `frame clause`, `empates`, `examen ITAM`, `MUY difícil`, `conceptual`

**Tipo de pregunta:** conceptual avanzado

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Tres modos de frame: por filas, por valor, por grupos de empates.

**Trampas típicas:**
- Asumir que `RANGE` y `ROWS` son intercambiables.
- No considerar empates al usar `RANGE`.

**Enunciado:**
Dada esta serie ordenada por `valor`: 10, 20, 20, 20, 30, 40. Y la ventana `BETWEEN CURRENT ROW AND CURRENT ROW`. Calcula la suma para cada fila usando `ROWS`, `RANGE` y `GROUPS`.

---

**Solución paso a paso:**

- **ROWS BETWEEN CURRENT ROW AND CURRENT ROW:** solo la fila actual.
- **RANGE BETWEEN CURRENT ROW AND CURRENT ROW:** todas las filas con el **mismo valor** que la actual.
- **GROUPS BETWEEN CURRENT ROW AND CURRENT ROW:** el grupo de empates actual (igual a RANGE en este caso porque CURRENT ROW = mismo grupo de valor).

| valor | ROWS | RANGE | GROUPS |
|---|---|---|---|
| 10 | 10 | 10 | 10 |
| 20 | 20 | 20+20+20 = 60 | 60 |
| 20 | 20 | 60 | 60 |
| 20 | 20 | 60 | 60 |
| 30 | 30 | 30 | 30 |
| 40 | 40 | 40 | 40 |

**Diferencia clave RANGE vs GROUPS:**
- `RANGE BETWEEN 1 PRECEDING AND CURRENT ROW`: todas las filas con `valor BETWEEN current-1 AND current`. Si el ordenamiento es por importe = 100, mira filas con valor entre 99 y 100.
- `GROUPS BETWEEN 1 PRECEDING AND CURRENT ROW`: las del grupo actual y el grupo anterior (en número de grupos distintos, no en valor).

**Respuesta final:** tabla arriba. Lección: con empates, `ROWS ≠ RANGE`.

---

## Ejercicio F6 — Promedio móvil de 3 meses

**Keywords para buscar:** `promedio móvil`, `moving average`, `AVG OVER`, `ROWS BETWEEN`, `serie temporal`, `examen ITAM`, `difícil`

**Tipo de pregunta:** SQL — window con frame

**Dificultad:** difícil

**Patrones relacionados:**
- Frame explícito `ROWS BETWEEN N PRECEDING AND CURRENT ROW`.
- Promedios móviles, suavizados.

**Trampas típicas:**
- Olvidar el frame → AVG aplica sobre toda la partición desde el inicio.
- Usar RANGE en lugar de ROWS para "últimos N meses" (RANGE se basa en valores, no posiciones).

**Enunciado:**
Para cada mes, calcula el promedio móvil de los últimos 3 meses (incluyendo el actual) del importe total de infracciones.

---

**Solución paso a paso:**

```sql
WITH por_mes AS (
  SELECT DATE_TRUNC('month', fecha) AS mes,
         SUM(importe) AS total_mes
  FROM infraccion
  GROUP BY DATE_TRUNC('month', fecha)
)
SELECT mes,
       total_mes,
       AVG(total_mes) OVER (
         ORDER BY mes
         ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS promedio_movil_3m
FROM por_mes
ORDER BY mes;
```

- `2 PRECEDING AND CURRENT ROW` = ventana de 3 filas (actual + 2 anteriores).
- Para los primeros 2 meses, el promedio será sobre menos filas (no hay suficientes anteriores).

**Respuesta final:** query arriba.

---

## Ejercicio F7 — NTILE: dividir vehículos en 4 cuartiles

**Keywords para buscar:** `NTILE`, `cuartiles`, `percentiles`, `window function`, `OVER ORDER BY`, `clasificar`, `examen ITAM`, `media`

**Tipo de pregunta:** SQL — NTILE

**Dificultad:** media

**Patrones relacionados:**
- `NTILE(N)` divide el resultado ordenado en N grupos lo más iguales posible.

**Trampas típicas:**
- Pensar que cada bucket tiene exactamente N/total filas — los primeros buckets pueden tener una fila más.

**Enunciado:**
Clasifica los vehículos en 4 cuartiles según la suma de importes de sus infracciones (cuartil 1 = más infractores).

---

**Solución paso a paso:**

```sql
WITH total_por_vehiculo AS (
  SELECT v.id, v.placa,
         COALESCE(SUM(i.importe), 0) AS total_importe
  FROM vehiculo v
  LEFT JOIN infraccion i ON i.vehiculo_id = v.id
  GROUP BY v.id, v.placa
)
SELECT id, placa, total_importe,
       NTILE(4) OVER (ORDER BY total_importe DESC) AS cuartil
FROM total_por_vehiculo;
```

- Cuartil 1: los 25% más infractores.
- Cuartil 4: los 25% con menos importe.

**Respuesta final:** query arriba.

---

## Ejercicio F8 — Window function dentro de CTE con LEFT JOIN

**Keywords para buscar:** `CTE`, `window function`, `LEFT JOIN`, `combinado`, `RANK`, `propietario`, `examen ITAM`, `MUY difícil`

**Tipo de pregunta:** SQL — combinada compleja

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Combinar 3+ conceptos en una sola query.

**Trampas típicas:**
- Olvidar GROUP BY en la CTE base.
- Aplicar la window function antes de filtrar — orden incorrecto.

**Enunciado:**
Para cada alcaldía, encuentra el propietario que ha pagado más dinero (suma de `pago.importe`) por infracciones cometidas en esa alcaldía. Si la alcaldía no tiene pagos, muéstrala igualmente con NULL en el campo del propietario.

---

**Solución paso a paso:**

```sql
WITH pagos_por_alc_prop AS (
  SELECT c.alcaldia,
         pg.acreedor_id,
         SUM(pg.importe) AS total_pagado
  FROM camara c
  JOIN infraccion i ON i.camara_id = c.id
  JOIN pago pg ON pg.infraccion_id = i.id
  GROUP BY c.alcaldia, pg.acreedor_id
),
ranked AS (
  SELECT alcaldia, acreedor_id, total_pagado,
         ROW_NUMBER() OVER (PARTITION BY alcaldia ORDER BY total_pagado DESC) AS rn
  FROM pagos_por_alc_prop
)
SELECT DISTINCT c.alcaldia,
       r.acreedor_id,
       p.nombre,
       p.apellido,
       r.total_pagado
FROM camara c
LEFT JOIN ranked r ON r.alcaldia = c.alcaldia AND r.rn = 1
LEFT JOIN propietario p ON p.id = r.acreedor_id;
```

**Por qué este orden:**
1. CTE 1: agrega pagos por (alcaldía, acreedor).
2. CTE 2: rankea dentro de cada alcaldía.
3. Query final: LEFT JOIN desde `camara` para incluir alcaldías sin pagos.

**Respuesta final:** query arriba. Patrón muy estilo final ITAM: combina agregación + window + LEFT JOIN para incluir grupos vacíos.

---

# 🔷 BLOQUE G — DDL: CREATE, ALTER, constraints

---

## Ejercicio G1 — CREATE TABLE básico con todos los constraints

**Keywords para buscar:** `CREATE TABLE`, `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`, `CHECK`, `DEFAULT`, `constraint inline`, `examen ITAM`, `fácil-media`

**Tipo de pregunta:** SQL — DDL

**Dificultad:** fácil-media

**Patrones relacionados:**
- Definición completa de una tabla con todos los constraints.

**Trampas típicas:**
- Olvidar tipo de la columna.
- Poner UNIQUE en una columna que después dará problemas con NULL.

**Enunciado:**
Crea la tabla `usuario(id, nombre, correo, edad, fecha_registro, plan)` donde:
- `id` es PK (autoincremental tipo SERIAL).
- `nombre` es obligatorio.
- `correo` debe ser único y obligatorio.
- `edad` debe ser ≥ 18.
- `fecha_registro` por default toma la fecha actual.
- `plan` solo puede ser `'free'`, `'pro'`, `'enterprise'`.

---

**Solución paso a paso:**

```sql
CREATE TABLE usuario (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  correo VARCHAR(150) NOT NULL UNIQUE,
  edad INTEGER NOT NULL CHECK (edad >= 18),
  fecha_registro DATE NOT NULL DEFAULT CURRENT_DATE,
  plan VARCHAR(20) NOT NULL CHECK (plan IN ('free', 'pro', 'enterprise'))
);
```

Cada constraint razonado:
- `SERIAL PRIMARY KEY`: autoincremento + única + no nula.
- `NOT NULL UNIQUE`: obligatorio y sin duplicados.
- `CHECK (edad >= 18)`: regla a nivel fila.
- `DEFAULT CURRENT_DATE`: si no se especifica, toma fecha actual.
- `CHECK (plan IN (...))`: lista cerrada de valores permitidos.

**Respuesta final:** query arriba.

---

## Ejercicio G2 — FOREIGN KEY con ON DELETE CASCADE (estilo Q11 examen)

**Keywords para buscar:** `FOREIGN KEY`, `REFERENCES`, `ON DELETE CASCADE`, `ON UPDATE CASCADE`, `borrado en cascada`, `examen ITAM`, `Q11`, `media`

**Tipo de pregunta:** SQL — DDL con CASCADE

**Dificultad:** media

**Patrones relacionados:**
- Comportamiento referencial: CASCADE, SET NULL, RESTRICT, NO ACTION.

**Trampas típicas:**
- Confundir CASCADE con SET NULL.
- Pensar que CASCADE solo afecta DELETE, no UPDATE.

**Enunciado:**
Crea la tabla `comentario(id, contenido, video_id, usuario_id, fecha)` donde:
- `video_id` referencia `video(id)` y al borrar el video se borren todos sus comentarios.
- `usuario_id` referencia `usuario(id)` y al borrar el usuario se pongan a NULL.

---

**Solución paso a paso:**

```sql
CREATE TABLE comentario (
  id SERIAL PRIMARY KEY,
  contenido TEXT NOT NULL,
  video_id INTEGER NOT NULL,
  usuario_id INTEGER,
  fecha TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (video_id) REFERENCES video(id) ON DELETE CASCADE,
  FOREIGN KEY (usuario_id) REFERENCES usuario(id) ON DELETE SET NULL
);
```

- `ON DELETE CASCADE`: si se borra el video, se borran los comentarios automáticamente.
- `ON DELETE SET NULL`: si se borra el usuario, el comentario se queda pero `usuario_id` queda NULL — por eso `usuario_id` **NO** puede ser NOT NULL.

**Razonamiento del NOT NULL en `usuario_id`:** no puede ser NOT NULL porque `SET NULL` lo violaría inmediatamente al borrar un usuario. Si quieres NOT NULL, usa `ON DELETE CASCADE` o `RESTRICT`.

**Respuesta final:** query arriba con razonamiento.

---

## Ejercicio G3 — ALTER TABLE: añadir columna NOT NULL a tabla con datos

**Keywords para buscar:** `ALTER TABLE`, `ADD COLUMN`, `SET NOT NULL`, `tabla con datos`, `default`, `dos pasos`, `examen ITAM`, `media-difícil`, `trampa`

**Tipo de pregunta:** SQL — DDL evolutiva

**Dificultad:** media-difícil

**Patrones relacionados:**
- Añadir columna NOT NULL a tabla no vacía.
- Estrategia en 3 pasos.

**Trampas típicas:**
- Hacer `ADD COLUMN nombre VARCHAR NOT NULL` directo → falla porque las filas existentes no tienen valor.

**Enunciado:**
Tienes la tabla `propietario` con miles de filas. Quieres añadir la columna `pais` que debe ser NOT NULL, con valor por defecto `'México'`. ¿Cómo lo haces sin que falle?

---

**Solución paso a paso:**

Opción 1 — un solo `ALTER` con `DEFAULT` (PostgreSQL acepta esto):

```sql
ALTER TABLE propietario
ADD COLUMN pais VARCHAR(50) NOT NULL DEFAULT 'México';
```

PostgreSQL puebla las filas existentes con `'México'` automáticamente.

Opción 2 — los 3 pasos clásicos (estándar SQL):

```sql
-- 1. Añadir como nullable
ALTER TABLE propietario ADD COLUMN pais VARCHAR(50);

-- 2. Poblar con valor
UPDATE propietario SET pais = 'México';

-- 3. Imponer NOT NULL
ALTER TABLE propietario ALTER COLUMN pais SET NOT NULL;
```

- Esta opción funciona en cualquier RDBMS.

**Respuesta final:** ambas opciones. La opción 1 es la práctica en PostgreSQL; la opción 2 es la portable.

---

## Ejercicio G4 — Añadir FK a tabla existente con datos inválidos

**Keywords para buscar:** `ALTER TABLE ADD CONSTRAINT`, `FOREIGN KEY`, `datos inválidos`, `limpiar antes`, `validación`, `examen ITAM`, `difícil`, `trampa`

**Tipo de pregunta:** SQL — DDL + DML correctivo

**Dificultad:** difícil

**Patrones relacionados:**
- Saneamiento de datos antes de añadir FK.

**Trampas típicas:**
- Asumir que `ADD FK` funciona sin verificar datos.

**Enunciado:**
Tienes la tabla `vehiculo` con la columna `propietario_id` que actualmente NO es FK. Algunos vehículos tienen `propietario_id = 99999` que no existe en `propietario`. Diseña la secuencia de pasos para añadir la FK sin perder datos.

---

**Solución paso a paso:**

Plan:
1. Identificar filas con `propietario_id` inválido.
2. Decidir qué hacer con ellas (poner NULL, asignar a un propietario "desconocido", borrar).
3. Añadir la FK.

```sql
-- 1. Diagnóstico
SELECT v.id, v.placa, v.propietario_id
FROM vehiculo v
LEFT JOIN propietario p ON p.id = v.propietario_id
WHERE p.id IS NULL;

-- 2. Estrategia A: poner a NULL (requiere que la columna sea nullable)
UPDATE vehiculo
SET propietario_id = NULL
WHERE propietario_id NOT IN (SELECT id FROM propietario);

-- O Estrategia B: crear propietario "desconocido" y reasignar
INSERT INTO propietario (id, nombre, apellido) VALUES (0, 'Desconocido', '-');
UPDATE vehiculo
SET propietario_id = 0
WHERE propietario_id NOT IN (SELECT id FROM propietario);

-- 3. Añadir FK
ALTER TABLE vehiculo
ADD CONSTRAINT fk_vehiculo_propietario
FOREIGN KEY (propietario_id) REFERENCES propietario(id);
```

**Respuesta final:** secuencia arriba.

---

## Ejercicio G5 — Crear tabla "como" otra (CREATE TABLE LIKE)

**Keywords para buscar:** `CREATE TABLE LIKE`, `INCLUDING ALL`, `clonar estructura`, `tabla espejo`, `examen ITAM`, `Q11`, `media`

**Tipo de pregunta:** SQL — DDL clonación

**Dificultad:** media

**Patrones relacionados:**
- Crear tabla con la misma estructura que otra.
- Q11 del examen YouTube pedía algo parecido.

**Trampas típicas:**
- `LIKE` sin `INCLUDING ...` solo copia columnas, no constraints.

**Enunciado:**
Crea una tabla `infraccion_archivada` con exactamente la misma estructura que `infraccion`, incluyendo constraints, defaults e índices.

---

**Solución paso a paso:**

```sql
CREATE TABLE infraccion_archivada (
  LIKE infraccion INCLUDING ALL
);
```

Opciones de `INCLUDING`:
- `INCLUDING DEFAULTS`: copia DEFAULT.
- `INCLUDING CONSTRAINTS`: copia CHECK y NOT NULL (no FKs).
- `INCLUDING INDEXES`: copia índices.
- `INCLUDING ALL`: todo lo anterior.

⚠️ **Importante:** `LIKE` NO copia FKs. Si necesitas FKs, agrégalas manualmente con `ALTER TABLE`.

Variante: copiar también los **datos**:

```sql
CREATE TABLE infraccion_archivada AS
SELECT * FROM infraccion;
```

Esta variante NO copia constraints, solo crea las columnas con los tipos inferidos.

**Respuesta final:** `CREATE TABLE ... (LIKE ... INCLUDING ALL)` para estructura; `CREATE TABLE ... AS SELECT` para estructura + datos sin constraints.

---

## Ejercicio G6 — DROP TABLE y dependencias (CASCADE)

**Keywords para buscar:** `DROP TABLE`, `CASCADE`, `RESTRICT`, `FK dependiente`, `examen ITAM`, `fácil-media`, `trampa`

**Tipo de pregunta:** SQL — DDL eliminación

**Dificultad:** fácil-media

**Patrones relacionados:**
- DROP cuando hay tablas que dependen.

**Trampas típicas:**
- `DROP TABLE propietario` falla si `vehiculo` tiene FK.

**Enunciado:**
Quieres borrar la tabla `propietario`, pero `vehiculo` la referencia. ¿Qué pasa con cada opción?

```sql
DROP TABLE propietario;
DROP TABLE propietario RESTRICT;
DROP TABLE propietario CASCADE;
```

---

**Solución paso a paso:**

- `DROP TABLE propietario;` → por defecto es `RESTRICT` en estándar SQL; falla con error "other objects depend on it".
- `DROP TABLE propietario RESTRICT;` → falla explícitamente igual.
- `DROP TABLE propietario CASCADE;` → borra `propietario` Y borra automáticamente la **constraint FK** de `vehiculo` (NO borra la tabla `vehiculo` ni sus datos). La columna `vehiculo.propietario_id` queda como columna normal sin FK.

> ⚠️ Trampa frecuente: muchos creen que `CASCADE` en DROP borra las tablas dependientes. **No**: solo borra los **objetos dependientes** como constraints, vistas que la usan, etc. Para borrar la tabla referenciante también, hay que hacer `DROP TABLE vehiculo, propietario CASCADE`.

**Respuesta final:** explicación arriba.

---

## Ejercicio G7 — Modificar constraint existente

**Keywords para buscar:** `ALTER TABLE DROP CONSTRAINT`, `ADD CONSTRAINT`, `modificar CHECK`, `cambiar regla`, `examen ITAM`, `media`

**Tipo de pregunta:** SQL — DDL modificación

**Dificultad:** media

**Patrones relacionados:**
- Para cambiar un CHECK, no existe ALTER directo: hay que DROP + ADD.

**Trampas típicas:**
- Buscar `ALTER CONSTRAINT` que no existe.

**Enunciado:**
La tabla `usuario` tiene `CHECK (edad >= 18)`. Quieres cambiar la regla a `edad >= 13`. ¿Cómo lo haces? (Suponiendo que el constraint se llama `usuario_edad_check`.)

---

**Solución paso a paso:**

```sql
-- 1. Quitar el constraint viejo
ALTER TABLE usuario DROP CONSTRAINT usuario_edad_check;

-- 2. Añadir el nuevo
ALTER TABLE usuario ADD CONSTRAINT usuario_edad_check CHECK (edad >= 13);
```

Si no sabes el nombre del constraint, consúltalo en PostgreSQL así:

```sql
SELECT conname FROM pg_constraint WHERE conrelid = 'usuario'::regclass;
```

**Respuesta final:** secuencia DROP + ADD.

---

# 🔷 BLOQUE H — DML: INSERT, UPDATE, DELETE

---

## Ejercicio H1 — INSERT básico y múltiples filas

**Keywords para buscar:** `INSERT`, `VALUES`, `múltiples filas`, `omitir columnas`, `examen ITAM`, `fácil`

**Tipo de pregunta:** SQL — DML

**Dificultad:** fácil

**Patrones relacionados:**
- INSERT simple, múltiple, con columnas omitidas.

**Trampas típicas:**
- Omitir columnas obligatorias.
- Orden de las columnas vs orden de los valores.

**Enunciado:**
Inserta 3 nuevos propietarios en la tabla. Asume que `id` es SERIAL y `correo` es opcional.

---

**Solución paso a paso:**

```sql
INSERT INTO propietario (nombre, apellido, telefono)
VALUES
  ('Ana', 'García', '5512345678'),
  ('Luis', 'Pérez', '5523456789'),
  ('Marta', 'Ruiz', '5534567890');
```

- Omitir `id` deja que SERIAL asigne automáticamente.
- Omitir `correo` deja NULL (si la columna lo permite).
- El orden en `VALUES` debe coincidir con el orden en `(nombre, apellido, telefono)`.

**Respuesta final:** query arriba.

---

## Ejercicio H2 — INSERT desde SELECT

**Keywords para buscar:** `INSERT INTO ... SELECT`, `copiar datos`, `migrar`, `archivar`, `examen ITAM`, `media`

**Tipo de pregunta:** SQL — DML masiva

**Dificultad:** media

**Patrones relacionados:**
- INSERT desde subquery.
- Archivado de datos antiguos.

**Trampas típicas:**
- No coincidir los tipos.
- Olvidar el WHERE → copiar todo cuando solo querías parte.

**Enunciado:**
Suponiendo que existe la tabla `infraccion_archivada` con la misma estructura que `infraccion`, copia todas las infracciones con fecha anterior al 2020-01-01 a la tabla archivada.

---

**Solución paso a paso:**

```sql
INSERT INTO infraccion_archivada (id, fecha, tipo, importe, vehiculo_id, camara_id)
SELECT id, fecha, tipo, importe, vehiculo_id, camara_id
FROM infraccion
WHERE fecha < '2020-01-01';
```

Si quieres archivar Y borrar de la original (mover):

```sql
BEGIN;

INSERT INTO infraccion_archivada
SELECT * FROM infraccion WHERE fecha < '2020-01-01';

DELETE FROM infraccion WHERE fecha < '2020-01-01';

COMMIT;
```

> ⚠️ Hacerlo en transacción asegura atomicidad: si falla el DELETE, no quedan duplicados.

**Respuesta final:** queries arriba.

---

## Ejercicio H3 — UPDATE con WHERE

**Keywords para buscar:** `UPDATE`, `WHERE`, `condición`, `infracciones masivas`, `examen ITAM`, `fácil`

**Tipo de pregunta:** SQL — DML

**Dificultad:** fácil

**Patrones relacionados:**
- UPDATE filtrado.

**Trampas típicas:**
- Olvidar WHERE → actualiza TODA la tabla. Error catastrófico clásico.

**Enunciado:**
Aumenta en 20% el importe de todas las infracciones de tipo `'velocidad'`.

---

**Solución paso a paso:**

```sql
UPDATE infraccion
SET importe = importe * 1.20
WHERE tipo = 'velocidad';
```

**Buena práctica antes de un UPDATE masivo:**
1. Convertir a SELECT primero para ver qué se afectaría:
   ```sql
   SELECT id, importe, importe * 1.20 AS nuevo_importe
   FROM infraccion WHERE tipo = 'velocidad';
   ```
2. Hacerlo en transacción con ROLLBACK opcional.

**Respuesta final:** query arriba.

---

## Ejercicio H4 — UPDATE correlacionado (estilo Q10 del examen)

**Keywords para buscar:** `UPDATE correlacionado`, `subquery`, `UPDATE FROM`, `propagar valor`, `examen ITAM`, `Q10`, `difícil`

**Tipo de pregunta:** SQL — DML avanzada

**Dificultad:** difícil

**Patrones relacionados:**
- Actualizar columna de tabla A con valor calculado en tabla B.
- Dos sintaxis: subquery correlacionada estándar, o `UPDATE ... FROM` (PostgreSQL).

**Trampas típicas:**
- Olvidar WHERE → todas las filas a NULL si la subquery no encuentra match.
- Subquery devolviendo múltiples filas → error.

**Enunciado:**
Acabas de añadir una columna `total_infracciones INTEGER` a la tabla `vehiculo`. Pueblala con el conteo de infracciones que tiene cada vehículo. Para vehículos sin infracciones, debe quedar 0.

---

**Solución paso a paso:**

Forma estándar (subquery correlacionada):

```sql
UPDATE vehiculo v
SET total_infracciones = (
  SELECT COUNT(*)
  FROM infraccion i
  WHERE i.vehiculo_id = v.id
);
```

- Para vehículos sin infracciones, la subquery devuelve 0 (porque `COUNT(*)` sobre conjunto vacío es 0), así que el COALESCE no es necesario.

Forma PostgreSQL (`UPDATE ... FROM`):

```sql
UPDATE vehiculo v
SET total_infracciones = COALESCE(c.n, 0)
FROM (
  SELECT vehiculo_id, COUNT(*) AS n
  FROM infraccion
  GROUP BY vehiculo_id
) c
WHERE c.vehiculo_id = v.id;
```

⚠️ Cuidado: este segundo formato solo actualiza vehículos que tienen al menos una infracción. Para incluir los demás, hay que hacer dos pasos o usar LEFT JOIN-style con subquery escalar como la primera forma.

**Respuesta final:** ambas queries arriba. Patrón muy estilo Q10 del examen.

---

## Ejercicio H5 — DELETE con subquery

**Keywords para buscar:** `DELETE`, `subquery`, `IN`, `EXISTS`, `examen ITAM`, `media`

**Tipo de pregunta:** SQL — DML con subquery

**Dificultad:** media

**Patrones relacionados:**
- Borrado masivo por condición compleja.

**Trampas típicas:**
- Olvidar WHERE → borra TODO. Error catastrófico.

**Enunciado:**
Borra todas las infracciones de cámaras que ya están inactivas.

---

**Solución paso a paso:**

```sql
DELETE FROM infraccion
WHERE camara_id IN (
  SELECT id FROM camara WHERE activa = FALSE
);
```

O con EXISTS (más NULL-safe):

```sql
DELETE FROM infraccion i
WHERE EXISTS (
  SELECT 1 FROM camara c
  WHERE c.id = i.camara_id AND c.activa = FALSE
);
```

**Respuesta final:** queries arriba.

---

## Ejercicio H6 — Transacción completa con múltiples DML

**Keywords para buscar:** `BEGIN`, `COMMIT`, `ROLLBACK`, `transacción`, `ACID`, `atómica`, `examen ITAM`, `media-difícil`

**Tipo de pregunta:** SQL — control de transacciones

**Dificultad:** media-difícil

**Patrones relacionados:**
- Operaciones que deben ser atómicas (todo o nada).

**Trampas típicas:**
- Olvidar COMMIT → los cambios no se persisten.
- No envolver en transacción cuando es necesario.

**Enunciado:**
Diseña una transacción que:
1. Inserte un nuevo propietario.
2. Inserte un vehículo para ese propietario.
3. Inserte una infracción para ese vehículo.

Si algo falla, todo debe revertirse.

---

**Solución paso a paso:**

```sql
BEGIN;

INSERT INTO propietario (nombre, apellido, telefono)
VALUES ('Juan', 'López', '5511111111')
RETURNING id;
-- Supón que devolvió id = 42

INSERT INTO vehiculo (placa, marca, anio, color, propietario_id)
VALUES ('ABC-123', 'Toyota', 2020, 'rojo', 42)
RETURNING id;
-- Supón que devolvió id = 100

INSERT INTO infraccion (fecha, tipo, importe, vehiculo_id, camara_id)
VALUES ('2024-05-01', 'velocidad', 1500.00, 100, 5);

COMMIT;
-- Si algo falló entre BEGIN y COMMIT, hacer ROLLBACK;
```

**Versión más realista** (usando CTE con RETURNING para no hardcodear IDs):

```sql
BEGIN;

WITH p AS (
  INSERT INTO propietario (nombre, apellido, telefono)
  VALUES ('Juan', 'López', '5511111111')
  RETURNING id
),
v AS (
  INSERT INTO vehiculo (placa, marca, anio, color, propietario_id)
  SELECT 'ABC-123', 'Toyota', 2020, 'rojo', id FROM p
  RETURNING id
)
INSERT INTO infraccion (fecha, tipo, importe, vehiculo_id, camara_id)
SELECT '2024-05-01', 'velocidad', 1500.00, id, 5 FROM v;

COMMIT;
```

**Respuesta final:** ambas queries arriba.

---

## Ejercicio H7 — DELETE con CASCADE: efectos invisibles

**Keywords para buscar:** `DELETE`, `CASCADE`, `efecto en cadena`, `borrado masivo`, `examen ITAM`, `difícil`, `trampa`

**Tipo de pregunta:** SQL — análisis de efectos

**Dificultad:** difícil

**Patrones relacionados:**
- Comprender cómo CASCADE propaga deletes a través del esquema.

**Trampas típicas:**
- Subestimar cuánto se borra.

**Enunciado:**
Supón que el ERD de Fotomultas está configurado así:
- `infraccion.vehiculo_id` → `vehiculo(id)` ON DELETE CASCADE
- `infraccion.camara_id` → `camara(id)` ON DELETE RESTRICT
- `pago.infraccion_id` → `infraccion(id)` ON DELETE CASCADE

Si ejecutas `DELETE FROM vehiculo WHERE id = 5`, donde el vehículo 5 tiene 10 infracciones y cada una tiene 1 pago, ¿qué pasa?

---

**Solución paso a paso:**

1. `DELETE FROM vehiculo WHERE id = 5` → intenta borrar el vehículo.
2. Por CASCADE en `infraccion.vehiculo_id`, las 10 infracciones del vehículo 5 se marcan para borrado.
3. Por CASCADE en `pago.infraccion_id`, cada pago de esas 10 infracciones también se borra.
4. La restricción RESTRICT en `infraccion.camara_id` **no se viola** porque las cámaras no se están borrando — solo se borran las infracciones que las referencian (eso está permitido).
5. **Resultado total:** 1 vehículo + 10 infracciones + 10 pagos eliminados (total 21 filas).

**Lección:** las cascadas pueden generar borrados masivos transitivos sorprendentes. Por eso muchas DBs prefieren `ON DELETE RESTRICT` por defecto y obligan a borrar explícitamente en orden.

**Respuesta final:** se borran 21 filas en total (1 vehículo, 10 infracciones, 10 pagos).

---

# 🔷 BLOQUE I — Normalización, DFs y DMVs

---

## Ejercicio I1 — Identificar anomalías en tabla denormalizada

**Keywords para buscar:** `anomalía`, `inserción`, `actualización`, `borrado`, `denormalizada`, `normalización`, `motivación`, `examen ITAM`, `fácil-media`

**Tipo de pregunta:** conceptual / análisis

**Dificultad:** fácil-media

**Patrones relacionados:**
- Detectar problemas en una tabla no normalizada.

**Trampas típicas:**
- Confundir el tipo de anomalía.

**Enunciado:**
Dada la siguiente tabla `cliente_pedido(cliente_id, cliente_nombre, cliente_email, pedido_id, fecha, total)`, donde un cliente puede tener muchos pedidos:

| cliente_id | cliente_nombre | cliente_email | pedido_id | fecha | total |
|---|---|---|---|---|---|
| 1 | Ana | ana@x.com | 100 | 2024-01-01 | 500 |
| 1 | Ana | ana@x.com | 101 | 2024-02-15 | 700 |
| 2 | Luis | luis@x.com | 102 | 2024-01-10 | 300 |

Identifica los 3 tipos de anomalías que sufre.

---

**Solución paso a paso:**

1. **Anomalía de actualización:** si Ana cambia su correo, hay que actualizar **todas** las filas donde aparece. Si actualizo solo una, queda inconsistente.

2. **Anomalía de inserción:** no puedo registrar un nuevo cliente sin que tenga al menos un pedido. Tendría que poner NULL en `pedido_id`, `fecha`, `total`.

3. **Anomalía de borrado:** si Luis solo tiene un pedido y lo cancelo (borro la fila), **pierdo también** los datos del cliente Luis.

Causa raíz: hay dos entidades distintas mezcladas en una sola tabla. La descomposición correcta es:
- `cliente(id, nombre, email)`
- `pedido(id, fecha, total, cliente_id FK)`

**Respuesta final:** las tres anomalías arriba, con descomposición correcta.

---

## Ejercicio I2 — Calcular cierre de atributos

**Keywords para buscar:** `cierre de atributos`, `cierre`, `closure`, `X+`, `Armstrong`, `DF`, `normalización`, `examen ITAM`, `media`, `teórico`

**Tipo de pregunta:** teórico — normalización

**Dificultad:** media

**Patrones relacionados:**
- Algoritmo de cierre.
- Determinar llaves a partir de DFs.

**Trampas típicas:**
- Saltarse iteraciones.
- No aplicar todas las DFs en cada paso.

**Enunciado:**
Sea la relación R(A, B, C, D, E) con DFs:
- A → B
- B → C
- CD → E

Calcula el cierre de {A, D} y determina si es una superllave.

---

**Solución paso a paso:**

Cierre = {A, D} inicialmente.

Iteración 1:
- `A → B`: A está en el cierre → agregamos B. Cierre = {A, B, D}.

Iteración 2:
- `B → C`: B está en el cierre → agregamos C. Cierre = {A, B, C, D}.

Iteración 3:
- `CD → E`: C y D ambos en el cierre → agregamos E. Cierre = {A, B, C, D, E}.

Iteración 4:
- No se puede agregar nada nuevo. STOP.

Cierre de {A, D} = {A, B, C, D, E} = todos los atributos de R.

**Conclusión:** {A, D} **es** una superllave. Y como ningún subconjunto propio ({A} o {D} solos) genera todos los atributos, es **llave** (mínima superllave).

**Respuesta final:** {A, D}+ = {A, B, C, D, E}, es llave.

---

## Ejercicio I3 — Determinar si una relación está en FNBC

**Keywords para buscar:** `FNBC`, `Boyce-Codd`, `BCNF`, `superllave`, `lado izquierdo de DF`, `examen ITAM`, `difícil`

**Tipo de pregunta:** teórico — normalización

**Dificultad:** difícil

**Patrones relacionados:**
- Verificar FNBC: toda DF no trivial X → Y tiene X superllave.

**Trampas típicas:**
- Olvidar verificar si la DF es trivial primero.

**Enunciado:**
Sea R(A, B, C, D) con DFs:
- A → B
- AC → D

¿Está en FNBC?

---

**Solución paso a paso:**

Paso 1: encontrar todas las llaves.

- {A, C}+: A → B agrega B; AC → D agrega D. Cierre = {A, B, C, D}. AC es superllave. ¿Es mínima? {A}+ = {A, B}; {C}+ = {C}. Ni A ni C solos son superllave. Entonces AC es **llave**.
- Buscar otras llaves: no las hay (B y D son sólo dependientes; nunca aparecen en lado izquierdo).

Única llave: {A, C}.

Paso 2: para cada DF no trivial, verificar si su lado izquierdo es superllave.

- `A → B`: B ⊄ A (no trivial). ¿A es superllave? {A}+ = {A, B} ≠ R. **A NO es superllave**. → Viola FNBC.
- `AC → D`: AC es la llave → es superllave. OK.

**Conclusión:** R **no** está en FNBC porque `A → B` tiene A no superllave.

**Descomposición FNBC:**
- R1(A, B) con DF A → B (en FNBC porque A es llave allí).
- R2(A, C, D) con DF AC → D (en FNBC porque AC es llave).

**Respuesta final:** no está en FNBC; descomposición arriba.

---

## Ejercicio I4 — Trivialidad de DF (estilo Q5 examen YouTube)

**Keywords para buscar:** `trivialidad`, `DF trivial`, `Y subconjunto X`, `definición formal`, `examen ITAM`, `Q5`, `fácil`, `teórico`

**Tipo de pregunta:** conceptual exacto

**Dificultad:** fácil (si conoces la definición)

**Patrones relacionados:**
- Trivialidad: Y ⊆ X.

**Trampas típicas:**
- Confundir trivialidad de DMV (que es distinta).

**Enunciado:**
Sean los atributos {Z, A, B, C} en una relación R. Determina si cada DF es trivial:
1. ZA → A
2. ZA → AB
3. ZAB → ZA
4. Z → A

---

**Solución paso a paso:**

Definición: X → Y es trivial sii Y ⊆ X.

1. `ZA → A`: ¿A ⊆ ZA? Sí. **Trivial.**
2. `ZA → AB`: ¿AB ⊆ ZA? AB tiene B; ZA no tiene B. **No trivial.**
3. `ZAB → ZA`: ¿ZA ⊆ ZAB? Sí. **Trivial.**
4. `Z → A`: ¿A ⊆ Z? No. **No trivial.**

**Respuesta final:** 1 y 3 son triviales; 2 y 4 no.

---

## Ejercicio I5 — Trivialidad de DMV (estilo Q5 examen YouTube)

**Keywords para buscar:** `DMV trivial`, `dependencia multivaluada`, `Y subconjunto X o XY = E`, `4FN`, `Fagin`, `examen ITAM`, `Q5`, `media`, `teórico`

**Tipo de pregunta:** conceptual exacto

**Dificultad:** media (porque la definición de trivialidad de DMV es menos intuitiva)

**Patrones relacionados:**
- Trivialidad DMV: Y ⊆ X **o** X ∪ Y = E (todos los atributos).

**Trampas típicas:**
- Aplicar la trivialidad de DF a DMVs.

**Enunciado:**
Sea R(A, B, C, D) (E = {A, B, C, D}). Determina si cada DMV es trivial:
1. AB →→ B
2. AB →→ CD
3. A →→ BC
4. AB →→ CDA

---

**Solución paso a paso:**

Definición: X →→ Y es trivial sii Y ⊆ X **o** X ∪ Y = E.

1. `AB →→ B`: ¿B ⊆ AB? Sí. **Trivial.**
2. `AB →→ CD`: ¿CD ⊆ AB? No. ¿AB ∪ CD = {A,B,C,D} = E? Sí. **Trivial.**
3. `A →→ BC`: ¿BC ⊆ A? No. ¿A ∪ BC = {A,B,C} ≠ E? D falta. **No trivial.**
4. `AB →→ CDA`: ¿CDA ⊆ AB? No. ¿AB ∪ CDA = {A,B,C,D} = E? Sí. **Trivial.**

**Respuesta final:** 1, 2, 4 triviales; 3 no.

---

## Ejercicio I6 — ¿Se mantiene 4FN al añadir un atributo? (estilo Q3 examen)

**Keywords para buscar:** `4FN`, `mantener forma normal`, `agregar atributo`, `uuid`, `unicidad por fila`, `Fagin`, `examen ITAM`, `Q3`, `MUY difícil`, `teórico`

**Tipo de pregunta:** análisis teórico

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Razonar sobre cómo añadir/quitar columnas afecta las FN.

**Trampas típicas:**
- Confundir si añadir una columna única conserva 4FN o no.

**Enunciado:**
La tabla `video(id, titulo, descripcion, fecha)` está en 4FN. Se decide añadir la columna `uuid VARCHAR(36) NOT NULL UNIQUE` (un identificador único alternativo, distinto del `id` PK pero también único). ¿Se mantiene la 4FN?

---

**Solución paso a paso:**

**Razonamiento:**

4FN requiere: para toda DMV no trivial X →→ Y, X debe ser superllave.

Antes del cambio:
- La tabla está en 4FN.
- `id` es PK → superllave.

Después de añadir `uuid UNIQUE NOT NULL`:
- `uuid` ahora es también superllave (porque es UNIQUE y NOT NULL → identifica unívocamente).
- Cualquier DF/DMV en la que `uuid` o `id` aparezcan del lado izquierdo, tienen superllave → ok.
- Las DFs/DMVs **anteriores** siguen siendo las mismas, ya que `uuid` no introduce nuevas dependencias multivaluadas (es solo otro identificador único).

**Conclusión:** sí se mantiene 4FN. Añadir una columna **UNIQUE NOT NULL** que no introduce nuevas DMVs no degrada la forma normal — más aún, refuerza la estructura porque crea una superllave adicional.

> ⚠️ Distinción importante: si en lugar de `uuid UNIQUE` añadieras un atributo multivaluado (por ejemplo, una lista de tags), entonces introducirías una DMV nueva `id →→ tag` que podría violar 4FN.

**Respuesta final:** sí se mantiene 4FN; razonamiento arriba.

---

## Ejercicio I7 — Descomposición sin pérdida (Heath)

**Keywords para buscar:** `descomposición sin pérdida`, `Heath`, `unión natural`, `JOIN reversibilidad`, `examen ITAM`, `difícil`, `teórico`

**Tipo de pregunta:** teórico — normalización

**Dificultad:** difícil

**Patrones relacionados:**
- Teorema de Heath: si X → Y y X ∩ Y = ∅, entonces R = R[X∪Y] ⋈ R[X∪Z] (donde Z son los demás atributos).

**Trampas típicas:**
- Olvidar que la intersección de los esquemas descompuestos debe ser una llave de al menos uno.

**Enunciado:**
Dada R(A, B, C, D) con DFs `A → B` y `A → C`. Descomponer en dos relaciones manteniendo la descomposición sin pérdida y justificar.

---

**Solución paso a paso:**

DFs conocidas: `A → B`, `A → C` → equivalente a `A → BC`.

Aplicando Heath con X = {A}, Y = {B, C}, Z = {D}:

- R1 = R[A, B, C] (los atributos del lado izquierdo + derecho de la DF que aplicamos).
- R2 = R[A, D] (atributos restantes + el lado izquierdo).

**Verificación de Heath:**
- R1 ∩ R2 = {A}.
- A es superllave de R1 (porque A → BC).
- Por Heath, la descomposición es sin pérdida: R1 ⋈ R2 = R.

**Respuesta final:** R1(A, B, C), R2(A, D). Sin pérdida por Heath porque A es llave en R1.

---

## Ejercicio I8 — Cuál forma normal se viola (caso paso a paso)

**Keywords para buscar:** `forma normal`, `1FN`, `2FN`, `3FN`, `FNBC`, `identificar violación`, `examen ITAM`, `difícil`, `teórico`

**Tipo de pregunta:** análisis paso a paso

**Dificultad:** difícil

**Patrones relacionados:**
- Diagnóstico de FN actual de una relación.

**Trampas típicas:**
- Saltarse 2FN y 3FN.

**Enunciado:**
Sea `R(estudiante_id, curso_id, nombre_estudiante, profesor, departamento_profesor)` con DFs:
- {estudiante_id, curso_id} → profesor
- estudiante_id → nombre_estudiante
- profesor → departamento_profesor

Llave: {estudiante_id, curso_id}. ¿En qué forma normal está?

---

**Solución paso a paso:**

**1FN:** todas las columnas atómicas. Asumimos que sí.

**2FN:** todo atributo no primo depende totalmente de la llave (no de una parte).
- `nombre_estudiante` depende de `estudiante_id` (parte de la llave). **DF parcial** → viola 2FN.

Conclusión: la relación está solo en 1FN.

**Cómo arreglar:**
- R1(estudiante_id, nombre_estudiante)
- R2(estudiante_id, curso_id, profesor)
- Si `profesor → departamento_profesor` (DF transitiva), aún viola 3FN en R2, así que:
- R3(profesor, departamento_profesor)
- R2'(estudiante_id, curso_id, profesor)
- R1(estudiante_id, nombre_estudiante)

Resultado: 3 tablas en FNBC.

**Respuesta final:** está en 1FN (viola 2FN). Descomposición arriba.

---

# 🔷 BLOQUE J — Debugging y preguntas tramposas

---

## Ejercicio J1 — COUNT(*) vs COUNT(col) en LEFT JOIN

**Keywords para buscar:** `COUNT estrella vs columna`, `LEFT JOIN`, `NULL`, `trampa`, `aggregation`, `debugging`, `examen ITAM`, `media`, `Q3 estilo`

**Tipo de pregunta:** debugging

**Dificultad:** media

**Patrones relacionados:**
- COUNT(*) cuenta filas; COUNT(col) ignora NULLs.

**Trampas típicas:**
- Esperar 0 con COUNT(*) cuando se obtiene 1.

**Enunciado:**
Esta query intenta contar cuántas infracciones tiene cada vehículo. ¿Por qué los vehículos sin infracciones devuelven 1 en vez de 0?

```sql
SELECT v.id, v.placa, COUNT(*) AS n
FROM vehiculo v
LEFT JOIN infraccion i ON i.vehiculo_id = v.id
GROUP BY v.id, v.placa;
```

---

**Solución paso a paso:**

- `COUNT(*)` cuenta **filas**, no valores.
- Para un vehículo sin infracciones, el LEFT JOIN produce 1 fila con todos los campos de `infraccion` en NULL.
- Esa fila se cuenta → resultado 1.

**Corrección:** usar `COUNT(i.id)` que ignora NULLs:

```sql
SELECT v.id, v.placa, COUNT(i.id) AS n
FROM vehiculo v
LEFT JOIN infraccion i ON i.vehiculo_id = v.id
GROUP BY v.id, v.placa;
```

Para los vehículos sin infracciones, `i.id` es NULL → `COUNT(i.id) = 0`.

**Respuesta final:** porque `COUNT(*)` cuenta filas (incluida la fila con NULLs del LEFT JOIN). Solución: `COUNT(i.id)`.

---

## Ejercicio J2 — NOT IN con NULLs

**Keywords para buscar:** `NOT IN`, `NULL`, `UNKNOWN`, `lógica trivalente`, `debugging`, `trampa`, `examen ITAM`, `difícil`

**Tipo de pregunta:** debugging

**Dificultad:** difícil

**Patrones relacionados:**
- Comportamiento de NOT IN con NULL.

**Trampas típicas:**
- Esperar resultados y obtener vacío.

**Enunciado:**
Esta query intenta listar vehículos sin propietario (donde `propietario_id` no coincide con ningún propietario). Devuelve resultado vacío aun cuando hay vehículos huérfanos. ¿Por qué?

```sql
SELECT * FROM vehiculo
WHERE propietario_id NOT IN (SELECT id FROM propietario);
```

Sabes que la tabla `propietario` tiene una fila con `id = NULL`.

---

**Solución paso a paso:**

- `NOT IN (lista)` se evalúa como `propietario_id <> x1 AND propietario_id <> x2 AND ...`.
- Si la lista contiene NULL: `propietario_id <> NULL` da **UNKNOWN**.
- En lógica trivalente, `algo AND UNKNOWN = UNKNOWN`.
- En el WHERE, UNKNOWN se trata como FALSE → ninguna fila pasa.

**Solución 1:** filtrar NULLs:

```sql
WHERE propietario_id NOT IN (SELECT id FROM propietario WHERE id IS NOT NULL);
```

**Solución 2 (preferida):** usar NOT EXISTS:

```sql
WHERE NOT EXISTS (
  SELECT 1 FROM propietario p WHERE p.id = vehiculo.propietario_id
);
```

`NOT EXISTS` es NULL-safe.

**Respuesta final:** porque la subquery devuelve un NULL y eso envenena la comparación con UNKNOWN. Usar `NOT EXISTS` o filtrar NULL.

---

## Ejercicio J3 — GROUP BY con columna no agregada

**Keywords para buscar:** `GROUP BY`, `columna no agregada`, `error`, `SELECT lista`, `debugging`, `examen ITAM`, `fácil-media`

**Tipo de pregunta:** debugging

**Dificultad:** fácil-media

**Patrones relacionados:**
- Regla estricta: cada columna del SELECT debe estar en GROUP BY o ser argumento de agregación.

**Trampas típicas:**
- En MySQL clásico el error se silenciaba; en PostgreSQL estándar siempre falla.

**Enunciado:**
Esta query falla. ¿Por qué? ¿Cómo arreglarla?

```sql
SELECT v.propietario_id, v.placa, COUNT(*) AS n
FROM vehiculo v
JOIN infraccion i ON i.vehiculo_id = v.id
GROUP BY v.propietario_id;
```

---

**Solución paso a paso:**

`v.placa` no está en `GROUP BY` ni dentro de una agregación. La base no sabe qué placa devolver si hay varios vehículos por propietario.

**Opciones de corrección:**

A) Agregar `v.placa` al GROUP BY (pero entonces se agrupará por propietario + placa, lo que cambia el significado):

```sql
GROUP BY v.propietario_id, v.placa;
```

B) Aplicar agregación a `v.placa`:

```sql
SELECT v.propietario_id, MIN(v.placa), COUNT(*) FROM ...
GROUP BY v.propietario_id;
```

C) Si lo que querías era conteo por propietario sin mostrar placa: quitar `v.placa` del SELECT.

**Respuesta final:** error porque `v.placa` no está agrupada. Decidir qué se quiere realmente y aplicar A, B o C.

---

## Ejercicio J4 — WHERE vs HAVING confundidos

**Keywords para buscar:** `WHERE vs HAVING`, `error`, `agregación en WHERE`, `debugging`, `examen ITAM`, `media`, `trampa`

**Tipo de pregunta:** debugging

**Dificultad:** media

**Patrones relacionados:**
- Agregaciones van en HAVING, no en WHERE.

**Trampas típicas:**
- Pensar que WHERE funciona con agregaciones.

**Enunciado:**
Esta query da error. ¿Por qué?

```sql
SELECT alcaldia, COUNT(*) AS n
FROM camara
WHERE COUNT(*) > 10
GROUP BY alcaldia;
```

---

**Solución paso a paso:**

- `COUNT(*) > 10` en el WHERE: error. WHERE se evalúa antes del GROUP BY, así que las agregaciones no existen todavía.

**Corrección:**

```sql
SELECT alcaldia, COUNT(*) AS n
FROM camara
GROUP BY alcaldia
HAVING COUNT(*) > 10;
```

**Regla mental:** WHERE filtra filas individuales; HAVING filtra grupos ya formados.

**Respuesta final:** corrección arriba.

---

## Ejercicio J5 — UNIQUE con NULL

**Keywords para buscar:** `UNIQUE`, `NULL`, `múltiples NULLs permitidos`, `constraint`, `debugging`, `trampa`, `examen ITAM`, `media`

**Tipo de pregunta:** debugging conceptual

**Dificultad:** media

**Patrones relacionados:**
- Comportamiento de UNIQUE ante NULLs en SQL estándar.

**Trampas típicas:**
- Pensar que UNIQUE prohíbe múltiples NULLs.

**Enunciado:**
La tabla `propietario` tiene `correo VARCHAR UNIQUE`. Se insertan estas filas:
1. (1, 'Ana', 'ana@x.com')
2. (2, 'Luis', NULL)
3. (3, 'Marta', NULL)
4. (4, 'Pepe', 'ana@x.com')

¿Cuáles insertan correctamente?

---

**Solución paso a paso:**

- Fila 1: inserta OK.
- Fila 2: inserta OK (NULL ≠ ningún valor concreto).
- Fila 3: **inserta OK** (sorprendentemente). En SQL estándar y PostgreSQL, `NULL` no se considera "igual" a otro `NULL` para efectos de UNIQUE. Se permiten múltiples NULLs.
- Fila 4: **FALLA** porque ya existe 'ana@x.com'.

> ⚠️ Excepción: SQL Server trata UNIQUE de forma distinta (solo permite un NULL). Pero en PostgreSQL, Oracle y SQL estándar, se permiten múltiples NULLs.

Si quieres prohibir múltiples NULLs, agrega NOT NULL al campo o usa un índice único filtrado:
```sql
CREATE UNIQUE INDEX ON propietario (correo) WHERE correo IS NOT NULL; -- esto es lo default
```

**Respuesta final:** filas 1, 2, 3 OK; fila 4 falla.

---

## Ejercicio J6 — Resultado inesperado por orden de columnas en GROUP BY

**Keywords para buscar:** `GROUP BY`, `múltiples columnas`, `cardinalidad de grupos`, `debugging`, `trampa`, `examen ITAM`, `media`

**Tipo de pregunta:** debugging conceptual

**Dificultad:** media

**Patrones relacionados:**
- GROUP BY (A, B) crea un grupo por cada par único de (A, B).

**Trampas típicas:**
- Esperar grupos por A solamente.

**Enunciado:**
La siguiente query intenta contar cuántas infracciones tiene cada tipo. Da más filas de las esperadas. ¿Por qué?

```sql
SELECT tipo, fecha, COUNT(*)
FROM infraccion
GROUP BY tipo, fecha;
```

---

**Solución paso a paso:**

- `GROUP BY tipo, fecha` crea un grupo por cada combinación única de tipo + fecha.
- Si hay 5 tipos y 100 fechas distintas, puede haber hasta 500 grupos en lugar de 5.

**Corrección:** quitar `fecha` del GROUP BY si solo quieres agrupar por tipo:

```sql
SELECT tipo, COUNT(*)
FROM infraccion
GROUP BY tipo;
```

**Respuesta final:** porque agrupar por más columnas refina los grupos. Quitar fecha.

---

## Ejercicio J7 — DISTINCT después de COUNT

**Keywords para buscar:** `DISTINCT`, `COUNT DISTINCT`, `duplicados`, `aggregation`, `debugging`, `trampa`, `examen ITAM`, `fácil-media`

**Tipo de pregunta:** debugging

**Dificultad:** fácil-media

**Patrones relacionados:**
- COUNT(DISTINCT col) vs COUNT(col).

**Trampas típicas:**
- Pensar que SELECT DISTINCT corrige.

**Enunciado:**
Quiero saber cuántos propietarios distintos han recibido al menos una infracción. Mi query:

```sql
SELECT COUNT(DISTINCT v.propietario_id)
FROM vehiculo v
JOIN infraccion i ON i.vehiculo_id = v.id;
```

Un compañero me dice que debe ser:

```sql
SELECT DISTINCT COUNT(v.propietario_id)
FROM vehiculo v
JOIN infraccion i ON i.vehiculo_id = v.id;
```

¿Quién tiene razón?

---

**Solución paso a paso:**

- La primera (yo) cuenta cuántos valores **distintos** de `propietario_id` hay después del JOIN → correcto.
- La segunda (compañero) primero cuenta TODOS los propietario_id (con duplicados), devuelve un número, y `DISTINCT` sobre un único número es trivialmente ese número → es lo mismo que `COUNT(...)` sin DISTINCT, no resuelve duplicados.

**Respuesta final:** la primera es correcta. `DISTINCT` debe ir **dentro** del COUNT.

---

# 🔷 BLOQUE K — MUY difíciles estilo final ITAM

---

## Ejercicio K1 — Normalizar tabla denormalizada paso a paso hasta FNBC

**Keywords para buscar:** `normalización`, `1FN a FNBC`, `descomposición paso a paso`, `DF`, `transitividad`, `examen ITAM`, `MUY difícil`, `teórico extenso`

**Tipo de pregunta:** análisis completo

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Aplicar todas las FN en secuencia.

**Trampas típicas:**
- Saltarse 2FN.
- No detectar dependencia transitiva.

**Enunciado:**
Dada la siguiente tabla:

`pedido(pedido_id, cliente_id, cliente_nombre, cliente_ciudad, codigo_ciudad, producto_id, producto_nombre, cantidad, fecha_pedido)`

Con DFs:
- pedido_id → cliente_id, fecha_pedido
- cliente_id → cliente_nombre, cliente_ciudad
- cliente_ciudad → codigo_ciudad
- producto_id → producto_nombre
- {pedido_id, producto_id} → cantidad

Normalízala a FNBC paso a paso.

---

**Solución paso a paso:**

**Paso 0 - Llave:** {pedido_id, producto_id}. Verificación con cierre:
- {pedido_id, producto_id}+ incluye pedido_id → cliente_id, fecha; cliente_id → cliente_nombre, cliente_ciudad; cliente_ciudad → codigo_ciudad; producto_id → producto_nombre; {pedido_id,producto_id}→cantidad. Cierre = todos. OK.

**Paso 1 - 1FN:** asumimos atomicidad. OK.

**Paso 2 - 2FN:** atributos no primos que dependen de parte de la llave.
- `pedido_id → cliente_id, fecha_pedido` → cliente_id, fecha_pedido dependen solo de pedido_id (parte de la llave). Violación.
- `producto_id → producto_nombre` → viola 2FN.
- `cliente_nombre, cliente_ciudad, codigo_ciudad` dependen transitivamente, también violan.

Descomposición a 2FN:
- R1(pedido_id, cliente_id, fecha_pedido, cliente_nombre, cliente_ciudad, codigo_ciudad)
- R2(producto_id, producto_nombre)
- R3(pedido_id, producto_id, cantidad)

**Paso 3 - 3FN sobre R1:** ¿hay transitividad?
- pedido_id → cliente_id → cliente_nombre, cliente_ciudad. Transitiva → viola 3FN.
- cliente_ciudad → codigo_ciudad. Transitiva → viola 3FN.

Descomposición a 3FN:
- R1a(pedido_id, cliente_id, fecha_pedido)
- R1b(cliente_id, cliente_nombre, cliente_ciudad)
- R1c(cliente_ciudad, codigo_ciudad)
- R2(producto_id, producto_nombre)
- R3(pedido_id, producto_id, cantidad)

**Paso 4 - FNBC:** verificar que toda DF no trivial X → Y tiene X superllave.
- R1a: llave = pedido_id. DF pedido_id → cliente_id, fecha. Pedido_id superllave. ✓
- R1b: llave = cliente_id. DF cliente_id → nombre, ciudad. ✓
- R1c: llave = cliente_ciudad. DF cliente_ciudad → codigo_ciudad. ✓
- R2: llave = producto_id. DF producto_id → producto_nombre. ✓
- R3: llave = {pedido_id, producto_id}. DF {pedido_id, producto_id} → cantidad. ✓

Todas en FNBC.

**Respuesta final:** 5 relaciones descompuestas arriba.

---

## Ejercicio K2 — Query brutal: top 3 propietarios por alcaldía con detalle

**Keywords para buscar:** `top N por grupo`, `window function`, `múltiples JOIN`, `CTE`, `RANK`, `examen ITAM`, `MUY difícil`, `Fotomultas`

**Tipo de pregunta:** SQL complejo

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Combinación de joins multi-tabla + window + filtro.

**Trampas típicas:**
- Olvidar el `PARTITION BY` adecuado.
- Mezclar la alcaldía del vehículo con la de la cámara.

**Enunciado:**
Para cada alcaldía donde han ocurrido infracciones, lista los 3 propietarios con más infracciones cometidas en esa alcaldía. Incluye: alcaldía, posición (1, 2 o 3), nombre del propietario, número de infracciones e importe total acumulado.

---

**Solución paso a paso:**

```sql
WITH infracciones_por_alc_prop AS (
  SELECT c.alcaldia,
         v.propietario_id,
         COUNT(*) AS n_infracciones,
         SUM(i.importe) AS total_importe
  FROM camara c
  JOIN infraccion i ON i.camara_id = c.id
  JOIN vehiculo v ON v.id = i.vehiculo_id
  GROUP BY c.alcaldia, v.propietario_id
),
con_ranking AS (
  SELECT alcaldia, propietario_id, n_infracciones, total_importe,
         RANK() OVER (PARTITION BY alcaldia ORDER BY n_infracciones DESC) AS posicion
  FROM infracciones_por_alc_prop
)
SELECT r.alcaldia,
       r.posicion,
       p.nombre,
       p.apellido,
       r.n_infracciones,
       r.total_importe
FROM con_ranking r
JOIN propietario p ON p.id = r.propietario_id
WHERE r.posicion <= 3
ORDER BY r.alcaldia, r.posicion;
```

**Razonamiento:**
1. CTE1: agregar conteo + importe por (alcaldía, propietario), uniendo tres tablas.
2. CTE2: calcular ranking dentro de cada alcaldía con `RANK() PARTITION BY alcaldia`.
3. Filtrar top 3 y unir con `propietario` para obtener nombres.

**Variantes:**
- Para evitar empates en la posición 3, usar `ROW_NUMBER()` en lugar de `RANK()`.
- Para incluir alcaldías sin infracciones, hacer LEFT JOIN desde una tabla maestra de alcaldías (no la tenemos aquí).

**Respuesta final:** query arriba.

---

## Ejercicio K3 — Diferencia porcentual mes a mes con window

**Keywords para buscar:** `LAG`, `porcentaje variación`, `mes a mes`, `serie temporal`, `window function`, `examen ITAM`, `MUY difícil`

**Tipo de pregunta:** SQL avanzado

**Dificultad:** MUY difícil

**Patrones relacionados:**
- LAG combinado con cálculo de porcentaje.
- Manejo de NULL en la primera fila.

**Trampas típicas:**
- División por cero.
- LAG sobre datos no truncados.

**Enunciado:**
Para cada mes calendárico, calcula la variación porcentual del número de infracciones respecto al mes anterior. Si es el primer mes registrado, muestra NULL.

---

**Solución paso a paso:**

```sql
WITH por_mes AS (
  SELECT DATE_TRUNC('month', fecha) AS mes,
         COUNT(*) AS n
  FROM infraccion
  GROUP BY DATE_TRUNC('month', fecha)
)
SELECT mes,
       n,
       LAG(n) OVER (ORDER BY mes) AS n_mes_anterior,
       ROUND(
         (n - LAG(n) OVER (ORDER BY mes)) * 100.0
         / NULLIF(LAG(n) OVER (ORDER BY mes), 0),
         2
       ) AS variacion_porcentual
FROM por_mes
ORDER BY mes;
```

- `NULLIF(LAG(n) OVER (ORDER BY mes), 0)` evita división por cero.
- Para la primera fila, `LAG` es NULL → la división es NULL → `variacion_porcentual` será NULL. Correcto.

**Respuesta final:** query arriba.

---

## Ejercicio K4 — Detectar inconsistencia: pago > infracción

**Keywords para buscar:** `JOIN`, `validación`, `pago vs infracción`, `detectar errores`, `debugging`, `examen ITAM`, `difícil`

**Tipo de pregunta:** SQL — análisis de integridad

**Dificultad:** difícil

**Patrones relacionados:**
- Comparar pagos sumados vs importe de la infracción.

**Trampas típicas:**
- Olvidar agrupar por infracción.
- No considerar infracciones con 0 pagos (LEFT JOIN para incluirlas).

**Enunciado:**
Encuentra todas las infracciones donde la suma de los pagos asociados **supera** el importe original de la infracción.

---

**Solución paso a paso:**

```sql
SELECT i.id,
       i.importe AS importe_original,
       COALESCE(SUM(p.importe), 0) AS total_pagado
FROM infraccion i
LEFT JOIN pago p ON p.infraccion_id = i.id
GROUP BY i.id, i.importe
HAVING COALESCE(SUM(p.importe), 0) > i.importe;
```

**Variante** (excluyendo infracciones sin pagos):

```sql
SELECT i.id, i.importe, SUM(p.importe) AS total_pagado
FROM infraccion i
JOIN pago p ON p.infraccion_id = i.id
GROUP BY i.id, i.importe
HAVING SUM(p.importe) > i.importe;
```

**Respuesta final:** query arriba.

---

## Ejercicio K5 — Transacción con múltiples ALTER + UPDATE (estilo Q10 examen)

**Keywords para buscar:** `BEGIN`, `ALTER TABLE`, `UPDATE`, `transacción`, `migración`, `examen ITAM`, `Q10`, `MUY difícil`

**Tipo de pregunta:** SQL — migración transaccional

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Combinar DDL + DML en una transacción.

**Trampas típicas:**
- Asumir que DDL es transaccional en todos los motores (sí en PostgreSQL).
- Orden incorrecto de pasos.

**Enunciado:**
Quieres añadir a la tabla `propietario` una columna `total_pagado NUMERIC(12,2) NOT NULL DEFAULT 0` que represente la suma de pagos que ha hecho el propietario. Diseña una migración transaccional que:
1. Añada la columna.
2. La pueble con la suma real desde la tabla `pago`.
3. Sea atómica (si algo falla, todo se revierte).

---

**Solución paso a paso:**

```sql
BEGIN;

-- 1. Añadir columna (con default 0 para filas existentes)
ALTER TABLE propietario
ADD COLUMN total_pagado NUMERIC(12,2) NOT NULL DEFAULT 0;

-- 2. Poblar con suma real
UPDATE propietario p
SET total_pagado = COALESCE(s.total, 0)
FROM (
  SELECT acreedor_id, SUM(importe) AS total
  FROM pago
  GROUP BY acreedor_id
) s
WHERE s.acreedor_id = p.id;

-- (Verificación opcional antes de COMMIT)
-- SELECT COUNT(*) FROM propietario WHERE total_pagado IS NULL;  -- debería ser 0

COMMIT;
```

**Notas clave:**
- En PostgreSQL, DDL es transaccional → el ALTER se revierte si hay ROLLBACK.
- El `DEFAULT 0` puebla todas las filas existentes con 0; el UPDATE las corrige con la suma real.
- Si hubiera un error en el UPDATE (por ejemplo un tipo incompatible), el ALTER se deshace también.

**Respuesta final:** transacción arriba.

---

## Ejercicio K6 — Análisis combinado: query que requiere 5 conceptos

**Keywords para buscar:** `query compleja`, `CTE`, `LEFT JOIN`, `window function`, `subquery`, `HAVING`, `examen ITAM`, `MUY difícil`, `final`

**Tipo de pregunta:** SQL master

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Múltiples conceptos en una sola query.

**Trampas típicas:**
- Cualquiera de las anteriores.

**Enunciado:**
Lista las alcaldías que cumplen TODAS estas condiciones:
1. Tienen al menos 5 cámaras activas.
2. Han recaudado en pagos al menos 100,000 MXN en el último año.
3. El propietario top 1 en infracciones de esa alcaldía es distinto del top 1 en pagos de esa alcaldía.

Devuelve: alcaldía, número de cámaras activas, total recaudado, nombre del propietario top 1 en infracciones, nombre del propietario top 1 en pagos.

---

**Solución paso a paso:**

```sql
WITH camaras_activas AS (
  SELECT alcaldia, COUNT(*) AS n_activas
  FROM camara
  WHERE activa = TRUE
  GROUP BY alcaldia
  HAVING COUNT(*) >= 5
),
pagos_ultimo_anio AS (
  SELECT c.alcaldia, SUM(pg.importe) AS total_pagado
  FROM camara c
  JOIN infraccion i ON i.camara_id = c.id
  JOIN pago pg ON pg.infraccion_id = i.id
  WHERE pg.fecha >= CURRENT_DATE - INTERVAL '1 year'
  GROUP BY c.alcaldia
  HAVING SUM(pg.importe) >= 100000
),
top_infractor AS (
  SELECT alcaldia, propietario_id
  FROM (
    SELECT c.alcaldia, v.propietario_id,
           ROW_NUMBER() OVER (PARTITION BY c.alcaldia ORDER BY COUNT(*) DESC) AS rn
    FROM camara c
    JOIN infraccion i ON i.camara_id = c.id
    JOIN vehiculo v ON v.id = i.vehiculo_id
    GROUP BY c.alcaldia, v.propietario_id
  ) t
  WHERE rn = 1
),
top_pagador AS (
  SELECT alcaldia, acreedor_id AS propietario_id
  FROM (
    SELECT c.alcaldia, pg.acreedor_id,
           ROW_NUMBER() OVER (PARTITION BY c.alcaldia ORDER BY SUM(pg.importe) DESC) AS rn
    FROM camara c
    JOIN infraccion i ON i.camara_id = c.id
    JOIN pago pg ON pg.infraccion_id = i.id
    GROUP BY c.alcaldia, pg.acreedor_id
  ) t
  WHERE rn = 1
)
SELECT ca.alcaldia,
       ca.n_activas,
       pa.total_pagado,
       p1.nombre || ' ' || p1.apellido AS top_infractor,
       p2.nombre || ' ' || p2.apellido AS top_pagador
FROM camaras_activas ca
JOIN pagos_ultimo_anio pa ON pa.alcaldia = ca.alcaldia
JOIN top_infractor ti ON ti.alcaldia = ca.alcaldia
JOIN top_pagador tp ON tp.alcaldia = ca.alcaldia
JOIN propietario p1 ON p1.id = ti.propietario_id
JOIN propietario p2 ON p2.id = tp.propietario_id
WHERE ti.propietario_id <> tp.propietario_id;
```

**Conceptos usados:**
1. CTEs múltiples encadenadas.
2. GROUP BY + HAVING para filtrar grupos.
3. Subquery con window function (ROW_NUMBER) para top-1 por grupo.
4. Múltiples JOINs entre las 4 tablas del ERD.
5. Filtrado final con comparación entre CTEs.

**Respuesta final:** query arriba — esto es el nivel "final ITAM real".

---

## Ejercicio K7 — Detectar query incorrecta con razonamiento profundo

**Keywords para buscar:** `debugging avanzado`, `LEFT JOIN`, `WHERE rompe LEFT JOIN`, `convertir LEFT a INNER`, `examen ITAM`, `MUY difícil`, `trampa`

**Tipo de pregunta:** debugging avanzado

**Dificultad:** MUY difícil

**Patrones relacionados:**
- WHERE en columna de tabla derecha en un LEFT JOIN convierte en INNER JOIN implícito.

**Trampas típicas:**
- No mover la condición al ON.

**Enunciado:**
Esta query intenta listar **todos** los vehículos con sus infracciones de tipo `'velocidad'`. Si un vehículo no tiene infracciones de velocidad, debe aparecer con NULLs. Pero solo aparecen vehículos con al menos una infracción de velocidad. ¿Por qué? Corrígela.

```sql
SELECT v.id, v.placa, i.fecha, i.importe
FROM vehiculo v
LEFT JOIN infraccion i ON i.vehiculo_id = v.id
WHERE i.tipo = 'velocidad';
```

---

**Solución paso a paso:**

- El LEFT JOIN incluye vehículos sin infracciones, pero para ellos `i.tipo` es NULL.
- La condición `WHERE i.tipo = 'velocidad'` evalúa a UNKNOWN para NULLs → se descartan.
- Resultado: solo quedan vehículos con infracciones de velocidad → LEFT JOIN actúa como INNER JOIN.

**Corrección:** mover la condición al ON:

```sql
SELECT v.id, v.placa, i.fecha, i.importe
FROM vehiculo v
LEFT JOIN infraccion i
  ON i.vehiculo_id = v.id
 AND i.tipo = 'velocidad';
```

Ahora la condición se aplica antes del LEFT JOIN: solo matches si `i.tipo = 'velocidad'`; los vehículos sin matches se preservan con NULL.

**Alternativa con OR:**

```sql
WHERE i.tipo = 'velocidad' OR i.tipo IS NULL
```

Pero esta puede incluir vehículos con infracciones de **otro** tipo pero no de velocidad de forma confusa; preferir mover al ON.

**Respuesta final:** mover la condición al ON.

---

## Ejercicio K8 — Pregunta capciosa: ¿cuándo NO se debe normalizar?

**Keywords para buscar:** `desnormalización`, `cuándo no normalizar`, `performance`, `OLAP`, `data warehouse`, `examen ITAM`, `conceptual`, `difícil`

**Tipo de pregunta:** conceptual extensiva

**Dificultad:** difícil (conceptual)

**Patrones relacionados:**
- Trade-off entre normalización e performance.

**Trampas típicas:**
- Decir "siempre normalizar" sin matices.

**Enunciado:**
Has visto que normalizar elimina anomalías. Pero el profesor te pregunta: "¿en qué casos NO conviene normalizar y por qué?" Da una respuesta conceptual completa.

---

**Solución paso a paso:**

**Casos donde NO conviene normalizar:**

1. **Data warehouses / OLAP:** las queries son mayoritariamente de lectura analítica con muchos JOINs. Normalizar al máximo provoca decenas de JOINs en cada query, lo que degrada el desempeño. Patrones como **star schema** o **snowflake** desnormalizan deliberadamente.

2. **Datos derivados frecuentemente leídos:** si una columna se calcula de otras pero se consulta cientos de veces por segundo, almacenarla denormalizada (con triggers o actualización en transacción) ahorra cómputo. Ejemplo: `total_pagado` en la tabla `propietario` aunque sea derivable.

3. **Reportes y vistas materializadas:** prácticamente todas las vistas materializadas son desnormalizaciones precalculadas para evitar el costo de JOIN repetido.

4. **Datos casi inmutables / históricos:** una factura emitida no cambia. Almacenar el nombre del cliente, dirección, etc. en la factura misma (denormalización deliberada) es **correcto** porque captura el estado en ese momento — si el cliente cambia de nombre después, la factura histórica no debe cambiar.

5. **Datos con DFs estables pero costo prohibitivo de JOIN:** si la DF es "casi" siempre verdadera pero forzarla con normalización mata el desempeño, a veces se preserva la denormalización con triggers o constraint check.

**Resumen mental:** normalizar es para evitar anomalías en sistemas OLTP (transaccionales). Desnormalizar es para optimizar lectura en sistemas OLAP o capturar estado histórico. La decisión no es absoluta: depende del patrón de uso.

**Respuesta final:** los 5 casos arriba.

---

## Ejercicio K9 — Recorrer mentalmente el ERD: query "imposible sin razonar"

**Keywords para buscar:** `ERD`, `recorrer mentalmente`, `múltiples caminos`, `Fotomultas`, `examen ITAM`, `MUY difícil`

**Tipo de pregunta:** análisis ERD + SQL

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Distinguir entre dos relaciones que conectan las mismas entidades por distintos caminos.

**Trampas típicas:**
- Confundir `propietario_id` (dueño del vehículo) con `acreedor_id` (quien pagó).

**Enunciado:**
Encuentra los propietarios que han **pagado** infracciones de vehículos que **no son suyos**. Devuelve nombre del pagador, placa del vehículo, e importe pagado.

---

**Solución paso a paso:**

**Recorrido mental del ERD:**
- Hay dos caminos entre `pago` y `propietario`:
  1. `pago.acreedor_id → propietario.id` (el que paga).
  2. `pago → infraccion → vehiculo → propietario` (el dueño del vehículo de la infracción).
- Queremos las filas donde estos dos caminos terminan en propietarios **distintos**.

```sql
SELECT pa_acreedor.nombre || ' ' || pa_acreedor.apellido AS pagador,
       v.placa,
       p.importe AS importe_pagado
FROM pago p
JOIN propietario pa_acreedor ON pa_acreedor.id = p.acreedor_id
JOIN infraccion i ON i.id = p.infraccion_id
JOIN vehiculo v ON v.id = i.vehiculo_id
WHERE v.propietario_id <> p.acreedor_id;
```

**Notas:**
- Usar alias `pa_acreedor` para no confundir con la tabla original.
- La condición clave: `v.propietario_id <> p.acreedor_id`.

**Variante** (excluyendo casos donde el dueño es NULL):

```sql
WHERE (v.propietario_id <> p.acreedor_id OR v.propietario_id IS NULL)
```

**Respuesta final:** query arriba — esto es exactamente el tipo de pregunta donde el examen prueba si entiendes la diferencia entre los dos FKs.

---

## Ejercicio K10 — Final: combinar window function, CTE recursiva conceptual y normalización

**Keywords para buscar:** `simulacro final`, `múltiples temas`, `window function`, `CTE`, `conceptual`, `examen ITAM`, `MUY difícil`

**Tipo de pregunta:** examen simulado

**Dificultad:** MUY difícil

**Patrones relacionados:**
- Todos los anteriores.

**Trampas típicas:**
- No leer toda la pregunta.

**Enunciado (multi-parte):**

a) Para cada propietario, calcula el ranking según el importe total que ha pagado en los últimos 12 meses (1 = más). Usa window function.

b) Considera la siguiente tabla:
`reporte(propietario_id, mes, n_infracciones, total_pagado, alcaldia)` donde un propietario puede aparecer varias veces por mes (una por alcaldía). DFs:
- {propietario_id, mes, alcaldia} → n_infracciones, total_pagado
¿Está en FNBC? Justifica.

c) ¿Qué pasaría si en la query del inciso (a) usaras `RANK()` en vez de `ROW_NUMBER()` y hubiera 3 propietarios empatados en el lugar 1?

---

**Solución paso a paso:**

**a)**

```sql
WITH pagos_anuales AS (
  SELECT acreedor_id,
         SUM(importe) AS total
  FROM pago
  WHERE fecha >= CURRENT_DATE - INTERVAL '12 months'
  GROUP BY acreedor_id
)
SELECT p.id, p.nombre, p.apellido,
       COALESCE(pa.total, 0) AS total,
       ROW_NUMBER() OVER (ORDER BY COALESCE(pa.total, 0) DESC) AS posicion
FROM propietario p
LEFT JOIN pagos_anuales pa ON pa.acreedor_id = p.id
ORDER BY posicion;
```

**b)** Llave de `reporte`: {propietario_id, mes, alcaldia} (única DF dada). Verificar FNBC:
- DF dada: {propietario_id, mes, alcaldia} → n_infracciones, total_pagado. Lado izquierdo es superllave (es la llave). ✓
- No hay otras DFs declaradas.

Está en FNBC.

⚠️ Pero ojo: si añadiéramos una DF como `propietario_id → nombre_propietario` violaría 2FN y por tanto FNBC. La tabla actual no la tiene, así que está bien.

**c)** Con `RANK()` y 3 empatados en 1:
- Los 3 reciben posición 1.
- La siguiente posición es 4 (RANK deja huecos).
- Con `ROW_NUMBER()` cada uno recibiría 1, 2, 3 (rompe empates arbitrariamente — el ordenamiento entre los 3 sería no determinista a menos que añadas un tiebreaker explícito).

Si se quiere "1, 1, 1, 2" usar `DENSE_RANK()`.

**Respuesta final:** las tres respuestas arriba.

---

# 🏁 Cierre y consejos finales

---

## Estrategia de examen — recomendaciones finales

1. **Lee TODO el enunciado antes de escribir SQL.** El examen ITAM mete trampas en la última oración.
2. **Identifica tipo de pregunta primero:**
   - Conceptual → escribe definición + ejemplo.
   - SQL → identifica tablas, JOINs necesarios, agregaciones, filtros.
   - ERD → dibuja primero las relaciones a mano.
   - Normalización → calcula llave, busca DFs problemáticas, descompón.
3. **En SQL, escribe primero el FROM/JOIN, luego el WHERE, luego el SELECT.** El orden de ejecución es el orden de pensamiento.
4. **Verifica casos borde:** ¿qué pasa con NULLs? ¿Y si no hay datos? ¿Y si hay empates?
5. **Si te quedan 10 minutos:** revisa los CHECKs, los CASCADE, los HAVING vs WHERE — ahí caen los puntos fáciles.
6. **No te trabes en una pregunta.** Si una query no sale, ataca otra y vuelve.

---

## Checklist mental rápido antes del examen

- [ ] Sé escribir CREATE TABLE con PK, FK, CHECK, NOT NULL, UNIQUE, DEFAULT.
- [ ] Sé las diferencias entre CASCADE, SET NULL, RESTRICT, NO ACTION.
- [ ] Sé todos los JOINs y cuándo usar LEFT vs INNER.
- [ ] Sé GROUP BY + HAVING y por qué WHERE no acepta agregaciones.
- [ ] Sé EXISTS, NOT EXISTS, IN, NOT IN, ANY, ALL, y los problemas con NULL.
- [ ] Sé ROW_NUMBER vs RANK vs DENSE_RANK, y LAG/LEAD.
- [ ] Sé window frames: ROWS vs RANGE vs GROUPS.
- [ ] Sé definir trivialidad de DF (Y⊆X) y de DMV (Y⊆X o XY=E).
- [ ] Sé calcular cierre de atributos.
- [ ] Sé verificar FNBC y 4FN.
- [ ] Sé identificar 2FN/3FN violadas y descomponer.
- [ ] Conozco el ERD de Fotomultas: 5 tablas, todas relaciones 1:N, dos FKs en `pago` (acreedor distinto de propietario del vehículo).

---

## Mensaje final

Esta guía es exhaustiva por diseño. No la leas linealmente — úsala como referencia mientras practicas. La forma más rápida de prepararse:

1. Lee la sección de **detección de patrones** (15 min).
2. Lee la sección de **teoría** de los temas donde te sientes débil (1-2 hrs).
3. Haz 5-10 ejercicios del bloque correspondiente intentando resolverlos **antes** de leer la solución (2-3 hrs).
4. Revisa el cheat sheet y el checklist el día del examen (30 min).

**Total: 4-6 horas de estudio focalizado** > 12 horas leyendo PPTs sin orden.

¡Mucha suerte en el final! 🍀

---
