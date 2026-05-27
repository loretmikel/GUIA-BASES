# 🎓 GUÍA DEFINITIVA — EXAMEN FINAL DE BASES DE DATOS (ITAM)

> **Base de datos del ERD:** Foto-multas de la Ciudad de México
> **Tablas:** `infraccion`, `camara`, `vehiculo`, `propietario`, `pago`
> **Cobertura:** Temas 1–5 + Examen tipo final + patrones recurrentes

---

## 📑 Tabla de contenido

1. [Cómo usar esta guía eficientemente](#cómo-usar-esta-guía-eficientemente)
2. [Análisis profundo del ERD de foto-multas](#análisis-profundo-del-erd-de-foto-multas)
3. [Detección de patrones del examen final](#detección-de-patrones-del-examen-final)
4. [Teoría — Tema 1: Modelo ER y Diseño Conceptual](#teoría--tema-1-modelo-er-y-diseño-conceptual)
5. [Teoría — Tema 2: Consultas SQL](#teoría--tema-2-consultas-sql)
6. [Teoría — Tema 3: DDL, Restricciones, Modificación de Datos](#teoría--tema-3-ddl-restricciones-modificación-de-datos)
7. [Teoría — Tema 4: Normalización (DF, DMV, 1FN–5FN, FNBC)](#teoría--tema-4-normalización-df-dmv-1fn5fn-fnbc)
8. [Teoría — Tema 5: Funcionalidades Avanzadas (índices, transacciones, vistas, ACID)](#teoría--tema-5-funcionalidades-avanzadas-índices-transacciones-vistas-acid)
9. [Mapa mental de cómo recorrer el ERD para resolver joins](#mapa-mental-de-cómo-recorrer-el-erd-para-resolver-joins)
10. [Ejercicios masivos — sección de práctica intensiva](#ejercicios-masivos--sección-de-práctica-intensiva)
11. [Checklist final de 24 h antes del examen](#checklist-final-de-24-h-antes-del-examen)

---

# Cómo usar esta guía eficientemente

## 🎯 Filosofía de la guía

Esta guía **NO es un resumen lineal**. Es una **base de datos de información indexada por Ctrl+F**. La idea es que durante el examen (o el repaso final) tú **sepas qué buscar**, encuentres el patrón, lo apliques, y termines.

## 🔍 Cómo buscar rápido con Ctrl+F

Usa **palabras clave específicas**, no genéricas. Estos son los términos más útiles, ordenados por frecuencia esperada en el examen:

### Para encontrar **teoría** (definiciones, conceptos)
| Buscar | Te lleva a |
|---|---|
| `# Teoría` | Inicio de todas las secciones teóricas |
| `## Definición:` | Definiciones formales |
| `## Intuición:` | Forma intuitiva de pensar un concepto |
| `## Trampa:` | Errores comunes en examen |
| `## Diferencia con` | Comparativas entre conceptos similares |

### Para encontrar **ejercicios** por tema
| Buscar | Te lleva a |
|---|---|
| `Ejercicio` | Cualquier ejercicio numerado |
| `Tipo de pregunta: SQL` | Solo ejercicios SQL |
| `Tipo de pregunta: ERD` | Solo conceptual ERD |
| `Tipo de pregunta: normalización` | Solo normalización |
| `Dificultad: MUY difícil` | Solo los más duros |

### Para encontrar **patrones SQL** específicos
| Buscar | Te lleva a |
|---|---|
| `INNER JOIN`, `LEFT JOIN`, `FULL OUTER JOIN` | Tipos de join |
| `GROUP BY`, `HAVING`, `COUNT(*)`, `SUM(`, `AVG(` | Agregación |
| `EXISTS`, `NOT EXISTS`, `IN`, `NOT IN` | Subconsultas |
| `OVER (PARTITION BY`, `ROW_NUMBER`, `RANK`, `LAG`, `LEAD` | Window functions |
| `WITH ` | CTEs |
| `CASCADE`, `RESTRICT`, `SET NULL` | FK actions |
| `EXTRACT(MONTH`, `EXTRACT(YEAR` | Manipulación de fechas |

### Para encontrar **tablas y columnas reales del ERD**
| Buscar | Te lleva a |
|---|---|
| `infraccion.id`, `vehiculo.placa`, etc. | Atributos específicos |
| `acreedor_id` | La FK confusa de pago |
| `propietario_id` | La FK confusa de vehiculo |
| `infraccion_id` | La FK de pago hacia infraccion |
| `camara_id`, `vehiculo_id` | FKs de infraccion |

## 📅 Plan de estudio de 1–2 días antes del examen

### **Día -2 (48 h antes)**
1. **(45 min)** Leer las secciones de teoría en orden de los Temas 1 → 5.
2. **(30 min)** Memorizar el ERD: las 5 tablas, sus columnas y todas las FKs. **Si no recuerdas las FKs de cabeza, no puedes escribir queries en el examen**.
3. **(60 min)** Hacer ejercicios fáciles + medios.
4. **(45 min)** Repaso de normalización: identificar DF triviales vs no triviales, condiciones de FNBC y 4FN.

### **Día -1 (24 h antes)**
1. **(60 min)** Hacer **todos** los ejercicios difíciles + muy difíciles.
2. **(30 min)** Revisar las "Trampas típicas" de cada sección.
3. **(30 min)** Resolver de memoria (sin ver) el examen-tipo-final completo traducido al ERD de foto-multas (Ejercicios 30+ de esta guía replican los del examen).
4. **(30 min)** Crear tu propio "cheat sheet mental" con la sintaxis BN de cada cláusula.

### **Día del examen (mañana, 1 h antes)**
- Lee solo los `## Trampa:` y los recuadros con 🚨.
- Repasa el ERD una última vez.
- **No estudies nada nuevo**.

## 🧠 Cómo identificar patrones de preguntas durante el examen

Cuando leas una pregunta, **clasifícala primero**. Cada patrón tiene una solución conocida:

| Si la pregunta dice... | Es probablemente... | Aplica esta plantilla |
|---|---|---|
| "Nombra las llaves foráneas de la tabla X" | **ERD conceptual** | Listar FKs + cardinalidad |
| "¿Por qué [no] conviene un identificador artificial?" | **PK natural vs artificial** | Estabilidad, indexación, tamaño |
| "¿Esta relvar sigue en X FN?" | **Normalización** | Identificar DF/DMV no triviales |
| "Indica cuáles DF son triviales" | **Definición trivial** | $X \to Y$ trivial sii $Y \subseteq X$ |
| "Devuelve [columnas] del usuario que..." | **Join + SELECT básico** | INNER JOIN encadenado |
| "...al menos N tuplas relacionadas..." | **GROUP BY + HAVING + COUNT** | Plantilla COUNT-HAVING |
| "Top N usuarios que más..." | **GROUP BY + ORDER BY + LIMIT** | Plantilla Top-N |
| "Para cada tupla, cuántos..." | **Window function** | `COUNT(*) OVER (PARTITION BY ...)` |
| "Agrega una columna y poblada según otra tabla" | **ALTER + UPDATE en transacción** | `BEGIN; ALTER...; UPDATE...; COMMIT;` |
| "Crea una tabla con las siguientes características" | **CREATE TABLE con constraints** | Plantilla CREATE con NOT NULL + PK + FK |
| "El sistema es lento al buscar por X" | **Optimización con índices** | `CREATE INDEX ON ...` |
| "Los usuarios ingresan valores inválidos" | **CHECK constraint o trigger** | `ADD CHECK (...)` |

## 🎯 Cómo usar cada ejercicio

1. **Lee el enunciado completo**. No mires hacia abajo.
2. **Identifica el patrón** usando la tabla anterior.
3. **Lista las tablas necesarias** (usando el ERD).
4. **Traza el camino de joins** mentalmente.
5. **Escribe la query** (o tu respuesta conceptual) en papel.
6. **Solo entonces baja** a "Solución paso a paso".
7. **Compara**. Si difiere, busca por qué.
8. **Si fallaste**, marca el patrón en el cheat-sheet mental.

---

# Análisis profundo del ERD de foto-multas

## 🗺️ Visión general

El ERD modela el **servicio de foto-multas de la CDMX**: cámaras automatizadas detectan infracciones de tránsito y registran multas que los propietarios de vehículos deben pagar.

> 💡 **Mentalidad**: piensa en el flujo real:
> `cámara` detecta → genera `infraccion` para un `vehiculo` → el `vehiculo` tiene un `propietario` → el propietario hace `pago(s)` para saldar la infracción.

## 📋 Catálogo exhaustivo de entidades

### 🟦 `propietario` — el dueño del vehículo

| Columna | Tipo | Notas |
|---|---|---|
| `id` | `bigint` | **PK** (artificial) |
| `nombre` | `varchar(300)` | Nombre |
| `apellido` | `varchar(300)` | Apellido |
| `correo` | `varchar(254)` | (no marcado UNIQUE en el ERD, pero conceptualmente único) |
| `telefono` | `varchar(15)` | |

- **Rol semántico:** ciudadano dueño de uno o más vehículos. Es quien paga las multas (a través de `pago.acreedor_id`).
- **Cuidado:** no es necesariamente quien conducía cuando se cometió la infracción.

### 🚗 `vehiculo` — el medio de transporte

| Columna | Tipo | Notas |
|---|---|---|
| `id` | `bigint` | **PK** |
| `placa` | `varchar(20)` | Placa (conceptualmente única en el mundo real) |
| `marca` | `varchar(100)` | |
| `anio` | `smallint` | |
| `color` | `varchar(20)` | |
| `propietario_id` | `bigint` | **FK → `propietario.id`** |

- **FK aquí:** `propietario_id` → `propietario.id`
- **Cuidado:** la columna `placa` **no es PK** según el examen tipo final (regla 4: "la columna id de cada tabla es la llave primaria; no es correcto asumir que otra columna es llave"). Aunque sea lógicamente única, **no asumas que tiene UNIQUE constraint**.

### 📸 `camara` — el equipo de vigilancia

| Columna | Tipo | Notas |
|---|---|---|
| `id` | `bigint` | **PK** |
| `tipo` | `varchar(100)` | tipo de cámara |
| `activa` | `boolean` | si está en funcionamiento |
| `alcaldia` | `varchar(100)` | en qué alcaldía está instalada |

- **No tiene FKs salientes.** Es una entidad "fuente".
- **Cuidado:** `activa` es booleano. Filtrar `WHERE activa = TRUE` o `WHERE activa IS TRUE`.

### ⚠️ `infraccion` — la multa

| Columna | Tipo | Notas |
|---|---|---|
| `id` | `bigint` | **PK** |
| `fecha` | `timestamp` | momento de la infracción |
| `tipo` | `varchar(100)` | clasificación de la falta |
| `importe` | `numeric(10, 2)` | monto original de la multa |
| `vehiculo_id` | `bigint` | **FK → `vehiculo.id`** |
| `camara_id` | `bigint` | **FK → `camara.id`** |

- **Tiene 2 FKs salientes:** `vehiculo_id` y `camara_id`.
- **Cuidado:** es la tabla "central" del modelo. Casi todas las queries pasan por aquí.

### 💰 `pago` — el pago (total o parcial) de una multa

| Columna | Tipo | Notas |
|---|---|---|
| `id` | `bigint` | **PK** |
| `fecha` | `timestamp` | cuándo se hizo el pago |
| `importe` | `numeric(10, 2)` | cuánto se pagó |
| `infraccion_id` | `bigint` | **FK → `infraccion.id`** |
| `acreedor_id` | `bigint` | **FK → `propietario.id`** ⚠️ **trampa** |

- **🚨 TRAMPA CRÍTICA:** `acreedor_id` apunta a `propietario.id`, **no** a una tabla "acreedor". Es el propietario que efectúa el pago.
- Una `infraccion` puede tener **múltiples `pago`s** (pagos parciales).

## 🔗 Catálogo exhaustivo de relaciones (FKs y cardinalidades)

| # | Relación | FK | Cardinalidad propia | Cardinalidad inversa |
|---|---|---|---|---|
| 1 | `propietario` 1 — N `vehiculo` | `vehiculo.propietario_id` | Un vehículo tiene **exactamente 1** propietario (obligatoria) | Un propietario tiene **0 ó muchos** vehículos (opcional) |
| 2 | `vehiculo` 1 — N `infraccion` | `infraccion.vehiculo_id` | Una infracción es de **exactamente 1** vehículo (obligatoria) | Un vehículo tiene **0 ó muchas** infracciones (opcional) |
| 3 | `camara` 1 — N `infraccion` | `infraccion.camara_id` | Una infracción la detecta **exactamente 1** cámara (obligatoria) | Una cámara puede haber detectado **0 ó muchas** infracciones (opcional) |
| 4 | `infraccion` 1 — N `pago` | `pago.infraccion_id` | Un pago corresponde a **exactamente 1** infracción (obligatoria) | Una infracción puede tener **0 ó muchos** pagos (opcional) |
| 5 | `propietario` 1 — N `pago` | `pago.acreedor_id` | Un pago lo efectúa **exactamente 1** propietario (obligatoria) | Un propietario puede haber hecho **0 ó muchos** pagos (opcional) |

**Notación de cardinalidad** (recordatorio del Tema 1):
- `‖` (raya doble) = obligatoria (al menos 1) y/o "una sola"
- `O` (círculo) = opcional (puede ser 0)
- `<` (pata de gallo / crow's foot) = muchos

## 🧭 Caminos de joins comunes (memorízalos)

Estos son los **caminos físicos** que vas a recorrer en casi todos los ejercicios. **Aprende a recorrer el ERD mentalmente.**

### Camino A: "del pago al propietario que lo hizo"
```
pago ── (acreedor_id) ──> propietario
```

### Camino B: "del pago al dueño del vehículo multado"
```
pago ── (infraccion_id) ──> infraccion ── (vehiculo_id) ──> vehiculo ── (propietario_id) ──> propietario
```
🚨 **Trampa común**: `acreedor_id` y "dueño del vehículo" **NO son lo mismo necesariamente**. Un propietario puede pagar la multa de otro vehículo. **Lee con cuidado a quién pertenece el pago**.

### Camino C: "de la cámara a los propietarios multados"
```
camara ── (camara_id) <── infraccion ── (vehiculo_id) ──> vehiculo ── (propietario_id) ──> propietario
```
Cuatro tablas. Patrón clásico de pregunta tipo "qué propietarios fueron detectados por cámaras de la alcaldía X".

### Camino D: "total recaudado por una infracción"
```
infraccion ── id ──> pago.infraccion_id
(GROUP BY infraccion.id, SUM(pago.importe))
```
Comparado con `infraccion.importe` te dice si una multa está **pagada totalmente, parcialmente o sin pagar**.

### Camino E: "infracciones por alcaldía"
```
camara.alcaldia ── camara.id ──> infraccion.camara_id
(GROUP BY camara.alcaldia)
```

### Camino F: "vehículos sin infracciones" (anti-join)
```
vehiculo LEFT JOIN infraccion ON vehiculo.id = infraccion.vehiculo_id
WHERE infraccion.id IS NULL
```
o equivalente con `NOT EXISTS`.

## 🎯 Lugares donde el profesor suele poner trampas

> 🚨 **Lista de focos rojos** — revisa cada uno antes del examen:

1. **`acreedor_id` apunta a `propietario`, no a una tabla "acreedor"**. Confunde porque el nombre semántico es diferente del nombre técnico.
2. **`placa` NO es llave primaria**. Es solo `varchar(20)` sin UNIQUE en el ERD.
3. **`correo` no aparece como UNIQUE en el ERD** de foto-multas (aunque conceptualmente lo sea). Confirma siempre.
4. **Múltiples pagos por una sola infracción**: si haces `JOIN infraccion ON pago...` y luego un `COUNT(*)`, vas a contar duplicados.
5. **Una infracción puede no tener ningún pago**: si quieres "saldo pendiente", necesitas `LEFT JOIN pago` o un `COALESCE(SUM(pago.importe), 0)`.
6. **`importe` aparece DOS veces** con el mismo nombre (en `infraccion` y en `pago`). Cuidado al hacer JOIN: califica siempre con prefijo de tabla.
7. **`fecha` también aparece DOS veces** (en `infraccion` y en `pago`). Misma regla.
8. **`activa` (de cámara) es boolean**, no integer. Sintaxis específica.
9. **Un propietario sin vehículos es válido**. Si haces `propietario JOIN vehiculo`, los pierdes; usa `LEFT JOIN`.
10. **Un vehículo sin infracciones es válido**. Same.

## 💡 Patrones de diseño que el ERD revela

- **Identificadores artificiales (`bigint id`) en todas las tablas**: regla de diseño. El profesor preguntará "por qué" en al menos una pregunta conceptual.
- **No hay tabla pivote N:M visible**: todas las relaciones son 1:N. Si el examen pide modelar algo M:N (ejemplo: vehículos con varios propietarios), tendrás que **proponer** la tabla pivote.
- **Pagos parciales modelados como tabla separada**: en vez de poner `monto_pagado` en `infraccion`, se modeló como tabla `pago`. Eso permite múltiples pagos por infracción → mejor diseño normalizado.
- **`tipo` aparece en `infraccion` y `camara`**: no parecen estar normalizadas en una tabla aparte (`tipo_infraccion`, `tipo_camara`). Esto podría ser un punto de mejora que el examen podría cuestionar.

---

# Detección de patrones del examen final

> **Análisis basado en**: el examen-tipo-final (BD youtube) + temas de las diapositivas + estructura típica de ITAM.

## 🎯 Estructura probable del examen final

| # | Patrón | Probabilidad | Cobertura en esta guía |
|---|---|---|---|
| 1 | Llaves foráneas + cardinalidad + obligatoriedad de una tabla específica | **🔴 Muy alta** | Ej. 1, 2 |
| 2 | Justificación ingenieril de PK artificial vs natural | **🔴 Muy alta** | Ej. 3 |
| 3 | Verificación de forma normal (FNBC o 4FN) tras agregar/quitar atributos | **🔴 Muy alta** | Ej. 4, 5, 28 |
| 4 | Acciones del DBMS para validar datos / acelerar consultas (CHECK + INDEX) | **🟡 Alta** | Ej. 6, 23 |
| 5 | Identificación de DF triviales y DMV triviales | **🔴 Muy alta** | Ej. 7, 8 |
| 6 | JOIN básico con ORDER BY (SELECT con columnas específicas de 2+ tablas) | **🔴 Muy alta** | Ej. 9, 10 |
| 7 | GROUP BY + HAVING + COUNT(*) ≥ N (umbral) | **🔴 Muy alta** | Ej. 11, 12 |
| 8 | Top N por SUM (con consideraciones de empate y LIMIT) | **🔴 Muy alta** | Ej. 13, 14 |
| 9 | Window function (running count por mes / partición) | **🔴 Muy alta** | Ej. 15, 16 |
| 10 | ALTER TABLE + UPDATE en una sola transacción (BEGIN/COMMIT) | **🔴 Muy alta** | Ej. 17, 18 |
| 11 | CREATE TABLE con NOT NULL + PK + FK con CASCADE | **🔴 Muy alta** | Ej. 19, 20 |

## 🔥 Conceptos favoritos del profesor (alta probabilidad de aparecer)

1. **Cardinalidad y obligatoriedad explícitas** (en lenguaje natural, no solo símbolos).
2. **Llave primaria artificial vs natural**: razones técnicas (estabilidad, tamaño, indexación).
3. **DF trivial: $X \to Y$ trivial sii $Y \subseteq X$**. Memorízalo literal.
4. **DMV trivial: $X \twoheadrightarrow Y$ trivial sii $Y \subseteq X$ o $X \cup Y = E$**.
5. **FNBC**: toda DF no trivial está implicada por las llaves (= "sale de superllave").
6. **4FN**: toda DMV no trivial está implicada por las llaves.
7. **Diferencia entre WHERE y HAVING**: WHERE filtra renglones antes de agrupar, HAVING filtra grupos.
8. **NULL en COUNT**: `COUNT(*)` cuenta tuplas; `COUNT(columna)` ignora NULL.
9. **Window vs GROUP BY**: window preserva todas las filas; GROUP BY colapsa.
10. **Transacciones atómicas**: DDL hace commit implícito en muchos DBMS.
11. **CASCADE en FK**: ON DELETE / ON UPDATE; efectos en propagación.
12. **Índices B-tree vs Hash**: hash solo igualdad; B-tree todos los operadores comparativos.

## 🎲 Tipos de ejercicios repetidos (formato heredado del examen tipo)

- **3 preguntas conceptuales** (ERD, PK, motivos ingenieriles).
- **2 preguntas de normalización** (verificar FN / identificar DF triviales).
- **3–4 queries SQL de complejidad creciente**.
- **1 query con window function**.
- **1 ejercicio de ALTER/UPDATE en transacción**.
- **1 ejercicio CREATE TABLE con constraints**.

## 📈 Patrones de dificultad observados

- Las **3 primeras preguntas** suelen ser conceptuales-medias → **no te confíes**.
- Las **queries SQL crecen en dificultad**: la primera es básica (JOIN simple), la última usa window functions o GROUP BY con HAVING complejo.
- El examen tipo tiene exactamente **11 preguntas**, todas del mismo valor → **no hay "decisivas"**. Saca todas las fáciles.

---

# Teoría — Tema 1: Modelo ER y Diseño Conceptual

## Definición: base de datos

Una **base de datos** es una colección organizada de datos estructurados, almacenada de forma persistente, que se puede consultar y modificar mediante un **DBMS** (Sistema de Gestión de Bases de Datos). El DBMS provee abstracción, integridad, concurrencia, recuperación y seguridad. Lo que el usuario ve como "una tabla" es en realidad una **relvar** (variable de relación) en el modelo relacional, y lo que ve como "datos en esa tabla" es el valor actual de esa relvar (una **relación**).

## Definición: modelo relacional vs modelo ER

- **Modelo ER** (Entidad-Relación): nivel **conceptual**. Describe *qué* hay (entidades) y *cómo se relacionan* (relaciones). No implementa nada. Es el dibujo.
- **Modelo relacional**: nivel **lógico**. Traduce el ER a tablas con columnas, llaves primarias, llaves foráneas y restricciones. Es lo que se implementa en PostgreSQL.

**Camino típico de diseño:** Requerimientos → ER → Esquema relacional → DDL en SQL → Tablas reales.

## Entidad

Una **entidad** es algo del mundo real (o abstracto) que el sistema necesita representar y de lo que necesita almacenar información. En foto-multas: `vehiculo`, `propietario`, `infraccion`, `camara`, `pago` son entidades.

> 💡 **Intuición**: si lo puedes señalar con el dedo o describir como "una cosa que tiene atributos y a la que les pasan eventos", es una entidad. Si solo es una propiedad de algo más, **es un atributo, no una entidad**.

## Atributos

Características de una entidad. Cada atributo tiene un **dominio** (tipo de dato). En el ERD, los tipos `bigint`, `varchar(N)`, `timestamp`, `boolean`, `numeric(p, s)`, `smallint` son los más usados.

- `bigint`: entero grande de 8 bytes. Default para IDs.
- `varchar(N)`: cadena variable, máximo N caracteres.
- `timestamp`: fecha + hora (sin zona horaria).
- `boolean`: TRUE / FALSE / NULL.
- `numeric(10, 2)`: número decimal, 10 dígitos totales, 2 después del punto. Para dinero.
- `smallint`: entero de 2 bytes (rango ~ -32 768 a 32 767). Útil para `anio`.

## Relación (en sentido ER)

Una **relación** en el modelo ER es una asociación entre dos (o más) entidades. **No confundir** con "relación" del modelo relacional (que es una tabla). Cuando el profesor dice "relación", **mira el contexto**:
- Si habla del ERD → asociación (línea entre tablas).
- Si habla de relvar / relación matemática → tabla.

## Cardinalidad

Cuántas instancias de una entidad pueden estar asociadas con cuántas de la otra:

| Tipo | Símbolo del lado | Significado |
|---|---|---|
| Uno y solo uno | `‖` | exactamente 1 |
| Cero o uno | `O‖` | 0 ó 1 (opcional, máximo 1) |
| Uno o muchos | `‖<` (raya + pata) | al menos 1 |
| Cero o muchos | `O<` (círculo + pata) | 0 ó más |

### Cómo leer una relación con notación de crow's foot

Mira el símbolo **del otro lado** de la relación. Si tienes:
```
A ──‖───────────O<── B
```
- "De A a B" → 0 ó muchos B (lado derecho de B)
- "De B a A" → exactamente 1 A (lado izquierdo de A)

### Obligatoriedad

- **Obligatoria**: la cardinalidad **mínima** es 1. El símbolo más cercano a la entidad es `‖`.
- **Opcional**: la cardinalidad mínima es 0. El símbolo más cercano a la entidad es `O`.

> 💡 **Trampa clásica**: confundir el símbolo cercano (obligatoriedad) con el lejano (máximo). **Lee primero el de adentro (obligatorio/opcional) y luego el de afuera (uno/muchos)**.

## Llave primaria (PK)

Conjunto mínimo de atributos que identifica unívocamente cada tupla.
- **Único** y **no nulo** por definición.
- En PostgreSQL, al declararse PK se genera **automáticamente un índice B-tree único**.
- Solo puede haber **una** PK por tabla.

## Llave foránea (FK)

Atributo (o conjunto) de una tabla que referencia la PK (o un UNIQUE) de otra tabla, garantizando **integridad referencial**.
- Puede ser **NULL** (significa "esta tupla no tiene relación con el otro lado").
- No es única por sí misma (la misma FK puede aparecer en múltiples tuplas: eso es lo que da el "muchos a uno").

## Llave candidata vs superllave

- **Superllave**: cualquier conjunto de atributos que identifica unívocamente una tupla. Puede tener atributos "de más".
- **Llave candidata**: superllave **irreducible** (si quitas un atributo, deja de ser superllave).
- La PK es **una** de las llaves candidatas, elegida por diseño.

> 💡 **Memoriza**: toda llave candidata es superllave, pero no al revés.

## PK artificial (surrogate) vs PK natural

| Aspecto | Artificial (ej. `id bigint`) | Natural (ej. `placa varchar(20)`) |
|---|---|---|
| **Estabilidad** | Inmutable (nunca cambia) | Puede cambiar (re-registro, error) |
| **Privacidad** | Opaca, no revela información | Revela datos sensibles |
| **Tamaño** | Compacto (8 bytes) | Grande (varchar) |
| **Indexación** | Rápida en B-tree | Más costosa |
| **Joins** | Eficientes | Menos eficientes |
| **Dependencia** | Ninguna fuera del DBMS | Atada a regulación externa |

> 🎯 **Plantilla de respuesta a pregunta tipo "¿por qué id artificial?"**
> 1. **Estabilidad**: la placa puede cambiar (re-emisión, re-registro vehicular), el id no.
> 2. **Privacidad / no exposición**: el id no expone información del dueño.
> 3. **Eficiencia de indexación**: `bigint` ocupa 8 bytes vs varchar de 20 → índices B-tree más pequeños, más rápidos.
> 4. **Joins más rápidos**: comparar bigint es más barato que comparar strings.
> 5. **Independencia regulatoria**: si cambia el formato de placas en CDMX, no rompe el esquema.

## Integridad referencial

La regla que garantiza que toda FK apunta a un valor existente (o es NULL). Se implementa con la cláusula `REFERENCES`. Cuando se borra/actualiza el "padre", el DBMS aplica la acción declarada (`CASCADE`, `RESTRICT`, `NO ACTION`, `SET NULL`, `SET DEFAULT`).

## Acciones referenciales (ON DELETE / ON UPDATE)

| Acción | Comportamiento |
|---|---|
| `NO ACTION` | Si hay tuplas hijas, lanza error (default en SQL estándar). Diferido al final de la transacción. |
| `RESTRICT` | Igual que NO ACTION pero **no diferido**: error inmediato. |
| `CASCADE` | Propaga el borrado/actualización a las tuplas hijas. |
| `SET NULL` | Pone NULL en las FKs hijas. |
| `SET DEFAULT` | Pone el valor por defecto en las FKs hijas. |

> 🚨 **Trampa**: `NO ACTION` vs `RESTRICT` parecen iguales pero solo difieren en cuándo se valida (al final del statement vs al final de la transacción).

---

# Teoría — Tema 2: Consultas SQL

## El "orden de ejecución" mental

| Orden de escritura | Orden de ejecución | Cláusula |
|---|---|---|
| 1 | 5 | `SELECT` |
| 2 | 1 | `FROM` (+ JOINs) |
| 3 | 2 | `WHERE` |
| 4 | 3 | `GROUP BY` |
| 5 | 4 | `HAVING` |
| 6 | 6 | `ORDER BY` |
| 7 | 7 | `LIMIT` |

> 💡 **Por qué importa**: explica por qué **no puedes** usar un alias de SELECT en WHERE (el alias no existe aún) pero **sí** en ORDER BY (ya se calculó SELECT).

## SELECT y FROM

- `SELECT *` trae todas las columnas. **Evítalo** en queries de producción (sobrecarga, fragilidad ante cambios de esquema).
- `SELECT col1, col2` lista columnas explícitas.
- `SELECT col AS alias` renombra.
- `FROM tabla` lee de una tabla.
- `FROM t1, t2` → producto cartesiano (¡cuidado!).

## Tipos de JOIN

### `INNER JOIN`
Solo tuplas donde **ambos lados coinciden**. Es el join "por defecto" cuando dices solo "join".

```sql
SELECT * FROM A INNER JOIN B ON A.id = B.a_id;
```

### `LEFT (OUTER) JOIN`
Todas las tuplas de la **izquierda**, más las coincidencias de la derecha. Donde no haya match, las columnas de la derecha son NULL.

```sql
SELECT * FROM A LEFT JOIN B ON A.id = B.a_id;
```

> 💡 **Cuándo usarlo**: cuando quieres "todos los X, incluso los que no tienen Y".

### `RIGHT (OUTER) JOIN`
Espejo del LEFT. **Casi nadie lo usa** (es más legible invertir y usar LEFT).

### `FULL OUTER JOIN`
Todas las tuplas de ambos lados, con NULL donde no haya match.

### `CROSS JOIN` (producto cartesiano)
Combina **todo con todo**. Tamaño = |A| × |B|. Útil para generar todas las combinaciones.

```sql
SELECT * FROM A CROSS JOIN B;
-- equivalente a:
SELECT * FROM A, B;
```

### `NATURAL JOIN`
Une por **columnas con el mismo nombre**. **Peligroso**: si agregan una columna con nombre coincidente, se rompe.

## WHERE vs HAVING

| | WHERE | HAVING |
|---|---|---|
| **Cuándo se ejecuta** | Antes de GROUP BY | Después de GROUP BY |
| **Filtra** | Renglones individuales | Grupos |
| **Puede usar funciones de agregación** | ❌ No | ✅ Sí |
| **Puede usar alias de SELECT** | ❌ No | ❌ No (en SQL estándar; algunos DBMS lo permiten) |

```sql
-- WHERE filtra renglones ANTES de agrupar
WHERE infraccion.fecha >= '2024-01-01'

-- HAVING filtra GRUPOS después de agrupar
HAVING COUNT(*) >= 10
```

> 🚨 **Trampa**: poner `HAVING fecha >= '2024-01-01'` cuando `fecha` no está en GROUP BY → **error**.

## Funciones de agregación

| Función | Notas |
|---|---|
| `COUNT(*)` | Cuenta **todas** las tuplas del grupo, incluyendo NULLs |
| `COUNT(columna)` | Cuenta las **no-nulas** de esa columna |
| `COUNT(DISTINCT columna)` | Cuenta valores únicos no-nulos |
| `SUM(columna)` | Suma, ignora NULLs |
| `AVG(columna)` | Promedio aritmético, ignora NULLs |
| `MIN(columna)` | Mínimo |
| `MAX(columna)` | Máximo |

> 🚨 **Trampa**: `COUNT(*)` vs `COUNT(columna)` cuando hay NULLs.
> ```
> COUNT(*)         → 5  (cuenta tuplas)
> COUNT(telefono)  → 3  (ignora 2 NULL)
> ```

## DISTINCT

`SELECT DISTINCT col1, col2 FROM ...` elimina duplicados **del conjunto resultante** (sobre la combinación de columnas seleccionadas).

> 🚨 **Trampa**: `DISTINCT` aplica a **todas** las columnas del SELECT. `SELECT DISTINCT id, nombre` no es lo mismo que "dar IDs distintos".

## Subconsultas

### Tipos por resultado

1. **Escalar** (1 fila, 1 columna): puede usarse en cualquier expresión con `=`, `<`, etc.
2. **Columnar** (N filas, 1 columna): se usa con `IN`, `NOT IN`, `ANY`, `ALL`.
3. **Tabular** (N filas, M columnas): se usa en `FROM` (como derived table) o con `EXISTS`.

### Tipos por dependencia

1. **No correlacionada**: se ejecuta una vez, independiente del query externo.
   ```sql
   WHERE importe > (SELECT AVG(importe) FROM infraccion)
   ```
2. **Correlacionada**: depende de columnas del query externo; se ejecuta una vez por cada tupla externa. Más caro pero más expresivo.
   ```sql
   WHERE EXISTS (SELECT 1 FROM pago WHERE pago.infraccion_id = infraccion.id)
   ```

### EXISTS / NOT EXISTS

Devuelve TRUE/FALSE según si la subconsulta tiene al menos una fila. Se usa con subconsultas correlacionadas.

```sql
-- ¿Hay al menos un pago para esta infracción?
WHERE EXISTS (SELECT 1 FROM pago WHERE pago.infraccion_id = infraccion.id)

-- ¿NO hay pagos para esta infracción?
WHERE NOT EXISTS (SELECT 1 FROM pago WHERE pago.infraccion_id = infraccion.id)
```

> 💡 **Truco de examen**: `SELECT 1` o `SELECT *` dentro de un EXISTS da **exactamente igual**. Lo único que cuenta es si hay filas.

### IN / NOT IN

```sql
WHERE id IN (SELECT vehiculo_id FROM infraccion WHERE ...)
```

> 🚨 **Trampa CRÍTICA con NOT IN y NULLs**: si la subconsulta puede devolver NULL, `NOT IN` devuelve **resultados vacíos inesperadamente**.
> Por eso, **prefiere `NOT EXISTS` sobre `NOT IN`** cuando la columna puede ser NULL.

## CTEs (Common Table Expressions)

Subconsulta nombrada que se define con `WITH`. Mejora legibilidad y permite referenciar varias veces.

```sql
WITH propietarios_morosos AS (
    SELECT propietario.id, propietario.nombre
    FROM propietario
    INNER JOIN vehiculo ON propietario.id = vehiculo.propietario_id
    INNER JOIN infraccion ON vehiculo.id = infraccion.vehiculo_id
    WHERE NOT EXISTS (
        SELECT 1 FROM pago WHERE pago.infraccion_id = infraccion.id
    )
)
SELECT * FROM propietarios_morosos;
```

> 💡 Las CTEs son **subconsultas no correlacionadas con nombre**. Se usan principalmente por legibilidad.

## Funciones de ventana (window functions)

Aplican una función a un "marco" de filas **sin colapsar** las filas. Ideales para "para cada fila, dame el ranking / running total / etc.".

### Sintaxis básica

```sql
funcion() OVER (
    [PARTITION BY columnas]
    [ORDER BY columnas]
    [frame_clause]
)
```

### Diferencia clave con GROUP BY

| | GROUP BY | Window function |
|---|---|---|
| Resultado | Colapsa filas en grupos | Mantiene todas las filas |
| ¿Devuelve detalle? | No | Sí |
| ¿Permite múltiples particiones? | No (uno por query) | Sí (cada ventana es independiente) |

### Funciones de ventana comunes

| Función | Qué hace |
|---|---|
| `ROW_NUMBER()` | Número consecutivo dentro de la partición (1, 2, 3, ...) |
| `RANK()` | Ranking con huecos cuando hay empates (1, 2, 2, 4) |
| `DENSE_RANK()` | Ranking sin huecos (1, 2, 2, 3) |
| `LAG(col, n)` | Valor de la fila `n` posiciones antes |
| `LEAD(col, n)` | Valor de la fila `n` posiciones después |
| `FIRST_VALUE(col)` | Primer valor de la partición ordenada |
| `LAST_VALUE(col)` | Último valor (cuidado con el frame: por default termina en current row) |
| `NTILE(n)` | Divide en `n` cubetas iguales |
| `CUME_DIST()` | Fracción acumulada |

### Frame clause

Define qué filas dentro de la partición se incluyen en cada cálculo. Útil para **running totals** y **moving averages**.

```sql
ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
-- desde el inicio de la partición hasta esta fila

ROWS BETWEEN 2 PRECEDING AND 2 FOLLOWING
-- 2 filas antes hasta 2 después (ventana móvil de 5)
```

> 💡 **ROWS vs RANGE vs GROUPS**: `ROWS` cuenta filas físicas, `RANGE` cuenta por valor del ORDER BY, `GROUPS` cuenta por grupos de pares (`peer groups`).

### Cláusula WINDOW (alias)

```sql
SELECT *, AVG(importe) OVER w
FROM infraccion
WINDOW w AS (PARTITION BY vehiculo_id ORDER BY fecha);
```

## Operadores de conjuntos

| Operador | Comportamiento |
|---|---|
| `UNION` | Une dos queries, **elimina duplicados** |
| `UNION ALL` | Une, **mantiene duplicados** (más rápido) |
| `INTERSECT` | Filas en ambos |
| `EXCEPT` | Filas del primero que no están en el segundo |

Requieren mismo número y tipos de columnas.

## Funciones útiles de fecha (PostgreSQL)

| Función | Ejemplo |
|---|---|
| `EXTRACT(field FROM timestamp)` | `EXTRACT(YEAR FROM fecha)` |
| `DATE_TRUNC('unit', timestamp)` | `DATE_TRUNC('month', fecha)` |
| `NOW()` o `CURRENT_TIMESTAMP` | Fecha-hora actual |
| `AGE(timestamp1, timestamp2)` | Intervalo entre dos fechas |
| `timestamp + INTERVAL '1 day'` | Aritmética de fechas |

---

# Teoría — Tema 3: DDL, Restricciones, Modificación de Datos

## DDL vs DML vs DCL

| Categoría | Comandos | Ejemplo |
|---|---|---|
| **DDL** (Data Definition Language) | CREATE, ALTER, DROP, TRUNCATE | Modifica el **esquema** |
| **DML** (Data Manipulation Language) | INSERT, UPDATE, DELETE, SELECT | Modifica los **datos** |
| **DCL** (Data Control Language) | GRANT, REVOKE | Permisos |

> 🚨 **Trampa**: en PostgreSQL las instrucciones DDL **NO** hacen commit implícito (sí están dentro de una transacción), pero en otros DBMS (Oracle, MySQL) **sí** hacen commit implícito y rompen tu transacción.

## CREATE TABLE — sintaxis completa

```sql
CREATE TABLE [IF NOT EXISTS] nombre_tabla (
    columna1 tipo [restricciones_columna...],
    columna2 tipo [restricciones_columna...],
    ...
    [restricciones_tabla...]
);
```

### Tipos de restricciones

| Restricción | A nivel | Sintaxis típica |
|---|---|---|
| `NOT NULL` | Columna | `nombre VARCHAR(100) NOT NULL` |
| `UNIQUE` | Columna o tabla | `correo VARCHAR(254) UNIQUE` o `UNIQUE (col1, col2)` |
| `PRIMARY KEY` | Columna o tabla | `id BIGINT PRIMARY KEY` o `PRIMARY KEY (col1, col2)` |
| `FOREIGN KEY` | Tabla | `FOREIGN KEY (col) REFERENCES otra(col)` |
| `CHECK` | Columna o tabla | `CHECK (precio > 0)` |
| `DEFAULT` | Columna | `activa BOOLEAN DEFAULT TRUE` |

### Plantilla CREATE TABLE típica de examen

```sql
CREATE TABLE multa_pagada (
    id BIGSERIAL PRIMARY KEY,
    infraccion_id BIGINT NOT NULL,
    fecha_confirmacion TIMESTAMP NOT NULL DEFAULT NOW(),
    monto_pagado NUMERIC(10, 2) NOT NULL CHECK (monto_pagado > 0),
    FOREIGN KEY (infraccion_id) REFERENCES infraccion(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

> 💡 **Tips de examen**:
> - Si dicen "no puede ser nulo" → `NOT NULL`
> - Si dicen "valor válido únicamente positivo" → `CHECK (col > 0)`
> - Si dicen "default" o "por defecto" → `DEFAULT valor`
> - Si dicen "se actualiza al borrar el padre" → `ON DELETE CASCADE`
> - Si dicen "no se puede borrar el padre si tiene hijos" → `ON DELETE RESTRICT` o `NO ACTION`

## ALTER TABLE — operaciones comunes

```sql
-- Agregar columna
ALTER TABLE tabla ADD COLUMN nueva_col TIPO [DEFAULT valor] [NOT NULL] [CHECK (...)];

-- Quitar columna
ALTER TABLE tabla DROP COLUMN col [CASCADE];

-- Agregar restricción
ALTER TABLE tabla ADD CONSTRAINT nombre_constraint UNIQUE (col);
ALTER TABLE tabla ADD FOREIGN KEY (col) REFERENCES padre(col);
ALTER TABLE tabla ADD CHECK (cond);
ALTER TABLE tabla ALTER COLUMN col SET NOT NULL;

-- Quitar restricción
ALTER TABLE tabla DROP CONSTRAINT nombre_constraint;
ALTER TABLE tabla ALTER COLUMN col DROP NOT NULL;

-- Modificar default
ALTER TABLE tabla ALTER COLUMN col SET DEFAULT valor;
ALTER TABLE tabla ALTER COLUMN col DROP DEFAULT;

-- Renombrar columna/tabla
ALTER TABLE tabla RENAME COLUMN viejo TO nuevo;
ALTER TABLE tabla RENAME TO nueva_tabla;

-- Cambiar tipo
ALTER TABLE tabla ALTER COLUMN col TYPE nuevo_tipo USING expresion;
```

> 🚨 **Trampa**: cuando agregas una restricción, se valida **inmediatamente sobre los datos existentes**. Si alguna tupla viola la nueva restricción, falla.

## INSERT

```sql
-- Forma 1: especificando columnas
INSERT INTO tabla (col1, col2) VALUES (val1, val2);

-- Forma 2: múltiples filas
INSERT INTO tabla (col1, col2) VALUES (1, 'a'), (2, 'b'), (3, 'c');

-- Forma 3: a partir de un SELECT
INSERT INTO destino (col1, col2)
SELECT colA, colB FROM origen WHERE ...;
```

## UPDATE

```sql
UPDATE tabla SET col = expresion [, col2 = expr2, ...] WHERE condicion;

-- UPDATE con subconsulta correlacionada
UPDATE vehiculo
SET color = 'gris'
WHERE EXISTS (
    SELECT 1 FROM infraccion
    WHERE infraccion.vehiculo_id = vehiculo.id
        AND infraccion.tipo = 'velocidad'
);
```

> 🚨 **Trampa CRÍTICA**: olvidar el `WHERE` → actualiza **toda la tabla**. Siempre escribe `WHERE` primero, luego rellena `SET`.

## DELETE

```sql
DELETE FROM tabla WHERE condicion;

-- DELETE con subconsulta
DELETE FROM pago
WHERE infraccion_id IN (
    SELECT id FROM infraccion WHERE fecha < '2020-01-01'
);
```

> 🚨 Sin `WHERE`, borra todo. `TRUNCATE TABLE` es más rápido para vaciar completamente pero **no es transaccional en todos los DBMS**.

---

# Teoría — Tema 4: Normalización (DF, DMV, 1FN–5FN, FNBC)

## ¿Por qué normalizamos?

1. **Arreglar fallas lógicas** (decir lo mismo más de una vez de manera inconsistente).
2. **Evitar redundancia** (un mismo hecho repetido en N filas).
3. **Eliminar anomalías** (de inserción, borrado, modificación).

### Las tres anomalías clásicas

- **Anomalía de inserción**: no puedes insertar X sin tener Y. Ejemplo: si pones `nombre_propietario` dentro de `vehiculo`, no puedes registrar un propietario sin vehículo.
- **Anomalía de modificación**: hay que cambiar el mismo dato en N lugares. Ejemplo: si guardas `marca_modelo_anio` en cada infracción, cambiar la marca implica N UPDATEs.
- **Anomalía de borrado**: borras una cosa y pierdes información de otra. Ejemplo: si borras la única infracción de un vehículo y el `color` solo está en `infraccion`, pierdes el color.

## Dependencia funcional (DF)

### Definición formal
Sea $E$ un encabezado (conjunto de atributos). Una DF $X \to Y$ con respecto a $E$ se mantiene en la relvar $R$ si y solo si toda relación que se puede asignar a $R$ satisface la DF.

**Una DF $X \to Y$ se satisface por una relación cuando**: para todo par de tuplas $t_1, t_2$ de la relación, si los valores de $X$ coinciden, entonces los valores de $Y$ también coinciden.

### Intuición
"$X$ determina $Y$" = "si sé $X$, sé $Y$".
Ejemplo: `vehiculo.id → vehiculo.placa` porque cada id de vehículo corresponde a una sola placa.

### DF trivial — DEFINICIÓN CLAVE
**Definición:** una DF $X \to Y$ es trivial si y solo si **se satisface por cualquier relación** con encabezado E.

**Teorema (operacional):** $X \to Y$ es trivial **si y solo si $Y \subseteq X$**.

> 🎯 **MEMORÍZALO LITERAL**: si el lado derecho está contenido (o es igual) en el lado izquierdo → trivial. Esa es la única condición.

**Ejemplos del ERD de foto-multas:**
- `{vehiculo_id, camara_id} → {vehiculo_id}` → **trivial** ({vehiculo_id} ⊆ {vehiculo_id, camara_id})
- `{id, fecha} → {fecha}` → **trivial**
- `{id} → {placa}` → **NO trivial** (placa no está en {id})
- `{id, placa} → {id, placa}` → **trivial** (todo conjunto se contiene a sí mismo)

### Irreductibilidad
Una DF $X \to Y$ es **irreductible con respecto a R** si se mantiene en R y NO se mantiene en R quitando atributos de X (no hay subconjunto propio $X' \subset X$ tal que $X' \to Y$).

## Dependencia multivaluada (DMV)

### Definición intuitiva

$X \twoheadrightarrow Y$ ("X multidetermina Y") significa que para cada valor de $X$, hay un conjunto bien definido de valores de $Y$ **independiente** de los otros atributos.

Ejemplo problemático: si una relvar tiene `(empleado, habilidad, idioma)` y para cada empleado hay un conjunto de habilidades y un conjunto de idiomas que son **independientes entre sí**, hay DMV $empleado \twoheadrightarrow habilidad$ y $empleado \twoheadrightarrow idioma$. La fila producto cartesiano genera redundancia.

### DMV trivial — DEFINICIÓN CLAVE

Una DMV $X \twoheadrightarrow Y$ es trivial si:
- $Y \subseteq X$, **O**
- $X \cup Y = E$ (los dos lados juntos forman todo el encabezado de la relvar).

> 🎯 **Diferencia clave con DF**: una DMV tiene **dos** formas de ser trivial; una DF solo tiene una.

### Las DMVs vienen en pares

Si $R$ tiene encabezado $E = X \cup Y \cup Z$ (disjuntos):
$$X \twoheadrightarrow Y \iff X \twoheadrightarrow Z$$

Por eso a veces se escribe $X \twoheadrightarrow Y | Z$.

### Relación entre DF y DMV
Toda DF es una DMV (lo opuesto no necesariamente). Una DF es un caso especial donde "el conjunto bien definido" tiene tamaño 1.

## Las formas normales — pirámide

```
            5FN
             |
            4FN
             |
           FNBC (Boyce-Codd)
             |
            3FN
             |
            2FN
             |
            1FN
```

Cada nivel implica el anterior. Si una relvar está en 4FN, automáticamente está en FNBC, 3FN, 2FN, 1FN.

## 1FN (Primera Forma Normal)

Todos los atributos son **atómicos** (no son colecciones, listas o estructuras anidadas). En el modelo relacional clásico, **toda relvar está en 1FN por definición**.

## 2FN (Segunda Forma Normal)

Está en 1FN **y** todo atributo no-llave depende funcionalmente de **toda la llave primaria** (no de parte de ella). Solo aplica cuando hay llaves compuestas.

> Ejemplo (anti-2FN): `(infraccion_id, pago_id, fecha_infraccion)` donde `(infraccion_id, pago_id)` es PK y `fecha_infraccion` depende solo de `infraccion_id` → viola 2FN.

## 3FN (Tercera Forma Normal)

Está en 2FN y no hay **dependencias transitivas** (un atributo no-llave determina otro atributo no-llave).

> Ejemplo (anti-3FN): si en `vehiculo` tuvieras `(id, placa, propietario_id, nombre_propietario)`, entonces `id → propietario_id → nombre_propietario` es transitiva.

## FNBC (Forma Normal de Boyce-Codd)

**Una relvar está en FNBC si y solo si toda DF no trivial está implicada por las llaves de R.**

### Versión práctica (memoriza esta)
> Las únicas DF que se mantienen en una relvar en FNBC son:
> 1. **Triviales**, **O**
> 2. **Flechas que salen de superllaves**.

### Cómo verificar FNBC en examen

1. Lista todas las DF no triviales.
2. Para cada una, verifica si el lado izquierdo es superllave (= determina todos los atributos).
3. Si **todas** lo son → está en FNBC.
4. Si **alguna** no lo es → no está en FNBC.

### Implicación por llaves — definición formal
Una DF $X \to Y$ con respecto a $E$ está implicada por las llaves de $R$ si y solo si toda relación que satisface las restricciones de llaves de $R$ también satisface $X \to Y$.

## 4FN (Cuarta Forma Normal)

**Una relvar está en 4FN si y solo si toda DMV no trivial está implicada por las llaves de R.**

### Cómo verificar 4FN

1. Lista todas las DMVs no triviales.
2. Verifica que cada lado izquierdo sea superllave.
3. Si todas lo son → está en 4FN.

> 💡 **Nota**: 4FN implica FNBC, así que también debes verificar que todas las DF no triviales salgan de superllaves.

## 5FN (Quinta Forma Normal o PJ/NF)

Una relvar está en 5FN si toda dependencia de join (JD) no trivial está implicada por las superllaves. **Casi nunca aparece en examen ITAM**, pero es el nivel máximo de normalización.

## ¿Cómo afecta agregar un atributo a la FN?

Esta es la pregunta del millón. Pattern:

> "Se añadió un nuevo atributo $X$ a la relvar $R$. ¿Sigue en FNBC / 4FN?"

**Procedimiento:**
1. **Agrega el nuevo atributo a $E$** (encabezado).
2. **Examina las nuevas DF/DMV** que introduce.
3. **Verifica:** ¿salen de superllaves o son triviales?
4. Si una nueva DF/DMV no trivial **no** sale de superllave, **se rompe la FN**.

### Ejemplo crítico (del examen tipo)
Si `video` tenía PK `{id}` y se agrega `uuid` con DF `{uuid} → {id, titulo, descripcion, fecha_creacion, duracion}`:
- ¿Es `{uuid}` superllave? **Sí**, porque determina todos los atributos (transitivamente, ya que `{id}` es PK).
- Por lo tanto la nueva DF **está implicada por llaves** (de hecho, `{uuid}` es una nueva llave candidata).
- **Sigue en FNBC y 4FN**.

> 💡 **Cuándo se rompe**: cuando el nuevo atributo introduce una DF no trivial cuyo lado izquierdo NO determina todos los atributos.

---

# Teoría — Tema 5: Funcionalidades Avanzadas (índices, transacciones, vistas, ACID)

## Índices

### ¿Qué son?
Estructuras auxiliares que aceleran consultas a cambio de:
- Más espacio en disco.
- INSERTs / UPDATEs / DELETEs más lentos (hay que mantener el índice).

### Tipos principales en PostgreSQL

| Tipo | Operadores soportados | Útil para |
|---|---|---|
| **B-tree (árbol balanceado)** | `=`, `<`, `<=`, `>`, `>=`, `BETWEEN`, `IS NULL`, `IS NOT NULL`, `LIKE 'prefijo%'`, `ILIKE` | La mayoría de los casos. **Default**. |
| **Hash** | Solo `=` | Igualdad pura. Raro de elegir manualmente. |
| GIN, GiST, BRIN, SP-GiST | Casos especializados (texto completo, geometría, rangos) | Casos avanzados |

### Sintaxis

```sql
CREATE INDEX nombre_idx ON tabla USING BTREE (columna);
CREATE INDEX ON tabla USING HASH (columna);
CREATE UNIQUE INDEX nombre_idx ON tabla (columna);
CREATE INDEX nombre_idx ON tabla (col1, col2);  -- multicolumna
DROP INDEX nombre_idx;
```

### Cuándo crear un índice

- Columnas en `WHERE`, `JOIN ON`, `ORDER BY` con alta selectividad.
- FKs (ayudan a JOINs).
- Columnas en `GROUP BY` cuando hay muchos valores distintos.

### Cuándo NO crear

- Tablas pequeñas (escaneo secuencial es más rápido).
- Columnas con poca cardinalidad (un boolean rara vez necesita índice).
- Tablas donde el OLTP es masivo y la lectura escasa (los índices ralentizan escritura).

### Índices únicos
PostgreSQL **genera automáticamente** un índice único cuando se declara `UNIQUE` o `PRIMARY KEY`.

## Vistas

Consulta nombrada que se comporta como tabla virtual.

```sql
CREATE VIEW vw_infracciones_pendientes AS
SELECT i.* 
FROM infraccion i
WHERE NOT EXISTS (
    SELECT 1 FROM pago p WHERE p.infraccion_id = i.id
);

SELECT * FROM vw_infracciones_pendientes;
DROP VIEW vw_infracciones_pendientes;
```

### Vistas actualizables (PostgreSQL)

Una vista es actualizable (puedes hacer INSERT/UPDATE/DELETE sobre ella) si:
1. **No** usa funciones de agregación ni de ventana.
2. **No** usa `GROUP BY` ni `HAVING`.
3. **No** hay subconsultas en SELECT ni FROM.
4. Las subconsultas de WHERE **no** referencian tablas del FROM.
5. **No** usa UNION, EXCEPT, INTERSECT.
6. **No** usa DISTINCT.
7. Si hay JOINs, solo `INNER JOIN`.

> 💡 **Vista materializada** (`CREATE MATERIALIZED VIEW`): vista cuyo resultado se guarda físicamente. Se refresca manualmente con `REFRESH MATERIALIZED VIEW`. Útil para queries caras de leer mucho.

## Transacciones

### ¿Qué es una transacción?
Secuencia de operaciones SQL tratadas como **una unidad indivisible** ("todo o nada").

### Propiedades ACID

| | Significado |
|---|---|
| **A**tomicidad | Una transacción ocurre como una unidad indivisible: o se aplican todos los cambios, o ninguno. |
| **C**onsistencia | Las restricciones (PK, FK, CHECK, UNIQUE, NOT NULL) se mantienen antes y después de la transacción. |
| **I**solation (Aislamiento) | Las transacciones concurrentes se comportan como si fueran serializadas (cada una "exclusiva"). |
| **D**urabilidad | Una vez committed, los cambios sobreviven a caídas del sistema. |

### Sintaxis

```sql
BEGIN;
    UPDATE saldos SET saldo = saldo - 500 WHERE no_cuenta = 123;
    UPDATE saldos SET saldo = saldo + 500 WHERE no_cuenta = 312;
COMMIT;

-- Si algo va mal:
BEGIN;
    -- operaciones...
ROLLBACK;
```

### Savepoints

Puntos intermedios dentro de una transacción a los que se puede regresar.

```sql
BEGIN;
    INSERT INTO ...;
    SAVEPOINT sp1;
    UPDATE ...;
    ROLLBACK TO SAVEPOINT sp1;  -- deshace solo lo de después del savepoint
COMMIT;  -- el INSERT se mantiene
```

### Qué puede terminar una transacción

1. `COMMIT` (éxito).
2. `ROLLBACK` (reversión manual).
3. **Caída del servidor** → rollback automático.
4. **Instrucción DDL** → en algunos DBMS hace commit implícito (en PostgreSQL no, pero ten cuidado).
5. **Comenzar una nueva transacción** sin cerrar la actual → commit implícito en algunos DBMS.
6. **Error / excepción** → rollback automático.

### Niveles de aislamiento (ISO SQL)

| Nivel | Lecturas sucias | No-repetibles | Fantasmas |
|---|---|---|---|
| `READ UNCOMMITTED` | Permitido | Permitido | Permitido |
| `READ COMMITTED` | Prevenido | Permitido | Permitido |
| `REPEATABLE READ` | Prevenido | Prevenido | Permitido |
| `SERIALIZABLE` | Prevenido | Prevenido | Prevenido |

**Fenómenos:**
- **Lectura sucia**: lees datos de otra transacción que aún no hizo commit.
- **Lectura no-repetible**: lees el mismo dato dos veces y obtienes valores distintos porque otra transacción lo modificó y comiteó en medio.
- **Lectura fantasma**: re-ejecutas una consulta y aparecen/desaparecen filas porque otra transacción insertó/borró tuplas.

**Default en PostgreSQL 17**: `READ COMMITTED` + `READ WRITE`.

### Sintaxis con modos

```sql
BEGIN ISOLATION LEVEL SERIALIZABLE READ ONLY;
```

## Mecanismo de logging (write-ahead log)

1. **Registro (log)** de la transacción: se anota la operación y el estado anterior.
2. **Aplicación** de los cambios.
3. **Confirmación** (commit del log).
4. **Reversión** en caso de fallo: usa el log para deshacer.

Esto da **durabilidad** (D de ACID): aunque caiga el servidor a medio commit, al reiniciar el DBMS lee el log y termina/deshace.

## Triggers

Procedimientos que se ejecutan automáticamente ante eventos (INSERT/UPDATE/DELETE).

```sql
CREATE OR REPLACE FUNCTION fn_validar_fecha_infraccion()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.fecha > NOW() THEN
        RAISE EXCEPTION 'La fecha de la infracción no puede ser futura';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER tg_validar_fecha
    BEFORE INSERT OR UPDATE ON infraccion
    FOR EACH ROW
    EXECUTE FUNCTION fn_validar_fecha_infraccion();
```

> 💡 Más simple para validaciones simples: `CHECK constraint`. Para lógica de negocio compleja: trigger.

---

# Mapa mental de cómo recorrer el ERD para resolver joins

Cuando veas una pregunta tipo SQL, sigue **estos 4 pasos**:

## Paso 1: ¿Qué quieren devolver?
Identifica las **columnas resultado**. Esas te dicen qué tablas hay que tocar al menos una vez.

## Paso 2: ¿Qué filtros hay?
Cláusulas `WHERE`/`HAVING` mencionan columnas. Esas tablas también deben estar.

## Paso 3: Conecta las tablas usando el grafo de FKs

```
        ┌─────────────┐
        │ propietario │
        └──────┬──────┘
               │ 1:N (propietario.id = vehiculo.propietario_id)
               ▼
        ┌─────────────┐         ┌─────────────┐
        │  vehiculo   │         │   camara    │
        └──────┬──────┘         └──────┬──────┘
               │ 1:N                  │ 1:N
               │ (.id =                │ (.id =
               │ infraccion           │ infraccion
               │ .vehiculo_id)        │ .camara_id)
               ▼                       ▼
              ┌──────────────────────────┐
              │       infraccion         │
              └──────────────┬───────────┘
                             │ 1:N
                             │ (.id =
                             │ pago.infraccion_id)
                             ▼
                       ┌──────────┐
                       │   pago   │
                       └─────┬────┘
                             │ N:1 (pago.acreedor_id = propietario.id)
                             ▼
                       (vuelve a propietario)
```

## Paso 4: Elige tipo de JOIN

- ¿Necesitas TODOS los X aunque no tengan Y? → **LEFT JOIN**
- ¿Solo los que cumplen con ambos lados? → **INNER JOIN**
- ¿Quieres existencia? → **EXISTS** o **WHERE ... IN**
- ¿Quieres no-existencia? → **NOT EXISTS** (prefiere sobre NOT IN)

---

# Ejercicios masivos — sección de práctica intensiva

> **Todos los ejercicios usan EXCLUSIVAMENTE el ERD de foto-multas** (`infraccion`, `camara`, `vehiculo`, `propietario`, `pago`).
>
> **Cómo usar:**
> 1. Lee el enunciado.
> 2. Resuelve sin ver hacia abajo.
> 3. Baja a la solución y compara.
> 4. Si erraste, marca el patrón para repaso.

---

## Ejercicio 1 — Llaves foráneas y cardinalidad de la tabla `infraccion`

**Keywords para buscar:** `ERD`, `llaves foráneas`, `cardinalidad`, `obligatoria`, `opcional`, `infraccion`, `examen tipo`, `conceptual`, `Q1`

**Tipo de pregunta:** conceptual / ERD

**Dificultad:** fácil

**Tablas involucradas:**
- `infraccion`
- `vehiculo`
- `camara`

**Relaciones usadas del ERD:**
- `infraccion.vehiculo_id → vehiculo.id`
- `infraccion.camara_id → camara.id`

**Patrones relacionados:**
- Pregunta clásica de inicio del examen final ITAM
- Verbalización de cardinalidad en lenguaje natural

**Trampas típicas:**
- Olvidar mencionar que ambas FKs son **obligatorias** (no nullable)
- Confundir el lado obligatorio con el lado opcional
- Pasar por alto que una de las tablas (camara) puede no tener infracciones aún

**Enunciado:**
Utilizando el ERD de foto-multas, nombra las llaves foráneas que existen para la tabla `infraccion`. Para cada una, indica la cardinalidad de la asociación y si es obligatoria u opcional para las entidades `vehiculo` e `infraccion`, así como para `camara` e `infraccion`.

---

### Solución paso a paso

**1. Identificación de FKs en `infraccion`:**
- `vehiculo_id` → referencia a `vehiculo.id`
- `camara_id` → referencia a `camara.id`

**2. Cardinalidad y obligatoriedad entre `vehiculo` e `infraccion`:**

La FK `infraccion.vehiculo_id` implementa la relación:
- Una **infracción** está asociada con **exactamente uno y solamente un vehículo** (obligatoria de lado infracción).
- Un **vehículo** puede estar asociado con **cero, una o muchas infracciones** (opcional de lado vehículo).

En notación: `vehiculo (1, 1) — (0, N) infraccion`.

**3. Cardinalidad y obligatoriedad entre `camara` e `infraccion`:**

La FK `infraccion.camara_id` implementa la relación:
- Una **infracción** es detectada por **exactamente una y solamente una cámara** (obligatoria de lado infracción).
- Una **cámara** puede haber detectado **cero, una o muchas infracciones** (opcional de lado cámara — una cámara recién instalada o desactivada podría no tener ninguna).

En notación: `camara (1, 1) — (0, N) infraccion`.

**4. Justificación de obligatoriedad:**
Las columnas `vehiculo_id` y `camara_id` no permiten NULL (en el ERD se asume eso porque ambas son llaves foráneas a la entidad central del modelo). Por eso son obligatorias desde el lado de `infraccion`.

---

### Respuesta concisa esperada en examen

> **Llaves foráneas de `infraccion`:**
> - `vehiculo_id` referencia `vehiculo.id`
> - `camara_id` referencia `camara.id`
>
> **Cardinalidad y obligatoriedad:**
> - `vehiculo` — `infraccion`: relación **1 a N**. Para `infraccion` es **obligatoria** (toda infracción debe tener vehículo). Para `vehiculo` es **opcional** (un vehículo puede no tener infracciones).
> - `camara` — `infraccion`: relación **1 a N**. Para `infraccion` es **obligatoria** (toda infracción debe tener cámara que la detectó). Para `camara` es **opcional** (una cámara puede no haber detectado infracciones aún).

---

## Ejercicio 2 — Llaves foráneas y cardinalidad de la tabla `pago` (con trampa)

**Keywords para buscar:** `pago`, `acreedor_id`, `propietario`, `cardinalidad`, `trampa`, `examen difícil`, `dos FKs`, `conceptual`

**Tipo de pregunta:** conceptual / ERD

**Dificultad:** media

**Tablas involucradas:**
- `pago`
- `infraccion`
- `propietario`

**Relaciones usadas del ERD:**
- `pago.infraccion_id → infraccion.id`
- `pago.acreedor_id → propietario.id`

**Patrones relacionados:**
- Variante de Ej. 1 pero con la trampa de que `acreedor_id` no tiene un nombre obvio.

**Trampas típicas:**
- Pensar que `acreedor_id` apunta a una entidad "acreedor" (no existe)
- Olvidar mencionar que el pago debe estar ligado obligatoriamente a una infracción

**Enunciado:**
Nombra las llaves foráneas que existen para la tabla `pago` del ERD de foto-multas. Indica la cardinalidad y obligatoriedad de las asociaciones que implementan estas FKs.

---

### Solución paso a paso

**1. Identificación de FKs en `pago`:**
- `infraccion_id` → referencia a `infraccion.id`
- `acreedor_id` → referencia a `propietario.id` ⚠️ **Nota**: a pesar del nombre "acreedor", apunta a la tabla `propietario` (representa al propietario que efectúa el pago de la multa).

**2. `infraccion` — `pago`:**
- Un **pago** está asociado a **una y solo una infracción** (obligatoria).
- Una **infracción** puede tener **cero, uno o muchos pagos** (opcional). Esto es lo que permite **pagos parciales**.

**3. `propietario` — `pago` (vía `acreedor_id`):**
- Un **pago** está realizado por **uno y solo un propietario** (obligatoria).
- Un **propietario** puede haber realizado **cero, uno o muchos pagos** (opcional).

---

### Respuesta concisa

> **FKs de `pago`:**
> - `infraccion_id` → `infraccion.id`
> - `acreedor_id` → `propietario.id`
>
> **Cardinalidad:**
> - `infraccion (1,1)` — `(0, N) pago`: obligatoria para pago, opcional para infracción (permite pagos parciales).
> - `propietario (1,1)` — `(0, N) pago` (vía `acreedor_id`): obligatoria para pago, opcional para propietario.

---

## Ejercicio 3 — Justificación ingenieril de PK artificial

**Keywords para buscar:** `PK artificial`, `surrogate key`, `placa`, `id`, `correo`, `UNIQUE`, `examen tipo`, `Q2`, `justificación ingenieril`

**Tipo de pregunta:** conceptual

**Dificultad:** media

**Tablas involucradas:**
- `vehiculo`

**Patrones relacionados:**
- Pregunta favorita del profesor sobre diseño físico
- Variante directa de la pregunta 2 del examen tipo final

**Trampas típicas:**
- Dar solo una razón ("es más rápido") sin explicar por qué
- Olvidar la razón de **estabilidad** (la razón #1 técnica)
- Confundir UNIQUE con PRIMARY KEY

**Enunciado:**
La tabla `vehiculo` cuenta con la columna `placa` que conceptualmente identifica de manera única a cada vehículo registrado en la CDMX. Indica en términos ingenieriles por qué o por qué no es conveniente agregar un identificador artificial `vehiculo.id` en lugar de emplear `vehiculo.placa` como llave primaria.

---

### Solución paso a paso

**Sí es conveniente** usar `vehiculo.id` artificial. Razones:

**1. Estabilidad (la más importante).**
La placa de un vehículo puede cambiar a lo largo del tiempo: re-emisión por daño, cambio de propietario en algunos esquemas, cambios regulatorios de la CDMX (por ejemplo, cuando se introducen formatos nuevos de placa). Si la placa fuera la PK, **cualquier cambio se propagaría** a todas las FKs que la referencian (`infraccion.vehiculo_id` debería ser `infraccion.placa`, etc.), provocando UPDATEs masivos y posibles inconsistencias. El `id` artificial **nunca cambia**.

**2. Tamaño e indexación.**
`placa VARCHAR(20)` ocupa hasta 20 bytes + overhead de longitud. `id BIGINT` ocupa solo 8 bytes. Esto importa porque:
- Los índices B-tree son **más pequeños** y caben más nodos en memoria.
- Las **lecturas son más rápidas** porque hay menos páginas que leer.
- Los **JOIN son más eficientes** porque comparar enteros es más barato que comparar strings.

**3. Privacidad y opacidad.**
La placa es información públicamente identificable. Exponerla en URLs, logs o errores facilita ataques. Un `id` opaco no revela información del vehículo ni del dueño.

**4. Independencia regulatoria.**
Si CDMX cambia el formato de placas (longitud, caracteres permitidos), el esquema interno **no se rompe**. Solo se actualiza el dato.

**5. Permite múltiples llaves candidatas.**
Puedes seguir poniendo `UNIQUE` a `placa` para garantizar su unicidad, pero **la PK queda independiente** de las decisiones de negocio.

---

### Respuesta concisa

> Conviene un `id` artificial por **estabilidad** (la placa puede cambiar y propagaría updates a todas las FKs), **tamaño compacto** (BIGINT 8 bytes vs VARCHAR(20) hasta 22 bytes, lo que mejora el tamaño de índices y velocidad de JOINs), **privacidad** (no expone info pública), e **independencia regulatoria** (cambios al formato de placa no rompen el esquema). Aun así, se puede mantener `UNIQUE` sobre `placa` para garantizar unicidad como llave candidata adicional.

---

## Ejercicio 4 — Verificación de FNBC tras agregar un atributo

**Keywords para buscar:** `FNBC`, `forma normal Boyce-Codd`, `agregar atributo`, `normalización`, `examen tipo`, `Q3`, `dependencia funcional`, `superllave`, `MUY difícil`

**Tipo de pregunta:** normalización

**Dificultad:** difícil

**Tablas involucradas:**
- `infraccion`

**Relaciones usadas del ERD:**
- Diseño conceptual de la relvar `infraccion`

**Patrones relacionados:**
- Variante directa de la Q3 del examen tipo
- Pregunta sobre estabilidad de FNBC ante cambios de esquema

**Trampas típicas:**
- Olvidar verificar si el nuevo atributo es **otra llave candidata** (superllave)
- Pensar que agregar un atributo siempre rompe la FN
- No verificar las DF nuevas que el atributo introduce

**Enunciado:**
La relvar `infraccion` cuenta originalmente con el siguiente encabezado:

$$E_{infraccion} = \{id, fecha, tipo, importe, vehiculo\_id, camara\_id\}$$

Y se demostró que se encuentra en FNBC. Los ingenieros añaden un nuevo atributo llamado `folio` (un código alfanumérico generado por una cámara cuando registra la multa). Se sabe que:

- `{id} → {fecha, tipo, importe, vehiculo_id, camara_id, folio}` (la PK determina todo)
- `{folio} → {id, fecha, tipo, importe, vehiculo_id, camara_id}` (el folio determina todo también, porque es único por diseño)

Asume que esas son todas las DF no triviales (más las implicadas). Indica si después de la adición de `folio`, la relvar `infraccion` continúa en FNBC.

---

### Solución paso a paso

**Paso 1: Encabezado nuevo.**
$$E' = \{id, fecha, tipo, importe, vehiculo\_id, camara\_id, folio\}$$

**Paso 2: Listar todas las DF no triviales explícitas.**
- DF1: `{id} → {fecha, tipo, importe, vehiculo_id, camara_id, folio}`
- DF2: `{folio} → {id, fecha, tipo, importe, vehiculo_id, camara_id}`

**Paso 3: Identificar llaves candidatas.**
Una llave candidata es un conjunto irreducible que es superllave (determina todos los atributos).
- `{id}` es superllave: determina todo (DF1).
- `{folio}` es superllave: determina todo (DF2, y por transitividad con DF1).
- ¿Hay otra? No hay información que lo sugiera.
- Las dos son **irreducibles** (cada una es un solo atributo).

→ **Llaves candidatas:** `{id}` y `{folio}`.

**Paso 4: Verificar FNBC.**
**FNBC**: toda DF no trivial sale de superllave.

- DF1: lado izquierdo `{id}` → es superllave ✅
- DF2: lado izquierdo `{folio}` → es superllave ✅

Todas las DF no triviales salen de superllaves.

**Paso 5: Conclusión.**
La relvar `infraccion` **sigue en FNBC** después de agregar `folio`.

---

### Respuesta concisa

> Sí, **sigue en FNBC**. Las DF que introduce el nuevo atributo (`{id} → ...folio` y `{folio} → ...`) tienen ambas lados izquierdos que son superllaves (`{id}` es la PK original, y `{folio}` se convierte en una **nueva llave candidata** porque determina todos los atributos). Toda DF no trivial sigue saliendo de superllaves, por lo que la condición de FNBC se mantiene.

---

## Ejercicio 5 — Identificación de DF y DMV triviales

**Keywords para buscar:** `DF trivial`, `DMV trivial`, `dependencia funcional trivial`, `dependencia multivaluada`, `Q5`, `examen tipo`, `normalización`, `subset`

**Tipo de pregunta:** normalización / conceptual

**Dificultad:** difícil

**Tablas involucradas:**
- `infraccion`, `vehiculo`, `pago`

**Patrones relacionados:**
- Pregunta directa del examen tipo (Q5)
- Identificar trivialidad

**Trampas típicas:**
- Confundir definición de DF trivial con DMV trivial
- Para DMV, olvidar la segunda condición (X ∪ Y = E)
- Pensar que "trivial" significa "obvia" o "cierta"; significa **se cumple automáticamente**

**Enunciado:**
Indica y justifica cuáles de las siguientes dependencias funcionales y multivaluadas son **triviales**, considerando los encabezados respectivos del ERD de foto-multas. Asume que el encabezado de cada relvar es el listado completo de columnas en el ERD.

i. `{id, vehiculo_id} → {vehiculo_id, id}` con respecto a $E_{infraccion}$
ii. `{placa} → {marca, anio}` con respecto a $E_{vehiculo}$
iii. `{infraccion_id, importe} → {importe}` con respecto a $E_{pago}$
iv. `{acreedor_id} ↠ {id, fecha, importe, infraccion_id}` con respecto a $E_{pago}$
v. `{id} ↠ {placa}` con respecto a $E_{vehiculo}$
vi. `{vehiculo_id, camara_id} → {tipo}` con respecto a $E_{infraccion}$

---

### Solución paso a paso

**Recordatorio:**
- **DF $X \to Y$ trivial** sii $Y \subseteq X$.
- **DMV $X \twoheadrightarrow Y$ trivial** sii $Y \subseteq X$ **O** $X \cup Y = E$.

---

**i. `{id, vehiculo_id} → {vehiculo_id, id}`** con $E_{infraccion} = \{id, fecha, tipo, importe, vehiculo\_id, camara\_id\}$
- ¿$\{vehiculo\_id, id\} \subseteq \{id, vehiculo\_id\}$? Sí (son el mismo conjunto).
- ✅ **TRIVIAL**.

---

**ii. `{placa} → {marca, anio}`** con $E_{vehiculo} = \{id, placa, marca, anio, color, propietario\_id\}$
- ¿$\{marca, anio\} \subseteq \{placa\}$? No.
- ❌ **NO TRIVIAL**.

(Adicional: probablemente esta DF tampoco se mantiene, ya que dos vehículos con la misma marca podrían tener placas distintas y el ejemplo es genérico.)

---

**iii. `{infraccion_id, importe} → {importe}`** con $E_{pago} = \{id, fecha, importe, infraccion\_id, acreedor\_id\}$
- ¿$\{importe\} \subseteq \{infraccion\_id, importe\}$? Sí.
- ✅ **TRIVIAL**.

---

**iv. `{acreedor_id} ↠ {id, fecha, importe, infraccion_id}`** con $E_{pago} = \{id, fecha, importe, infraccion\_id, acreedor\_id\}$
- Condición A: ¿$\{id, fecha, importe, infraccion\_id\} \subseteq \{acreedor\_id\}$? No.
- Condición B: ¿$\{acreedor\_id\} \cup \{id, fecha, importe, infraccion\_id\} = E_{pago}$?
  - $\{acreedor\_id, id, fecha, importe, infraccion\_id\} = E_{pago}$? Sí (contiene los 5 atributos).
- ✅ **TRIVIAL** (por la condición B).

---

**v. `{id} ↠ {placa}`** con $E_{vehiculo} = \{id, placa, marca, anio, color, propietario\_id\}$
- Condición A: ¿$\{placa\} \subseteq \{id\}$? No.
- Condición B: ¿$\{id\} \cup \{placa\} = E_{vehiculo}$? $\{id, placa\}$ vs los 6 atributos: No.
- ❌ **NO TRIVIAL**.

(Adicional: esta DMV sí se mantiene en `vehiculo` porque `id` es PK y determina todo, pero ese análisis es independiente de la trivialidad.)

---

**vi. `{vehiculo_id, camara_id} → {tipo}`** con $E_{infraccion} = \{id, fecha, tipo, importe, vehiculo\_id, camara\_id\}$
- ¿$\{tipo\} \subseteq \{vehiculo\_id, camara\_id\}$? No.
- ❌ **NO TRIVIAL**.

---

### Resumen final

| # | Tipo | ¿Trivial? | Razón |
|---|---|---|---|
| i | DF | ✅ Sí | $\{vehiculo\_id, id\} \subseteq \{id, vehiculo\_id\}$ |
| ii | DF | ❌ No | $\{marca, anio\} \not\subseteq \{placa\}$ |
| iii | DF | ✅ Sí | $\{importe\} \subseteq \{infraccion\_id, importe\}$ |
| iv | DMV | ✅ Sí | $X \cup Y = E_{pago}$ (los dos lados cubren todo el encabezado) |
| v | DMV | ❌ No | Ni $Y \subseteq X$ ni $X \cup Y = E$ |
| vi | DF | ❌ No | $\{tipo\} \not\subseteq \{vehiculo\_id, camara\_id\}$ |

---

## Ejercicio 6 — Soluciones desde el DBMS para datos inválidos y consultas lentas

**Keywords para buscar:** `CHECK constraint`, `índice`, `validación`, `optimización`, `examen tipo`, `Q4`, `lentitud`, `fecha futura`, `trigger`, `B-tree`

**Tipo de pregunta:** conceptual / optimización

**Dificultad:** media

**Tablas involucradas:**
- `infraccion`

**Patrones relacionados:**
- Pregunta de "diagnóstico ingenieril" típica
- Variante directa de Q4 del examen tipo

**Trampas típicas:**
- Proponer solo soluciones de aplicación, no del DBMS
- Olvidar mencionar B-tree vs Hash al hablar de índices con ORDER BY
- Confundir CHECK constraint con NOT NULL

**Enunciado:**
Los ingenieros del sistema de foto-multas han detectado dos problemas en la tabla `infraccion`:

1. **Valores inválidos en `fecha`**: ocasionalmente se registran valores imposibles, como fechas en el futuro o fechas de antes del despliegue del sistema (digamos antes del 1 de enero de 2018). El atributo debe contener la fecha-hora exacta en que la cámara detectó la infracción.

2. **Consultas lentas al buscar infracciones por vehículo**: el portal web del gobierno tarda mucho cuando un ciudadano consulta las infracciones de su vehículo, mostradas en orden descendente por `fecha`.

Explica (sin usar código) qué acciones se pueden realizar desde el manejador o el esquema para atender estos problemas.

---

### Solución paso a paso

**Problema 1: Valores inválidos en `fecha`.**

Se pueden tomar dos rutas desde el DBMS:

**Opción A — `CHECK` constraint (preferida por simplicidad):**
Agregar una restricción que valide que `fecha` esté dentro del rango permitido:
- La fecha no puede ser mayor a la fecha actual (`NOW()` o `CURRENT_TIMESTAMP`).
- La fecha no puede ser anterior al inicio del sistema (`'2018-01-01'`).

Esta restricción se evalúa automáticamente en cada INSERT y UPDATE. Si una tupla la viola, el DBMS lanza un error y la operación se aborta.

**Opción B — Trigger:**
Crear un trigger `BEFORE INSERT OR UPDATE` que valide la fecha. Útil si la lógica es más compleja (por ejemplo, debe consultar otras tablas o aplicar reglas dinámicas). Para validaciones simples como esta, **el CHECK es más eficiente y más declarativo**.

**Por qué desde el DBMS, no desde la aplicación:** garantiza la integridad **incluso si la inserción viene de otro cliente** (script Python, otra API, conexión directa). La aplicación puede tener bugs; el DBMS es la última línea de defensa.

---

**Problema 2: Consultas lentas con ORDER BY descendente sobre `fecha` filtrando por `vehiculo_id`.**

**Solución: crear un índice B-tree compuesto sobre `(vehiculo_id, fecha DESC)`.**

Razones:
- Las consultas filtran por `vehiculo_id = X` → un índice sobre esa columna acelera el filtro (de O(N) a O(log N)).
- Luego ordenan por `fecha DESC` → si el índice ya incluye `fecha`, el DBMS puede **leer directamente en el orden necesario** sin ordenar.
- **B-tree** (no Hash), porque hash no soporta ORDER BY ni rangos.
- Compuesto con `vehiculo_id` primero porque ese es el filtro de igualdad (mejor selectividad inicial), luego `fecha` para el orden.

Adicionalmente, si la tabla es muy grande y muchos vehículos rara vez se consultan, puede considerarse un **índice parcial** filtrado por algún criterio (ej. solo infracciones del último año), pero esto depende del patrón de uso.

---

### Respuesta concisa

> **Problema 1**: añadir un `CHECK constraint` en `infraccion` que valide `fecha BETWEEN '2018-01-01' AND NOW()` (o usar un trigger BEFORE INSERT/UPDATE para validaciones más complejas). El DBMS rechazará automáticamente cualquier tupla con fecha inválida.
>
> **Problema 2**: crear un **índice B-tree compuesto** sobre `(vehiculo_id, fecha DESC)`. Esto acelera tanto el filtro por vehículo como el ordenamiento descendente por fecha, evitando un sort en memoria.

---

## Ejercicio 7 — DFs triviales en `vehiculo`

**Keywords para buscar:** `DF trivial`, `subconjunto`, `vehiculo`, `vehicular`, `examen difícil`, `fundamentos`

**Tipo de pregunta:** normalización / conceptual

**Dificultad:** fácil-media

**Tablas involucradas:**
- `vehiculo`

**Patrones relacionados:**
- Forma simplificada de Ej. 5 para repaso de conceptos

**Trampas típicas:**
- Pensar que toda DF que "se cumple" es trivial (cumplir ≠ trivial)
- No verificar inclusión literal del lado derecho

**Enunciado:**
Considerando $E_{vehiculo} = \{id, placa, marca, anio, color, propietario\_id\}$, indica cuáles de las siguientes DF son triviales:

a. `{placa} → {placa}`
b. `{id, placa} → {marca}`
c. `{marca, anio, color} → {marca, color}`
d. `{id} → {placa, marca, anio, color, propietario_id}`
e. `{propietario_id, color} → {color, propietario_id}`

---

### Solución paso a paso

**a.** `{placa} → {placa}`: ¿$\{placa\} \subseteq \{placa\}$? Sí. ✅ **Trivial**.

**b.** `{id, placa} → {marca}`: ¿$\{marca\} \subseteq \{id, placa\}$? No. ❌ **NO trivial** (de hecho, esta DF tampoco se sostiene en general: hay vehículos del mismo id pero "marca" no es función de placa).

**c.** `{marca, anio, color} → {marca, color}`: ¿$\{marca, color\} \subseteq \{marca, anio, color\}$? Sí. ✅ **Trivial**.

**d.** `{id} → {placa, marca, anio, color, propietario_id}`: ¿$\{placa, marca, anio, color, propietario\_id\} \subseteq \{id\}$? No. ❌ **NO trivial** (es la DF de la PK; **se sostiene** pero no es trivial).

**e.** `{propietario_id, color} → {color, propietario_id}`: ¿$\{color, propietario\_id\} \subseteq \{propietario\_id, color\}$? Sí (mismos elementos). ✅ **Trivial**.

---

### Tabla resumen

| Inciso | ¿Trivial? |
|---|---|
| a | ✅ Sí |
| b | ❌ No |
| c | ✅ Sí |
| d | ❌ No |
| e | ✅ Sí |

> 💡 **Lección clave**: si en un examen ves `X → Y` donde **los elementos de Y aparecen entre los de X**, marca trivial inmediatamente.

---

## Ejercicio 8 — DMVs triviales en `pago`

**Keywords para buscar:** `DMV trivial`, `dependencia multivaluada`, `pago`, `encabezado completo`, `condición B`

**Tipo de pregunta:** normalización

**Dificultad:** media-difícil

**Tablas involucradas:**
- `pago`

**Patrones relacionados:**
- Aplicación directa de las dos condiciones de DMV trivial

**Trampas típicas:**
- Olvidar la segunda condición ($X \cup Y = E$)
- Confundir DMV con DF (DMV es más permisiva con la trivialidad)

**Enunciado:**
Considerando $E_{pago} = \{id, fecha, importe, infraccion\_id, acreedor\_id\}$, indica cuáles de las siguientes DMV son triviales:

a. `{id} ↠ {id, fecha}`
b. `{id} ↠ {fecha, importe, infraccion_id, acreedor_id}`
c. `{fecha} ↠ {importe}`
d. `{infraccion_id} ↠ {id, importe}`
e. `{acreedor_id, fecha} ↠ {id, importe, infraccion_id}`

---

### Solución paso a paso

**Recordatorio:** DMV $X \twoheadrightarrow Y$ es **trivial** sii $Y \subseteq X$ **O** $X \cup Y = E$.

---

**a.** `{id} ↠ {id, fecha}`:
- Condición A: ¿$\{id, fecha\} \subseteq \{id\}$? No.
- Condición B: ¿$\{id\} \cup \{id, fecha\} = E_{pago}$? $\{id, fecha\}$ vs 5 atributos: No.
- ❌ **NO trivial**.

---

**b.** `{id} ↠ {fecha, importe, infraccion_id, acreedor_id}`:
- Condición A: ¿$\{fecha, importe, infraccion\_id, acreedor\_id\} \subseteq \{id\}$? No.
- Condición B: ¿$\{id\} \cup \{fecha, importe, infraccion\_id, acreedor\_id\} = E_{pago}$? Sí, contiene los 5 atributos.
- ✅ **Trivial** (por condición B).

---

**c.** `{fecha} ↠ {importe}`:
- Condición A: ¿$\{importe\} \subseteq \{fecha\}$? No.
- Condición B: ¿$\{fecha, importe\} = E_{pago}$? No, faltan 3 atributos.
- ❌ **NO trivial**.

---

**d.** `{infraccion_id} ↠ {id, importe}`:
- Condición A: ¿$\{id, importe\} \subseteq \{infraccion\_id\}$? No.
- Condición B: ¿$\{infraccion\_id, id, importe\} = E_{pago}$? No, faltan `fecha` y `acreedor_id`.
- ❌ **NO trivial**.

---

**e.** `{acreedor_id, fecha} ↠ {id, importe, infraccion_id}`:
- Condición A: ¿$\{id, importe, infraccion\_id\} \subseteq \{acreedor\_id, fecha\}$? No.
- Condición B: ¿$\{acreedor\_id, fecha, id, importe, infraccion\_id\} = E_{pago}$? Sí (los 5 atributos).
- ✅ **Trivial** (por condición B).

---

### Resumen

| Inciso | ¿Trivial? | Razón |
|---|---|---|
| a | ❌ No | — |
| b | ✅ Sí | Condición B (X ∪ Y = E) |
| c | ❌ No | — |
| d | ❌ No | Falta `fecha` y `acreedor_id` |
| e | ✅ Sí | Condición B |

---

## Ejercicio 9 — JOIN básico con ORDER BY (consulta de infracciones)

**Keywords para buscar:** `INNER JOIN`, `ORDER BY`, `SELECT`, `infraccion`, `vehiculo`, `propietario`, `examen tipo`, `Q6`, `básico`

**Tipo de pregunta:** SQL

**Dificultad:** fácil-media

**Tablas involucradas:**
- `infraccion`
- `vehiculo`
- `propietario`

**Relaciones usadas del ERD:**
- `infraccion.vehiculo_id → vehiculo.id`
- `vehiculo.propietario_id → propietario.id`

**Patrones relacionados:**
- Variante directa de Q6 del examen tipo
- Encadenamiento de 3 tablas vía FKs

**Trampas típicas:**
- Omitir el filtro `WHERE` y devolver todas las infracciones
- Olvidar prefijar columnas que existen en varias tablas (`fecha`, `importe`)
- Confundir orden ASC vs DESC

**Enunciado:**
Se desean mostrar todos las infracciones registradas para el vehículo con `id = 50`. Escribe una consulta que devuelva la fecha de la infracción, el tipo, el importe, así como el nombre y apellido del propietario del vehículo, ordenando los resultados de forma descendente usando la fecha. La relación resultante tendrá las siguientes columnas:

`fecha | tipo | importe | nombre | apellido`

---

### Solución paso a paso

**1. Identificar columnas pedidas:**
- `fecha`, `tipo`, `importe` → vienen de `infraccion`.
- `nombre`, `apellido` → vienen de `propietario`.

**2. Trazar el camino de FKs:**
`infraccion` ─→ `vehiculo` ─→ `propietario`.

**3. Filtro:** `infraccion.vehiculo_id = 50` (o `vehiculo.id = 50`; son equivalentes vía el JOIN).

**4. Tipo de JOIN:**
- ¿Quiero infracciones sin vehículo? No (vehículo es obligatorio para infracción).
- ¿Quiero infracciones sin propietario? El vehículo siempre tiene propietario.
- → **INNER JOIN** está bien.

**5. Orden:** `ORDER BY infraccion.fecha DESC`.

---

### Query final

```sql
SELECT 
    infraccion.fecha,
    infraccion.tipo,
    infraccion.importe,
    propietario.nombre,
    propietario.apellido
FROM infraccion
INNER JOIN vehiculo 
    ON infraccion.vehiculo_id = vehiculo.id
INNER JOIN propietario 
    ON vehiculo.propietario_id = propietario.id
WHERE infraccion.vehiculo_id = 50
ORDER BY infraccion.fecha DESC;
```

---

### Explicación de la query

- `FROM infraccion`: arrancamos de la tabla central.
- `INNER JOIN vehiculo ON infraccion.vehiculo_id = vehiculo.id`: vinculamos cada infracción con su vehículo.
- `INNER JOIN propietario ON vehiculo.propietario_id = propietario.id`: vinculamos el vehículo con su dueño.
- `WHERE infraccion.vehiculo_id = 50`: filtramos al vehículo objetivo. (También podríamos usar `WHERE vehiculo.id = 50` con idéntico resultado.)
- `ORDER BY infraccion.fecha DESC`: la más reciente primero.

> 💡 **Alternativa**: `WHERE vehiculo.id = 50` es 100% equivalente porque el INNER JOIN forzó la igualdad. Cualquiera de las dos formas es aceptada.

---

## Ejercicio 10 — JOIN con filtro por fecha y formato

**Keywords para buscar:** `INNER JOIN`, `WHERE`, `EXTRACT YEAR`, `ORDER BY`, `LIMIT`, `multas`, `fecha rango`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Tablas involucradas:**
- `infraccion`, `vehiculo`, `propietario`

**Patrones relacionados:**
- Combinación de filtros sobre fechas con multiplicación de tablas

**Trampas típicas:**
- Usar `BETWEEN` con fechas inclusivas/exclusivas incorrectas
- Cuando filtras por año, una alternativa es `EXTRACT(YEAR FROM fecha) = 2024`

**Enunciado:**
Devuelve el correo, nombre y apellido de los propietarios que recibieron alguna infracción durante el año 2024. No quieres duplicados (si un propietario tiene 5 multas, debe aparecer 1 vez). Ordena alfabéticamente por apellido y luego por nombre.

Columnas esperadas: `correo | nombre | apellido`

---

### Solución paso a paso

1. Identifica las tablas: `propietario`, `vehiculo`, `infraccion`.
2. Filtro: `EXTRACT(YEAR FROM infraccion.fecha) = 2024` o equivalente con rango `BETWEEN '2024-01-01' AND '2024-12-31 23:59:59.999999'`.
3. Necesito eliminar duplicados → `DISTINCT`.
4. Orden: `ORDER BY apellido, nombre`.

---

### Query final

```sql
SELECT DISTINCT
    propietario.correo,
    propietario.nombre,
    propietario.apellido
FROM propietario
INNER JOIN vehiculo 
    ON propietario.id = vehiculo.propietario_id
INNER JOIN infraccion 
    ON vehiculo.id = infraccion.vehiculo_id
WHERE infraccion.fecha >= '2024-01-01'
  AND infraccion.fecha <  '2025-01-01'
ORDER BY propietario.apellido, propietario.nombre;
```

---

### Explicación de la query

- `DISTINCT` elimina duplicados (un propietario aparece N veces sin esto si tiene N multas).
- `infraccion.fecha >= '2024-01-01' AND infraccion.fecha < '2025-01-01'` es **preferible** a `EXTRACT(YEAR FROM infraccion.fecha) = 2024` porque permite usar índices sobre `fecha` (la función `EXTRACT` impide el uso del índice salvo que sea un índice de expresión).
- El `ORDER BY` actúa después del DISTINCT, ordenando el resultado final.

---

## Ejercicio 11 — GROUP BY + HAVING (vehículos con muchas multas)

**Keywords para buscar:** `GROUP BY`, `HAVING`, `COUNT`, `umbral`, `examen tipo`, `Q7`, `al menos N`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Tablas involucradas:**
- `infraccion`, `vehiculo`

**Patrones relacionados:**
- Patrón clásico "X con al menos N de Y"
- Variante directa de Q7 del examen tipo

**Trampas típicas:**
- Poner el COUNT en WHERE en vez de HAVING
- No incluir todas las columnas no-agregadas en GROUP BY
- Olvidar que COUNT(*) y COUNT(infraccion.id) pueden diferir si hay LEFT JOIN

**Enunciado:**
La CDMX quiere identificar a los vehículos "habituales infractores": aquellos con al menos 5 infracciones registradas en el sistema. Escribe una consulta que devuelva el `id` del vehículo y el número de infracciones que tiene.

Columnas esperadas: `vehiculo_id | no_infracciones`

---

### Solución paso a paso

1. Necesito agrupar por vehículo.
2. Para cada grupo, contar infracciones.
3. Filtrar grupos con conteo ≥ 5.
4. No necesito JOIN si la FK `vehiculo_id` ya está en `infraccion`.

---

### Query final

```sql
SELECT 
    infraccion.vehiculo_id,
    COUNT(*) AS no_infracciones
FROM infraccion
GROUP BY infraccion.vehiculo_id
HAVING COUNT(*) >= 5;
```

---

### Explicación de la query

- `FROM infraccion`: solo necesito esta tabla porque tiene la FK `vehiculo_id`.
- `GROUP BY infraccion.vehiculo_id`: agrupa todas las infracciones de cada vehículo.
- `COUNT(*)`: cuenta tuplas de cada grupo.
- `HAVING COUNT(*) >= 5`: filtra grupos con ≥ 5 infracciones.

> 🚨 **Trampa común**: si te piden incluir más datos del vehículo (placa, marca), tienes que JOIN con `vehiculo` y agregar esas columnas al GROUP BY:
> ```sql
> SELECT vehiculo.id, vehiculo.placa, COUNT(*) AS no_infracciones
> FROM vehiculo
> INNER JOIN infraccion ON vehiculo.id = infraccion.vehiculo_id
> GROUP BY vehiculo.id, vehiculo.placa
> HAVING COUNT(*) >= 5;
> ```

---

## Ejercicio 12 — GROUP BY + HAVING con SUM (multas no pagadas completamente)

**Keywords para buscar:** `GROUP BY`, `HAVING`, `SUM`, `LEFT JOIN`, `COALESCE`, `pagos parciales`, `morosos`, `MUY difícil`

**Tipo de pregunta:** SQL

**Dificultad:** difícil

**Tablas involucradas:**
- `infraccion`, `pago`

**Patrones relacionados:**
- Comparación entre suma agregada y un valor en la tabla externa
- `LEFT JOIN` + `COALESCE` para manejar infracciones sin pagos

**Trampas típicas:**
- INNER JOIN excluye infracciones sin ningún pago (¡las más importantes!)
- SUM(NULL) es NULL → necesitas COALESCE
- Confundir "no pagada totalmente" con "no pagada en absoluto"

**Enunciado:**
Devuelve el `id` de cada infracción cuyo total pagado es **menor** al importe original. Incluye también infracciones que no tienen ningún pago registrado. Devuelve además el importe original, el total pagado (o 0) y el saldo pendiente.

Columnas esperadas: `infraccion_id | importe | total_pagado | saldo_pendiente`

---

### Solución paso a paso

1. Cada infracción tiene 0 ó más pagos.
2. Necesito sumar los pagos por infracción.
3. Una infracción sin pagos debe aparecer (con total_pagado = 0).
4. → Uso `LEFT JOIN pago`.
5. Uso `COALESCE(SUM(pago.importe), 0)` para que NULL → 0.
6. Filtro HAVING: `COALESCE(SUM(pago.importe), 0) < infraccion.importe`.

---

### Query final

```sql
SELECT 
    infraccion.id AS infraccion_id,
    infraccion.importe,
    COALESCE(SUM(pago.importe), 0) AS total_pagado,
    infraccion.importe - COALESCE(SUM(pago.importe), 0) AS saldo_pendiente
FROM infraccion
LEFT JOIN pago 
    ON pago.infraccion_id = infraccion.id
GROUP BY infraccion.id, infraccion.importe
HAVING COALESCE(SUM(pago.importe), 0) < infraccion.importe;
```

---

### Explicación de la query

- `LEFT JOIN pago` garantiza que las infracciones sin pagos también aparezcan (con `pago.importe = NULL`).
- `COALESCE(SUM(pago.importe), 0)`: si no hay pagos, SUM devolvería NULL; lo convertimos a 0.
- `GROUP BY infraccion.id, infraccion.importe`: hay que incluir `importe` porque está en SELECT no agregado.
- `HAVING ... < infraccion.importe`: comparamos el total pagado con el importe original.

> 💡 **Variante extrema (truco)**: si quieres infracciones con cero pagos solamente, usa `NOT EXISTS`:
> ```sql
> SELECT * FROM infraccion i
> WHERE NOT EXISTS (SELECT 1 FROM pago p WHERE p.infraccion_id = i.id);
> ```

---

## Ejercicio 13 — Top N con SUM (cámaras más recaudadoras)

**Keywords para buscar:** `GROUP BY`, `SUM`, `ORDER BY`, `LIMIT`, `top N`, `examen tipo`, `Q8`, `recaudación`

**Tipo de pregunta:** SQL

**Dificultad:** media-difícil

**Tablas involucradas:**
- `camara`, `infraccion`, `pago`

**Patrones relacionados:**
- Variante directa de Q8 del examen tipo
- Cadena de 3 tablas con agregación

**Trampas típicas:**
- Sumar `infraccion.importe` cuando realmente recaudado es lo pagado (`pago.importe`)
- Usar INNER JOIN con pagos puede excluir infracciones impagas (ok aquí porque interesa recaudación, no infracciones)
- Olvidar el LIMIT
- No agrupar correctamente

**Enunciado:**
La SSC quiere saber cuáles son las 10 cámaras que han recaudado más dinero en pagos efectivamente realizados. Devuelve el `id`, tipo y alcaldía de la cámara, así como la suma total recaudada en pagos. Si hay empate en la posición 10, devuelve todas las cámaras empatadas.

Consideraciones:
- Solo cuentan los pagos efectivamente registrados (tabla `pago`).
- Una infracción puede tener varios pagos parciales.

Columnas esperadas: `camara_id | tipo | alcaldia | total_recaudado`

---

### Solución paso a paso

1. La recaudación está en `pago.importe`, no en `infraccion.importe`.
2. Cadena: `pago → infraccion → camara`.
3. Agrupo por cámara (incluyendo `tipo` y `alcaldia` en el GROUP BY porque están en SELECT no agregado).
4. `SUM(pago.importe)`.
5. ORDER BY DESC, y para empates en la posición 10 → usar `RANK()` o `DENSE_RANK()` con window function en lugar de LIMIT.

---

### Query final

```sql
WITH recaudacion_por_camara AS (
    SELECT 
        camara.id AS camara_id,
        camara.tipo,
        camara.alcaldia,
        SUM(pago.importe) AS total_recaudado
    FROM camara
    INNER JOIN infraccion 
        ON camara.id = infraccion.camara_id
    INNER JOIN pago 
        ON pago.infraccion_id = infraccion.id
    GROUP BY camara.id, camara.tipo, camara.alcaldia
),
ranked AS (
    SELECT *,
           DENSE_RANK() OVER (ORDER BY total_recaudado DESC) AS rk
    FROM recaudacion_por_camara
)
SELECT camara_id, tipo, alcaldia, total_recaudado
FROM ranked
WHERE rk <= 10
ORDER BY total_recaudado DESC;
```

---

### Explicación de la query

- **CTE `recaudacion_por_camara`**: calcula la recaudación por cámara.
  - `INNER JOIN`: solo nos interesan cámaras con al menos un pago.
  - `GROUP BY` incluye todas las columnas no agregadas.
- **CTE `ranked`**: usa `DENSE_RANK()` sobre el total recaudado descendente. `DENSE_RANK` da el mismo número a empates sin saltar (1, 2, 2, 3).
- **Resultado final**: filtra `rk <= 10` para incluir empates en la décima posición.

> 💡 **Variante simple (si no me importan empates exactos)**:
> ```sql
> SELECT camara.id, camara.tipo, camara.alcaldia, SUM(pago.importe) AS total_recaudado
> FROM camara
> INNER JOIN infraccion ON camara.id = infraccion.camara_id
> INNER JOIN pago ON pago.infraccion_id = infraccion.id
> GROUP BY camara.id, camara.tipo, camara.alcaldia
> ORDER BY total_recaudado DESC
> LIMIT 10;
> ```
> Pero **si dicen "no hay problema en empate en la posición 10"** se espera la versión con DENSE_RANK/RANK.

---

## Ejercicio 14 — Top N propietarios más infraccionados

**Keywords para buscar:** `GROUP BY`, `COUNT`, `ORDER BY DESC`, `LIMIT`, `top`, `propietario`, `morosos`

**Tipo de pregunta:** SQL

**Dificultad:** media

**Tablas involucradas:**
- `propietario`, `vehiculo`, `infraccion`

**Patrones relacionados:**
- Top-N con cadena de 3 tablas

**Trampas típicas:**
- Olvidar incluir el nombre y apellido del propietario en GROUP BY
- Confundir COUNT(*) con COUNT(DISTINCT)

**Enunciado:**
Devuelve los 5 propietarios que más infracciones han acumulado (sumando entre todos los vehículos a su nombre). Devuelve `id`, `nombre`, `apellido` y el número total de infracciones. Ordena descendente por número.

---

### Query final

```sql
SELECT 
    propietario.id,
    propietario.nombre,
    propietario.apellido,
    COUNT(infraccion.id) AS no_infracciones
FROM propietario
INNER JOIN vehiculo 
    ON propietario.id = vehiculo.propietario_id
INNER JOIN infraccion 
    ON vehiculo.id = infraccion.vehiculo_id
GROUP BY propietario.id, propietario.nombre, propietario.apellido
ORDER BY no_infracciones DESC
LIMIT 5;
```

---

### Explicación de la query

- INNER JOIN porque solo me interesan propietarios CON al menos una infracción.
- `COUNT(infraccion.id)` es equivalente a `COUNT(*)` aquí porque `infraccion.id` es NOT NULL (es PK).
- `GROUP BY` incluye los 3 atributos de SELECT no agregados.

---

## Ejercicio 15 — Window function: ranking dentro de partición (Top vehículo por alcaldía)

**Keywords para buscar:** `window function`, `RANK`, `PARTITION BY`, `ORDER BY OVER`, `top por grupo`, `MUY difícil`, `subquery`

**Tipo de pregunta:** SQL

**Dificultad:** muy difícil

**Tablas involucradas:**
- `camara`, `infraccion`, `vehiculo`

**Patrones relacionados:**
- "Top N por categoría" → clásico de window functions
- `RANK() OVER (PARTITION BY ...)` para limitar por grupo

**Trampas típicas:**
- Usar GROUP BY simple devuelve un solo top global, no por grupo
- LIMIT 1 no funciona aquí (querría 1 por alcaldía, no 1 global)

**Enunciado:**
Para cada alcaldía, devuelve el vehículo (id y placa) que recibió más infracciones detectadas por las cámaras de esa alcaldía, junto con el número de infracciones. Si hay empate en la primera posición de una alcaldía, incluye todos los empatados.

Columnas esperadas: `alcaldia | vehiculo_id | placa | no_infracciones`

---

### Solución paso a paso

1. Necesito infracciones por (alcaldía, vehículo).
2. Para cada alcaldía, encontrar el vehículo con máximo conteo.
3. Patrón: agrupar primero, luego rankear con `RANK() OVER (PARTITION BY alcaldía ORDER BY conteo DESC)`.
4. Tomar solo `rank = 1`.

---

### Query final

```sql
WITH conteo_por_alcaldia_vehiculo AS (
    SELECT 
        camara.alcaldia,
        infraccion.vehiculo_id,
        COUNT(*) AS no_infracciones
    FROM camara
    INNER JOIN infraccion ON camara.id = infraccion.camara_id
    GROUP BY camara.alcaldia, infraccion.vehiculo_id
),
ranked AS (
    SELECT *,
           RANK() OVER (PARTITION BY alcaldia ORDER BY no_infracciones DESC) AS rk
    FROM conteo_por_alcaldia_vehiculo
)
SELECT 
    ranked.alcaldia,
    ranked.vehiculo_id,
    vehiculo.placa,
    ranked.no_infracciones
FROM ranked
INNER JOIN vehiculo ON vehiculo.id = ranked.vehiculo_id
WHERE rk = 1
ORDER BY ranked.alcaldia, ranked.no_infracciones DESC;
```

---

### Explicación de la query

- **CTE 1**: agrupa por (alcaldía, vehículo) y cuenta infracciones.
- **CTE 2**: dentro de cada alcaldía, ordena descendente por conteo y asigna ranking. `RANK()` da el mismo número a empates.
- **SELECT final**: filtra `rk = 1` para quedarte con el top de cada alcaldía. JOIN con `vehiculo` para traer la `placa`.

> 💡 **Si quisieras top 3 por alcaldía**: cambia `WHERE rk = 1` a `WHERE rk <= 3`.

---

## Ejercicio 16 — Window function: running count (infracciones acumuladas por vehículo por mes)

**Keywords para buscar:** `window function`, `running count`, `EXTRACT MONTH`, `COUNT OVER PARTITION BY`, `examen tipo`, `Q9`, `MUY difícil`

**Tipo de pregunta:** SQL

**Dificultad:** muy difícil

**Tablas involucradas:**
- `infraccion`

**Patrones relacionados:**
- Variante directa de Q9 del examen tipo
- Función de ventana con frame ROWS BETWEEN UNBOUNDED PRECEDING

**Trampas típicas:**
- Confundir COUNT(*) sin OVER (colapsa) con COUNT(*) OVER (no colapsa)
- Olvidar el ORDER BY dentro del OVER → ranking aleatorio
- No particionar por mes → cuenta global en vez de mensual

**Enunciado:**
Para cada tupla en la tabla `infraccion`, devuelve cuántas infracciones tenía el vehículo correspondiente hasta ese momento dentro del mismo mes. Es decir, si un vehículo tuvo 3 infracciones en marzo, la primera muestra "1", la segunda "2", la tercera "3".

Considera:
- Usa `EXTRACT(MONTH FROM fecha)` para obtener el mes.
- Para considerar también el año, particiona por año y mes.
- La forma más sencilla es con una función de ventana.

Columnas esperadas: `id | fecha | vehiculo_id | no_infracciones_acumuladas_en_el_mes`

---

### Solución paso a paso

1. Quiero un valor por cada fila (no colapsar) → **window function**.
2. La partición es por `(vehiculo, año, mes)`.
3. El orden interno es por `fecha` ascendente.
4. La función: `COUNT(*)` sobre el frame que va desde el inicio hasta la fila actual.

---

### Query final

```sql
SELECT 
    id,
    fecha,
    vehiculo_id,
    COUNT(*) OVER (
        PARTITION BY 
            vehiculo_id, 
            EXTRACT(YEAR FROM fecha), 
            EXTRACT(MONTH FROM fecha)
        ORDER BY fecha
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS no_infracciones_acumuladas_en_el_mes
FROM infraccion
ORDER BY vehiculo_id, fecha;
```

---

### Explicación de la query

- `PARTITION BY vehiculo_id, EXTRACT(YEAR FROM fecha), EXTRACT(MONTH FROM fecha)`: una partición distinta por cada (vehículo, año, mes).
- `ORDER BY fecha`: dentro de cada partición, ordena cronológicamente.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: el frame va desde el inicio de la partición hasta la fila actual (inclusive).
- `COUNT(*) OVER (...)`: cuenta filas en ese frame → da el conteo acumulado.

> 💡 **Variante con DATE_TRUNC** (más limpia):
> ```sql
> COUNT(*) OVER (
>     PARTITION BY vehiculo_id, DATE_TRUNC('month', fecha)
>     ORDER BY fecha
>     ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
> )
> ```

> 🚨 **Sin el frame clause explícito**: cuando hay `ORDER BY` en la ventana sin frame especificado, el default es `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`, que para `COUNT(*)` da el mismo resultado en este caso. Pero **es buena práctica especificarlo siempre** para evitar sorpresas.

---

## Ejercicio 17 — ALTER TABLE + UPDATE en una transacción (es_moroso)

**Keywords para buscar:** `ALTER TABLE`, `ADD COLUMN`, `UPDATE`, `BEGIN`, `COMMIT`, `transacción`, `examen tipo`, `Q10`, `boolean default`

**Tipo de pregunta:** SQL / DDL

**Dificultad:** media

**Tablas involucradas:**
- `propietario`, `vehiculo`, `infraccion`, `pago`

**Patrones relacionados:**
- Variante directa de Q10 del examen tipo
- Atomicidad del DDL + DML

**Trampas típicas:**
- Olvidar el `DEFAULT FALSE` con `NOT NULL` cuando hay datos existentes
- Olvidar BEGIN/COMMIT
- Hacer 2 transacciones separadas (no atómico)

**Enunciado:**
Para mejorar el reporte de morosos, realiza los siguientes cambios a la tabla `propietario` dentro de **una sola transacción**:

1. Agrega una nueva columna llamada `es_moroso` de tipo booleano, **no nulleable**, con default `FALSE`.
2. Modifica este nuevo atributo a `TRUE` para aquellos propietarios que tengan al menos una infracción **sin pagar completamente** (es decir, el total pagado en `pago` es menor al `infraccion.importe`).

---

### Solución paso a paso

1. Empiezo transacción con `BEGIN`.
2. `ALTER TABLE ... ADD COLUMN ... BOOLEAN NOT NULL DEFAULT FALSE`. (Esto deja todos los registros existentes en FALSE).
3. `UPDATE propietario SET es_moroso = TRUE WHERE EXISTS (...)`.
4. Confirmo con `COMMIT`.

---

### Query final

```sql
BEGIN;

ALTER TABLE propietario
    ADD COLUMN es_moroso BOOLEAN NOT NULL DEFAULT FALSE;

UPDATE propietario
SET es_moroso = TRUE
WHERE EXISTS (
    SELECT 1
    FROM vehiculo
    INNER JOIN infraccion 
        ON vehiculo.id = infraccion.vehiculo_id
    LEFT JOIN pago 
        ON pago.infraccion_id = infraccion.id
    WHERE vehiculo.propietario_id = propietario.id
    GROUP BY infraccion.id, infraccion.importe
    HAVING COALESCE(SUM(pago.importe), 0) < infraccion.importe
);

COMMIT;
```

---

### Explicación de la query

- `BEGIN`: inicia la transacción. Si algo falla, todo se revierte con `ROLLBACK`.
- `ALTER TABLE ... ADD COLUMN ... DEFAULT FALSE NOT NULL`: agrega la columna. Como tiene DEFAULT, los registros existentes se llenan con FALSE.
- `UPDATE ... WHERE EXISTS`: subconsulta correlacionada que verifica si el propietario tiene al menos una infracción no pagada totalmente.
  - INNER JOIN vehiculo + infraccion: encuentra las infracciones del propietario.
  - LEFT JOIN pago: incluye infracciones sin ningún pago.
  - GROUP BY + HAVING: filtra las que tienen total pagado < importe original.
- `COMMIT`: hace permanentes los cambios.

> 💡 **Alternativa más simple usando `IN` con subconsulta**:
> ```sql
> UPDATE propietario
> SET es_moroso = TRUE
> WHERE id IN (
>     SELECT vehiculo.propietario_id
>     FROM vehiculo
>     INNER JOIN infraccion ON vehiculo.id = infraccion.vehiculo_id
>     LEFT JOIN pago ON pago.infraccion_id = infraccion.id
>     GROUP BY vehiculo.propietario_id, infraccion.id, infraccion.importe
>     HAVING COALESCE(SUM(pago.importe), 0) < infraccion.importe
> );
> ```

---

## Ejercicio 18 — ALTER TABLE + UPDATE (es_creador_frecuente equivalente)

**Keywords para buscar:** `ALTER TABLE`, `ADD COLUMN`, `UPDATE`, `BEGIN`, `transacción`, `boolean`

**Tipo de pregunta:** SQL / DDL

**Dificultad:** media

**Tablas involucradas:**
- `vehiculo`, `infraccion`

**Patrones relacionados:**
- Variante del Ej. 17 pero contar y filtrar por umbral

**Trampas típicas:**
- Confundir COUNT en HAVING con COUNT en WHERE
- Olvidar el agregado en la subconsulta

**Enunciado:**
Agrega a la tabla `vehiculo` una columna `categoria_riesgo` de tipo `VARCHAR(20)`, no nulleable, con default `'bajo'`. Luego, en la misma transacción, actualízala a `'alto'` para todo vehículo con 10 o más infracciones registradas, y a `'medio'` para vehículos con entre 3 y 9 infracciones.

---

### Query final

```sql
BEGIN;

ALTER TABLE vehiculo
    ADD COLUMN categoria_riesgo VARCHAR(20) NOT NULL DEFAULT 'bajo';

-- Marcar 'alto' a los de >= 10 infracciones
UPDATE vehiculo
SET categoria_riesgo = 'alto'
WHERE id IN (
    SELECT vehiculo_id
    FROM infraccion
    GROUP BY vehiculo_id
    HAVING COUNT(*) >= 10
);

-- Marcar 'medio' a los de 3-9 infracciones
UPDATE vehiculo
SET categoria_riesgo = 'medio'
WHERE id IN (
    SELECT vehiculo_id
    FROM infraccion
    GROUP BY vehiculo_id
    HAVING COUNT(*) BETWEEN 3 AND 9
);

COMMIT;
```

---

### Explicación

- Hago el UPDATE de **'alto' primero** porque después el de 'medio' no toca esos registros (filtros disjuntos).
- En realidad como los rangos `[3,9]` y `[10, ∞)` no se solapan, **el orden no importa**, pero por claridad procedo de forma incremental.
- `BETWEEN x AND y` es inclusivo en ambos extremos.

> 🚨 **Trampa**: si los rangos se solaparan, el orden sí importa. Por ejemplo si dijera "medio = ≥3" y "alto = ≥10", tendría que hacer "alto" después, sino los de ≥10 se quedan en "medio".

---

## Ejercicio 19 — CREATE TABLE con CASCADE (multas_apeladas)

**Keywords para buscar:** `CREATE TABLE`, `FOREIGN KEY`, `CASCADE`, `NOT NULL`, `PRIMARY KEY`, `BIGSERIAL`, `examen tipo`, `Q11`

**Tipo de pregunta:** SQL / DDL

**Dificultad:** media

**Tablas involucradas:**
- Nueva tabla `apelacion`, FKs a `infraccion` y `propietario`

**Patrones relacionados:**
- Variante directa de Q11 del examen tipo
- Diseño de tabla con relaciones y políticas de cascada

**Trampas típicas:**
- Olvidar `NOT NULL` en columnas (lo piden explícitamente)
- Omitir `ON DELETE CASCADE`
- Confundir CASCADE con RESTRICT

**Enunciado:**
La SSC quiere implementar un módulo de apelaciones. Crea una tabla llamada `apelacion` con las siguientes características:

- Columnas:
  - `id` (llave primaria, autoincremental)
  - `infraccion_id` (referencia a infracción)
  - `propietario_id` (referencia al propietario que apela)
  - `fecha_apelacion` (timestamp del momento de la apelación)
  - `motivo` (texto explicativo)
  - `estado` (cadena: 'pendiente', 'aceptada', 'rechazada')

Consideraciones:
- Ningún atributo puede ser nulo.
- `id` debe ser llave primaria autoincremental.
- Las llaves foráneas deben estar correctamente referenciadas.
- Si la infracción se borra, la apelación también (CASCADE).
- Si el propietario se borra, **no** se debe permitir (RESTRICT).
- `estado` solo puede tener uno de los 3 valores válidos.

---

### Query final

```sql
CREATE TABLE apelacion (
    id              BIGSERIAL    PRIMARY KEY,
    infraccion_id   BIGINT       NOT NULL,
    propietario_id  BIGINT       NOT NULL,
    fecha_apelacion TIMESTAMP    NOT NULL DEFAULT NOW(),
    motivo          TEXT         NOT NULL,
    estado          VARCHAR(20)  NOT NULL CHECK (estado IN ('pendiente', 'aceptada', 'rechazada')),

    FOREIGN KEY (infraccion_id)
        REFERENCES infraccion(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE,

    FOREIGN KEY (propietario_id)
        REFERENCES propietario(id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);
```

---

### Explicación

- `BIGSERIAL`: tipo especial de PostgreSQL = `BIGINT` + secuencia + DEFAULT nextval. Equivale a autoincrement.
- `NOT NULL` en todas las columnas, como pide el enunciado.
- `CHECK (estado IN (...))`: restringe los valores permitidos. Alternativa: usar un tipo ENUM, pero CHECK es más portable.
- `ON DELETE CASCADE` para `infraccion_id`: si se borra la infracción, se borran sus apelaciones.
- `ON DELETE RESTRICT` para `propietario_id`: si se intenta borrar un propietario con apelaciones activas, el DBMS lanza error.
- `ON UPDATE CASCADE` en ambas: si por algún motivo se cambia el id del padre, se propaga.

> 💡 **Convención de nombres de constraints**: aunque no es obligatorio nombrar las FKs, en producción se hace así:
> ```sql
> CONSTRAINT fk_apelacion_infraccion FOREIGN KEY (infraccion_id) ...
> ```
> Esto ayuda al DROP CONSTRAINT más tarde.

---

## Ejercicio 20 — CREATE TABLE pivote (vehiculo_copropietario)

**Keywords para buscar:** `tabla pivote`, `CREATE TABLE`, `PK compuesta`, `relación M:N`, `copropietario`, `examen difícil`

**Tipo de pregunta:** SQL / DDL

**Dificultad:** difícil

**Tablas involucradas:**
- Nueva tabla pivote entre `vehiculo` y `propietario`

**Patrones relacionados:**
- Modelar relación M:N agregando tabla pivote
- PK compuesta

**Trampas típicas:**
- Olvidar la PK compuesta
- Permitir duplicados de la combinación

**Enunciado:**
La CDMX ahora quiere permitir que un vehículo tenga **varios copropietarios** (es decir, una relación M:N entre `vehiculo` y `propietario`). Crea la tabla pivote `vehiculo_copropietario` que registre los copropietarios adicionales (además del titular ya guardado en `vehiculo.propietario_id`). Incluye:
- `vehiculo_id`, `propietario_id` (ambos no nulos, formando juntos la PK)
- `porcentaje_propiedad` (numeric(5, 2), no nulo, entre 0 y 100)
- `fecha_alta` (timestamp, no nulo, default ahora)

Restricciones:
- No puede haber dos veces el mismo par (vehículo, copropietario) → eso lo garantiza la PK compuesta.
- Si se borra el vehículo, se borran los registros pivote.
- Si se borra un propietario que está como copropietario, debe lanzar error.

---

### Query final

```sql
CREATE TABLE vehiculo_copropietario (
    vehiculo_id          BIGINT         NOT NULL,
    propietario_id       BIGINT         NOT NULL,
    porcentaje_propiedad NUMERIC(5, 2)  NOT NULL CHECK (porcentaje_propiedad > 0 AND porcentaje_propiedad <= 100),
    fecha_alta           TIMESTAMP      NOT NULL DEFAULT NOW(),

    PRIMARY KEY (vehiculo_id, propietario_id),

    FOREIGN KEY (vehiculo_id)
        REFERENCES vehiculo(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE,

    FOREIGN KEY (propietario_id)
        REFERENCES propietario(id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);
```

---

### Explicación

- `PRIMARY KEY (vehiculo_id, propietario_id)`: clave compuesta. Garantiza unicidad del par.
- Las FKs apuntan a `vehiculo.id` y `propietario.id`.
- `CHECK (porcentaje_propiedad > 0 AND porcentaje_propiedad <= 100)`: rango válido. (No usé `BETWEEN 0 AND 100` porque 0% no tiene sentido lógico).
- `NUMERIC(5, 2)`: 5 dígitos totales, 2 decimales (rango: -999.99 a 999.99). Suficiente para porcentajes.
- `ON DELETE RESTRICT` en propietario: protege al copropietario de borrado accidental.

---

## Ejercicio 21 — EXISTS para encontrar propietarios CON multas

**Keywords para buscar:** `EXISTS`, `subquery correlacionada`, `WHERE EXISTS`, `propietarios`, `infracciones`, `subquery`, `semi-join`, `existencia`

**Tipo de pregunta:** SQL — subquery correlacionada

**Dificultad:** media

**Tablas involucradas:**
- `propietario`
- `vehiculo`
- `infraccion`

**Relaciones usadas del ERD:**
- `propietario` 1—N `vehiculo`
- `vehiculo` 1—N `infraccion`

**Patrones relacionados:**
- EXISTS vs IN vs JOIN DISTINCT
- Subquery correlacionada (referencia tabla externa)

**Trampas típicas:**
- Si uso `JOIN` directo puedo duplicar propietarios (uno por cada multa). Por eso `EXISTS` o `DISTINCT` son necesarios.
- `EXISTS` no se preocupa por el valor devuelto, solo por si la subquery devuelve al menos una fila → por eso es común poner `SELECT 1`.

**Enunciado:**
Lista nombre y apellido de todos los propietarios que tienen **al menos una infracción registrada** en alguno de sus vehículos. Usa `EXISTS`, no `JOIN`.

---

### Solución paso a paso

1. **Lo que pide:** propietarios con ≥ 1 multa.
2. **Lo correlacionado:** para cada `propietario` de la query externa, debo verificar si existe **algún** vehículo suyo que tenga **alguna** multa.
3. **Estructura:**
   - `SELECT FROM propietario p WHERE EXISTS (SELECT 1 FROM vehiculo v JOIN infraccion i ON v.id = i.vehiculo_id WHERE v.propietario_id = p.id)`
4. La condición `v.propietario_id = p.id` es la que **correlaciona** la subquery con la fila externa.

---

### Query final

```sql
SELECT p.nombre,
       p.apellido
FROM   propietario p
WHERE  EXISTS (
           SELECT 1
           FROM   vehiculo v
           JOIN   infraccion i ON i.vehiculo_id = v.id
           WHERE  v.propietario_id = p.id
       )
ORDER  BY p.apellido, p.nombre;
```

---

### Explicación de la query

- `SELECT 1` en el `EXISTS` es convención: no importa qué proyectes, sólo si hay al menos una fila.
- `EXISTS` se evalúa **por cada fila externa**: para cada propietario, PostgreSQL ejecuta la subquery con `p.id` ya bindeado.
- Equivalente con `IN`:
  ```sql
  WHERE p.id IN (SELECT v.propietario_id
                 FROM vehiculo v JOIN infraccion i ON i.vehiculo_id = v.id)
  ```
  pero `EXISTS` suele optimizar mejor cuando hay correlación.
- Equivalente con `JOIN + DISTINCT`:
  ```sql
  SELECT DISTINCT p.nombre, p.apellido
  FROM propietario p
  JOIN vehiculo v ON v.propietario_id = p.id
  JOIN infraccion i ON i.vehiculo_id = v.id;
  ```
  funciona, pero genera duplicados intermedios y luego los elimina (más costoso).

---

## Ejercicio 22 — NOT EXISTS para encontrar cámaras NUNCA usadas

**Keywords para buscar:** `NOT EXISTS`, `anti-join`, `LEFT JOIN IS NULL`, `cámaras inactivas`, `sin uso`, `subquery negada`, `complemento`

**Tipo de pregunta:** SQL — anti-join

**Dificultad:** difícil

**Tablas involucradas:**
- `camara`
- `infraccion`

**Relaciones usadas del ERD:**
- `camara` 1—N `infraccion` (camara.id ← infraccion.camara_id)

**Patrones relacionados:**
- `NOT EXISTS` (preferido) vs `LEFT JOIN ... WHERE x IS NULL` vs `NOT IN`
- Trampa de `NOT IN` con NULLs

**Trampas típicas:**
- 🚨 `NOT IN (SELECT camara_id FROM infraccion)` falla si hay un `NULL` en la subquery: toda la query devuelve 0 filas. **Nunca uses `NOT IN` con columnas que puedan ser nulas.**
- `NOT EXISTS` es seguro frente a NULLs y suele ser más eficiente.

**Enunciado:**
Lista las cámaras (id, tipo, alcaldía) que **nunca** han registrado una infracción. Usa `NOT EXISTS`.

---

### Solución paso a paso

1. **Lo que pide:** cámaras que NO aparecen en `infraccion`.
2. **Estructura:** "para cada cámara, NO debe existir ninguna infracción que la referencie".
3. La subquery correlacionada es:
   ```sql
   NOT EXISTS (SELECT 1 FROM infraccion i WHERE i.camara_id = c.id)
   ```
4. **Alternativa equivalente** (anti-join con LEFT JOIN):
   ```sql
   FROM camara c LEFT JOIN infraccion i ON i.camara_id = c.id WHERE i.id IS NULL
   ```

---

### Query final

```sql
SELECT c.id,
       c.tipo,
       c.alcaldia
FROM   camara c
WHERE  NOT EXISTS (
           SELECT 1
           FROM   infraccion i
           WHERE  i.camara_id = c.id
       )
ORDER  BY c.alcaldia, c.id;
```

---

### Explicación de la query

- Para cada cámara externa `c`, busco si hay alguna fila en `infraccion` con `i.camara_id = c.id`. Si **no** hay → la cámara entra al resultado.
- Patrón clásico de "anti-join". Ideal para preguntas tipo "los X que no tienen ningún Y".
- Si quisiera además filtrar sólo cámaras **activas** sin uso: `WHERE c.activa = TRUE AND NOT EXISTS ...`.
- Versión LEFT JOIN equivalente:
  ```sql
  SELECT c.id, c.tipo, c.alcaldia
  FROM   camara c
  LEFT   JOIN infraccion i ON i.camara_id = c.id
  WHERE  i.id IS NULL;
  ```

---

## Ejercicio 23 — CREATE INDEX para acelerar query frecuente

**Keywords para buscar:** `CREATE INDEX`, `índice B-tree`, `índice compuesto`, `optimización`, `EXPLAIN`, `tuning`, `índice parcial`, `WHERE` rango

**Tipo de pregunta:** Optimización con DBMS

**Dificultad:** media

**Tablas involucradas:**
- `infraccion`

**Patrones relacionados:**
- Decidir tipo de índice (B-tree, Hash, parcial)
- Orden de columnas en índice compuesto
- Cuándo NO crear índice

**Trampas típicas:**
- Si filtras por igualdad **y** rango, la columna de igualdad va PRIMERO en el índice compuesto.
- Hash no sirve para rangos; B-tree sí.
- Un índice sobre una columna muy poco selectiva (ej. `boolean`) suele NO ayudar.

**Enunciado:**
Una query frecuente del sistema es:
```sql
SELECT *
FROM   infraccion
WHERE  tipo = 'velocidad'
  AND  fecha >= DATE '2025-01-01';
```
Esta query tarda varios segundos porque `infraccion` tiene millones de filas. Propón un índice óptimo y justifica el orden de las columnas.

---

### Solución paso a paso

1. **Patrón de acceso:** igualdad sobre `tipo` + rango sobre `fecha`.
2. **Regla:** en índice compuesto B-tree, **igualdad antes de rango**. Razón: el índice se recorre como árbol; una vez que entras al rango, ya no puedes aprovechar la siguiente columna para acotar más.
3. **Tipo de índice:** B-tree (porque hay rango sobre fecha; Hash queda descartado).
4. **Selectividad:** `tipo = 'velocidad'` reduce mucho; combinado con la fecha, el índice será muy efectivo.
5. **Opcional:** si la mayoría de queries siempre filtran fecha reciente, podría hacerse índice **parcial**.

---

### Query final

```sql
-- Índice principal recomendado
CREATE INDEX idx_infraccion_tipo_fecha
ON infraccion (tipo, fecha);

-- Opción avanzada: índice parcial sólo para los últimos años
-- (sirve si casi todas las queries filtran fechas recientes)
CREATE INDEX idx_infraccion_tipo_fecha_recientes
ON infraccion (tipo, fecha)
WHERE fecha >= DATE '2024-01-01';
```

---

### Explicación de la query

- **Orden `(tipo, fecha)`**: B-tree navega primero a la rama `tipo='velocidad'`, luego dentro de esa rama hace el barrido por rango sobre `fecha`. Si invirtiera el orden, tendría que escanear todo el rango de fechas y filtrar por tipo después.
- **Hash queda descartado** porque no soporta `>=` ni `<` ni `BETWEEN`.
- **Índice parcial** reduce tamaño y costo de mantenimiento si las consultas históricas son raras.
- ⚠️ Trade-off: cada índice nuevo penaliza `INSERT`/`UPDATE`/`DELETE` y consume espacio. No conviene crear índices sobre tablas con escritura muy alta y lectura baja.

---

## Ejercicio 24 — CTEs encadenadas (WITH) para análisis multinivel

**Keywords para buscar:** `WITH`, `CTE`, `common table expression`, `CTE encadenadas`, `subquery legible`, `pago`, `morosos`

**Tipo de pregunta:** SQL — CTEs

**Dificultad:** difícil

**Tablas involucradas:**
- `propietario`, `vehiculo`, `infraccion`, `pago`

**Relaciones usadas del ERD:**
- `propietario` 1—N `vehiculo` 1—N `infraccion` 1—N `pago`

**Patrones relacionados:**
- Romper una query compleja en pasos (cada paso = CTE)
- Reutilizar el resultado intermedio varias veces

**Trampas típicas:**
- Confundir el total adeudado: `importe` está duplicado en `infraccion` y `pago`. El **adeudo real** = `infraccion.importe − SUM(pago.importe)`.
- Si nunca pagó algo, `SUM(pago.importe)` es NULL → usar `COALESCE(..., 0)`.

**Enunciado:**
Construye un reporte que liste los **5 propietarios con mayor adeudo total** en la CDMX. El "adeudo" de una infracción se calcula como `infraccion.importe − SUM(pagos asociados)`. Usa CTEs encadenadas para mantener el código legible.

---

### Solución paso a paso

1. **CTE 1 — `pago_por_infraccion`**: suma de pagos por infracción.
2. **CTE 2 — `adeudo_por_infraccion`**: para cada infracción, calculo `importe - COALESCE(pago_total, 0)`. Filtro las que tengan adeudo > 0.
3. **CTE 3 — `adeudo_por_propietario`**: sumo adeudos por propietario (saltando vehiculo).
4. **Query final**: tomo top 5.

---

### Query final

```sql
WITH pago_por_infraccion AS (
    SELECT   infraccion_id,
             SUM(importe) AS pagado
    FROM     pago
    GROUP BY infraccion_id
),
adeudo_por_infraccion AS (
    SELECT i.id              AS infraccion_id,
           i.vehiculo_id,
           i.importe - COALESCE(p.pagado, 0) AS adeudo
    FROM   infraccion i
    LEFT   JOIN pago_por_infraccion p ON p.infraccion_id = i.id
    WHERE  i.importe - COALESCE(p.pagado, 0) > 0
),
adeudo_por_propietario AS (
    SELECT   v.propietario_id,
             SUM(a.adeudo) AS adeudo_total
    FROM     adeudo_por_infraccion a
    JOIN     vehiculo v ON v.id = a.vehiculo_id
    GROUP BY v.propietario_id
)
SELECT   pr.id,
         pr.nombre,
         pr.apellido,
         ad.adeudo_total
FROM     adeudo_por_propietario ad
JOIN     propietario pr ON pr.id = ad.propietario_id
ORDER BY ad.adeudo_total DESC
LIMIT    5;
```

---

### Explicación de la query

- **Por qué CTEs y no subqueries anidadas:** legibilidad. Cada CTE es un "paso conceptual" con nombre.
- **`LEFT JOIN` a `pago_por_infraccion`**: si una infracción no tiene pagos, queremos contar su importe completo como adeudo.
- **`COALESCE(p.pagado, 0)`**: convierte el NULL en 0 para que la resta funcione.
- **Filtro `adeudo > 0`** dentro de la CTE 2: ya descarta las infracciones liquidadas antes de agregar (menos filas para sumar).
- **Limitación:** si dos propietarios empatan en posición 5, `LIMIT 5` corta arbitrariamente. Para manejar empates correctamente usaría `DENSE_RANK()` (ver Ej 13).

---

## Ejercicio 25 — FULL OUTER JOIN para auditoría de cámaras vs alcaldías

**Keywords para buscar:** `FULL OUTER JOIN`, `FULL JOIN`, `COALESCE`, `outer join completo`, `inconsistencia`, `auditoría`

**Tipo de pregunta:** SQL — FULL JOIN (raro pero clásico)

**Dificultad:** difícil

**Tablas involucradas:**
- `camara`
- `infraccion`

**Patrones relacionados:**
- FULL OUTER JOIN combina LEFT y RIGHT
- Útil para encontrar inconsistencias bidireccionales

**Trampas típicas:**
- 🚨 Confundir cuándo se necesita FULL. Reglas:
  - Sólo izquierdas pueden ser huérfanas → LEFT.
  - Sólo derechas pueden ser huérfanas → RIGHT (o invertir).
  - **Ambas pueden ser huérfanas → FULL.**
- 🚨 Al hacer FULL JOIN sobre `camara.alcaldia`, NO sobre `camara.id`. El propósito es agrupar por alcaldía.

**Enunciado:**
Genera un reporte que, **por alcaldía**, muestre:
- cuántas cámaras tiene instaladas,
- cuántas infracciones se han registrado allí.

Incluye alcaldías que tengan cámaras pero **ninguna** infracción, y (caso hipotético) infracciones cuya cámara haya sido borrada de la tabla `camara`. Usa FULL OUTER JOIN.

---

### Solución paso a paso

1. **Necesito agrupar por alcaldía** desde dos fuentes distintas.
2. Primero, agrupo cámaras por alcaldía (subquery o CTE).
3. Luego, agrupo infracciones por alcaldía (vía join con cámara). El detalle: si la cámara fue borrada (FK rota hipotéticamente), no tendríamos alcaldía. Para el escenario realista, asumo que `infraccion.camara_id` siempre conduce a una `camara` válida.
4. **FULL JOIN** entre los dos resúmenes para no perder alcaldías que aparezcan sólo en uno.

---

### Query final

```sql
WITH camaras_por_alcaldia AS (
    SELECT   alcaldia,
             COUNT(*) AS num_camaras
    FROM     camara
    GROUP BY alcaldia
),
infracciones_por_alcaldia AS (
    SELECT   c.alcaldia,
             COUNT(*) AS num_infracciones
    FROM     infraccion i
    JOIN     camara c ON c.id = i.camara_id
    GROUP BY c.alcaldia
)
SELECT   COALESCE(ca.alcaldia, ia.alcaldia) AS alcaldia,
         COALESCE(ca.num_camaras, 0)        AS num_camaras,
         COALESCE(ia.num_infracciones, 0)   AS num_infracciones
FROM     camaras_por_alcaldia ca
FULL     OUTER JOIN infracciones_por_alcaldia ia
         ON ca.alcaldia = ia.alcaldia
ORDER BY num_infracciones DESC;
```

---

### Explicación de la query

- **`FULL OUTER JOIN`**: si una alcaldía está sólo en `ca` (cámaras instaladas pero sin uso), aparece con `num_infracciones = NULL`; si está sólo en `ia`, aparece con `num_camaras = NULL`.
- **`COALESCE(ca.alcaldia, ia.alcaldia)`**: cuando una fila viene sólo de un lado, el otro lado es NULL, incluyendo la columna de agrupación. Por eso uso COALESCE en el SELECT para tener una sola columna "alcaldia".
- **`COALESCE(num, 0)`**: presentar 0 en vez de NULL para legibilidad.
- En esquemas con integridad referencial estricta, el FULL JOIN aquí degenera a LEFT JOIN. Pero en preguntas de examen, FULL es la respuesta "más segura" cuando se pide cobertura bidireccional.

---

## Ejercicio 26 — Múltiples agregaciones en una sola query (dashboard)

**Keywords para buscar:** `dashboard`, `COUNT(*)`, `SUM`, `AVG`, `múltiples agregaciones`, `FILTER`, `CASE WHEN`, `cross-tab`

**Tipo de pregunta:** SQL — agregaciones condicionales

**Dificultad:** difícil

**Tablas involucradas:**
- `infraccion`, `pago`

**Patrones relacionados:**
- `COUNT(*) FILTER (WHERE …)` (PostgreSQL)
- `SUM(CASE WHEN … THEN 1 ELSE 0 END)` (estándar SQL)

**Trampas típicas:**
- `COUNT(*)` cuenta filas; `COUNT(col)` no cuenta nulos. Diferencia importante en LEFT JOIN.
- `AVG(numeric)` divide entre el número de no-nulos, no entre todas las filas.

**Enunciado:**
Construye un mini-dashboard de una sola fila con las siguientes métricas globales:
1. Total de infracciones registradas.
2. Total de infracciones de tipo `'velocidad'`.
3. Total de infracciones de tipo `'estacionamiento'`.
4. Importe promedio de las infracciones.
5. Total recaudado (suma de todos los pagos).
6. Porcentaje de infracciones que están totalmente liquidadas.

---

### Solución paso a paso

1. Métricas 1–4 → sólo `infraccion`.
2. Métrica 5 → sólo `pago`.
3. Métrica 6 → necesito comparar pagos vs importe por infracción. Lo hago con subquery escalar.
4. Combino todo en un `SELECT` sin `FROM` agrupado: cada métrica es una subquery escalar, o uso un solo `SELECT FROM infraccion` con `FILTER`.

---

### Query final

```sql
WITH liquidadas AS (
    SELECT i.id
    FROM   infraccion i
    LEFT   JOIN (
               SELECT   infraccion_id,
                        SUM(importe) AS pagado
               FROM     pago
               GROUP BY infraccion_id
           ) p ON p.infraccion_id = i.id
    WHERE  COALESCE(p.pagado, 0) >= i.importe
)
SELECT
    (SELECT COUNT(*) FROM infraccion)                                                          AS total_infracciones,
    (SELECT COUNT(*) FROM infraccion WHERE tipo = 'velocidad')                                 AS total_velocidad,
    (SELECT COUNT(*) FROM infraccion WHERE tipo = 'estacionamiento')                           AS total_estacionamiento,
    (SELECT ROUND(AVG(importe), 2) FROM infraccion)                                            AS importe_promedio,
    (SELECT COALESCE(SUM(importe), 0) FROM pago)                                               AS total_recaudado,
    ROUND(
        100.0 * (SELECT COUNT(*) FROM liquidadas)
              / NULLIF((SELECT COUNT(*) FROM infraccion), 0),
        2
    )                                                                                          AS pct_liquidadas;
```

Versión alternativa con `FILTER` (PostgreSQL):

```sql
WITH pagos_por_inf AS (
    SELECT   infraccion_id, SUM(importe) AS pagado
    FROM     pago
    GROUP BY infraccion_id
)
SELECT
    COUNT(*)                                                              AS total_infracciones,
    COUNT(*) FILTER (WHERE i.tipo = 'velocidad')                          AS total_velocidad,
    COUNT(*) FILTER (WHERE i.tipo = 'estacionamiento')                    AS total_estacionamiento,
    ROUND(AVG(i.importe), 2)                                              AS importe_promedio,
    COALESCE(SUM(p.pagado), 0)                                            AS total_recaudado,
    ROUND(100.0 * COUNT(*) FILTER (WHERE COALESCE(p.pagado, 0) >= i.importe) / COUNT(*), 2)
                                                                          AS pct_liquidadas
FROM        infraccion i
LEFT JOIN   pagos_por_inf p ON p.infraccion_id = i.id;
```

---

### Explicación de la query

- **Subqueries escalares**: cada métrica es independiente; muy legible para dashboards.
- **`FILTER (WHERE ...)`**: extensión SQL estándar (también soportada por PostgreSQL). Equivalente a `SUM(CASE WHEN ... THEN 1 ELSE 0 END)`.
- **`NULLIF(x, 0)`**: protege contra división entre cero. Si la tabla está vacía → null en vez de error.
- **`100.0 *`**: fuerza aritmética con decimales (no entera).
- ⚠️ Trampa: si pongo `SUM(p.pagado)` sin haber hecho LEFT JOIN agregado, podría duplicar valores. Por eso primero agrego en CTE.

---

## Ejercicio 27 — Self-join: parejas de copropietarios potenciales

**Keywords para buscar:** `self-join`, `JOIN consigo misma`, `alias diferentes`, `parejas`, `combinatoria`, `evitar duplicados`, `<`

**Tipo de pregunta:** SQL — self-join

**Dificultad:** difícil

**Tablas involucradas:**
- `propietario`

**Patrones relacionados:**
- Auto-join con dos alias
- Filtrar duplicados con `a.id < b.id`

**Trampas típicas:**
- Sin el filtro `a.id < b.id`, cada pareja aparece 2 veces (A,B y B,A) y además las parejas trivializadas (A,A).
- Si usas `a.id != b.id`, evitas (A,A) pero NO los duplicados (A,B) y (B,A).

**Enunciado:**
La oficina quiere detectar parejas de propietarios que comparten **el mismo apellido** (posibles familiares para fines de revisión cruzada). Lista todas las parejas (sin repetir) que cumplan esa condición. Devuelve nombre y apellido de ambos.

---

### Solución paso a paso

1. **Self-join** sobre `propietario` con dos alias: `a` y `b`.
2. **Condición de match:** `a.apellido = b.apellido`.
3. **Evitar (A,A):** `a.id <> b.id`.
4. **Evitar (B,A) cuando ya tengo (A,B):** `a.id < b.id`. Esto garantiza una sola dirección.

---

### Query final

```sql
SELECT a.nombre   AS nombre_1,
       a.apellido AS apellido_1,
       b.nombre   AS nombre_2,
       b.apellido AS apellido_2
FROM   propietario a
JOIN   propietario b
       ON a.apellido = b.apellido
       AND a.id < b.id
ORDER  BY a.apellido, a.nombre, b.nombre;
```

---

### Explicación de la query

- Dos alias `a` y `b` para tratar la misma tabla como dos "copias virtuales".
- `a.id < b.id`: la clave para evitar duplicados. Equivale a tomar combinaciones C(n, 2), no permutaciones.
- Si el examen pidiera "parejas con misma alcaldía" sobre `vehiculo` o `camara`, el patrón es idéntico.
- **Generalización:** para tríos, harías `a.id < b.id AND b.id < c.id`.

---

## Ejercicio 28 — Descomposición a FNBC (normalización dura)

**Keywords para buscar:** `FNBC`, `Boyce-Codd`, `descomposición`, `DF parciales`, `descomposición sin pérdida`, `normalización`, `superllave`, `flecha sale de superllave`

**Tipo de pregunta:** Normalización avanzada

**Dificultad:** MUY difícil

**Tablas involucradas:**
- Esquema hipotético derivado de `infraccion` (no normalizado)

**Patrones relacionados:**
- Detectar DF problemática (flecha que no sale de superllave)
- Descomponer en dos relaciones

**Trampas típicas:**
- Una relación puede estar en 3FN pero no en FNBC.
- En FNBC: **toda** flecha sale de superllave (sin excepciones).
- La descomposición debe ser **sin pérdida** (lossless): el atributo en común debe ser llave en al menos una de las dos relaciones resultantes.

**Enunciado:**
Suponga que un becario diseñó la siguiente tabla "infraccion_completa" para evitar joins:

```
infraccion_completa(id_infraccion, fecha, tipo_infraccion,
                    importe, placa, marca, anio, color,
                    nombre_propietario, telefono_propietario)
```

DFs identificadas:
- `id_infraccion → fecha, tipo_infraccion, importe, placa`
- `placa → marca, anio, color, nombre_propietario, telefono_propietario`
- `nombre_propietario → telefono_propietario`

(a) ¿Está en FNBC? Justifica.
(b) Si no lo está, descompón en relaciones que sí estén en FNBC, sin pérdida.

---

### Solución paso a paso

**Paso 1 — Encontrar la llave candidata de `infraccion_completa`.**

`id_infraccion` determina todo el resto (sigue las flechas: id → placa → todo lo demás). Entonces `{id_infraccion}` es **superllave** y, dado que es atómica, es **llave candidata** única.

**Paso 2 — Revisar cada DF: ¿la parte izquierda es superllave?**

| DF | Lado izquierdo | ¿Superllave? |
|----|----------------|--------------|
| `id_infraccion → ...` | `{id_infraccion}` | ✅ Sí |
| `placa → marca, anio, color, nombre_propietario, telefono_propietario` | `{placa}` | ❌ NO |
| `nombre_propietario → telefono_propietario` | `{nombre_propietario}` | ❌ NO |

Hay **dos** DFs cuyo lado izquierdo no es superllave → **NO está en FNBC**.

(Además, fíjate: tampoco está en 3FN porque `nombre_propietario` no es atributo primo y determina `telefono_propietario`.)

**Paso 3 — Descomponer.**

Algoritmo: tomamos cada DF problemática `X → Y` y creamos una relación `(X, Y)`.

- DF 2 problemática: `placa → marca, anio, color, nombre_propietario, telefono_propietario`
- DF 3 problemática: `nombre_propietario → telefono_propietario`

Pero la DF 3 está "encerrada" dentro de DF 2. Resolvemos por capas:

1. Saco propietario (porque `nombre_propietario` determina su teléfono):
   - **Propietario(nombre_propietario, telefono_propietario)**
2. Saco vehículo (placa determina sus atributos físicos + el propietario, ya por nombre):
   - **Vehiculo(placa, marca, anio, color, nombre_propietario)**
3. Lo que queda de infracción:
   - **Infraccion(id_infraccion, fecha, tipo_infraccion, importe, placa)**

**Paso 4 — Verificar.**

- **Infraccion**: única DF es `id_infraccion → resto`. Lado izquierdo = superllave. ✅ FNBC.
- **Vehiculo**: única DF es `placa → resto`. Lado izquierdo = superllave. ✅ FNBC.
- **Propietario**: única DF es `nombre_propietario → telefono_propietario`. Lado izquierdo = superllave. ✅ FNBC.

**Paso 5 — Sin pérdida (lossless):**

- `Infraccion ⋈ Vehiculo` por `placa` ← placa es PK en `Vehiculo`. ✅
- `Vehiculo ⋈ Propietario` por `nombre_propietario` ← nombre_propietario es PK en `Propietario`. ✅

Reconstruyo perfectamente `infraccion_completa` con dos joins.

---

### Query final (resultado de la descomposición)

```sql
CREATE TABLE propietario (
    nombre_propietario   VARCHAR(300) PRIMARY KEY,
    telefono_propietario VARCHAR(15)  NOT NULL
);

CREATE TABLE vehiculo (
    placa              VARCHAR(20)  PRIMARY KEY,
    marca              VARCHAR(100) NOT NULL,
    anio               SMALLINT     NOT NULL,
    color              VARCHAR(20),
    nombre_propietario VARCHAR(300) NOT NULL REFERENCES propietario(nombre_propietario)
);

CREATE TABLE infraccion (
    id_infraccion   BIGINT          PRIMARY KEY,
    fecha           TIMESTAMP       NOT NULL,
    tipo_infraccion VARCHAR(100)    NOT NULL,
    importe         NUMERIC(10, 2)  NOT NULL,
    placa           VARCHAR(20)     NOT NULL REFERENCES vehiculo(placa)
);
```

---

### Explicación

- ⚠️ Nota crítica: en la práctica real el examen ITAM prefiere PK artificial (ver Ej 3). Usar `nombre_propietario` como PK es **mala idea** (no único en la vida real). En el ejercicio académico de normalización lo aceptamos porque las DFs lo asumen. En producción agregaríamos un `id` surrogate.
- La descomposición resuelve dos violaciones de FNBC y queda **sin pérdida** porque los atributos de empalme (`placa`, `nombre_propietario`) son llaves en al menos una de las relaciones.
- También preserva las DFs originales: nada se pierde, todo se puede volver a inferir.

---

## Ejercicio 29 — Transacciones, ACID y ROLLBACK (conceptual)

**Keywords para buscar:** `transacción`, `ACID`, `ROLLBACK`, `COMMIT`, `SAVEPOINT`, `atomicidad`, `aislamiento`, `consistencia`, `durabilidad`, `READ COMMITTED`, `SERIALIZABLE`

**Tipo de pregunta:** Conceptual sobre Tema 5

**Dificultad:** difícil

**Tablas involucradas:**
- `infraccion`, `pago`

**Patrones relacionados:**
- ACID (Tema 5)
- Diferencia entre ROLLBACK total y ROLLBACK TO SAVEPOINT
- Niveles de aislamiento y anomalías que evitan

**Trampas típicas:**
- 🚨 Si `COMMIT` ya pasó, **no se puede** rollback. La durabilidad lo garantiza.
- `ROLLBACK TO SAVEPOINT s1` deshace sólo hasta el savepoint, no toda la transacción.
- `READ COMMITTED` (default en PostgreSQL) NO previene lecturas no repetibles ni fantasmas.

**Enunciado:**
Se ejecuta el siguiente bloque transaccional. ¿Cuál es el estado final de los datos? Justifica cada paso explicando qué garantía ACID se está respetando.

```sql
BEGIN;
  INSERT INTO pago (id, fecha, importe, infraccion_id, acreedor_id)
  VALUES (1001, NOW(), 500.00, 999, 42);

  SAVEPOINT antes_segundo_pago;

  INSERT INTO pago (id, fecha, importe, infraccion_id, acreedor_id)
  VALUES (1002, NOW(), 300.00, 999, 42);

  -- Nos arrepentimos
  ROLLBACK TO SAVEPOINT antes_segundo_pago;

  INSERT INTO pago (id, fecha, importe, infraccion_id, acreedor_id)
  VALUES (1003, NOW(), 800.00, 999, 42);

COMMIT;
```

(a) ¿Qué filas quedan persistidas?
(b) ¿Qué pasaría si **otra transacción** intentara leer `pago` con `infraccion_id = 999` después del primer INSERT pero antes del COMMIT, asumiendo `READ COMMITTED`?
(c) ¿Y si en lugar de `COMMIT`, ocurre una caída del servidor justo antes? ¿Qué propiedad ACID se prueba?

---

### Solución paso a paso

**(a) Filas persistidas:**

1. INSERT id=1001 → encolado en transacción.
2. SAVEPOINT `antes_segundo_pago` marca este punto.
3. INSERT id=1002 → encolado.
4. ROLLBACK TO SAVEPOINT → deshace el INSERT 1002, pero **NO** el 1001 (porque el savepoint está después de 1001).
5. INSERT id=1003 → encolado.
6. COMMIT → persiste 1001 y 1003.

**Estado final: filas con id = 1001 y 1003.** El id=1002 nunca se persistió.

→ Garantía ACID demostrada: **atomicidad parcial** (savepoints). Todo o nada, pero el "todo" se redefine al punto del savepoint.

**(b) Otra transacción lee `pago` con `READ COMMITTED` antes del COMMIT:**

`READ COMMITTED` ve sólo cambios **commiteados**. Como nada se ha hecho COMMIT, esa otra transacción **no verá ninguna de las filas nuevas**. Vería el estado anterior de la tabla.

→ Garantía ACID demostrada: **aislamiento** (los cambios no commiteados son invisibles a otras transacciones).

**(c) Caída del servidor justo antes del COMMIT:**

Como nunca llegó a hacer `COMMIT`, **toda la transacción se aborta** al recuperar. El log de transacciones detecta que no se commiteó y revierte cambios al estado anterior usando UNDO (rollback automático).

→ Garantía ACID demostrada: **atomicidad** (todo o nada) y **durabilidad** (cuando sí hay COMMIT, los datos persisten incluso ante caída; cuando no hay COMMIT, no quedan rastros).

---

### Query final (estado final inspeccionado)

```sql
-- Después del COMMIT exitoso del bloque original:
SELECT id, importe
FROM   pago
WHERE  id IN (1001, 1002, 1003);

-- Resultado esperado:
-- id   | importe
-- 1001 | 500.00
-- 1003 | 800.00
-- (1002 NO aparece)
```

---

### Explicación

- **Atomicidad**: una transacción es indivisible. Pero con savepoints, podemos tener "puntos de control" dentro de ella.
- **Consistencia**: si todos los CHECKs y FKs se respetan al final, la BD queda en estado válido.
- **Aislamiento**: cada nivel define qué fenómenos permite:
  - `READ UNCOMMITTED`: permite dirty reads.
  - `READ COMMITTED` (default PG): evita dirty reads.
  - `REPEATABLE READ`: evita lecturas no repetibles.
  - `SERIALIZABLE`: evita también fantasmas (resultado equivalente a ejecución secuencial).
- **Durabilidad**: una vez que `COMMIT` retorna, los cambios sobreviven incluso a un crash.

---

## Ejercicio 30 — CREATE VIEW y vistas actualizables

**Keywords para buscar:** `CREATE VIEW`, `vista`, `vista actualizable`, `WITH CHECK OPTION`, `vista materializada`, `simplificar query`, `seguridad por vista`

**Tipo de pregunta:** SQL + conceptual

**Dificultad:** media

**Tablas involucradas:**
- `infraccion`, `vehiculo`, `propietario`

**Patrones relacionados:**
- Vista como query nombrada (no almacena datos)
- Vista actualizable: sólo si referencia una sola tabla, sin agregaciones, sin DISTINCT
- WITH CHECK OPTION

**Trampas típicas:**
- Vista con JOIN, GROUP BY, DISTINCT o agregación → NO es actualizable.
- WITH CHECK OPTION: impide insertar/actualizar filas que no satisfagan el WHERE de la vista.

**Enunciado:**
(a) Crea una vista `vw_infracciones_velocidad_2025` que devuelva todas las infracciones del 2025 de tipo velocidad, con nombre del propietario incluido.
(b) ¿Es esta vista actualizable? Justifica.
(c) Crea una segunda vista `vw_velocidad_simple` que sí sea actualizable y que sólo muestre infracciones de tipo `'velocidad'`. Añade `WITH CHECK OPTION`.

---

### Solución paso a paso

(a) Necesita JOIN entre infraccion, vehiculo, propietario. WHERE filtra tipo y rango de fecha.

(b) NO es actualizable: hace JOIN entre tres tablas. Las vistas con JOINs múltiples no permiten INSERT (¿en qué tabla insertaríamos?). Algunos DBMS permiten UPDATE con vistas join-actualizables limitadas, pero el caso general no lo es.

(c) Vista de una sola tabla, sin agregaciones, con WHERE simple → actualizable. WITH CHECK OPTION garantiza que si alguien hace UPDATE/INSERT vía la vista, no podrá violar el WHERE.

---

### Query final

```sql
-- (a) Vista informativa con JOIN — NO actualizable
CREATE VIEW vw_infracciones_velocidad_2025 AS
SELECT i.id,
       i.fecha,
       i.importe,
       v.placa,
       p.nombre   AS propietario_nombre,
       p.apellido AS propietario_apellido
FROM   infraccion i
JOIN   vehiculo   v ON v.id = i.vehiculo_id
JOIN   propietario p ON p.id = v.propietario_id
WHERE  i.tipo = 'velocidad'
  AND  i.fecha >= DATE '2025-01-01'
  AND  i.fecha <  DATE '2026-01-01';

-- (c) Vista actualizable + check option
CREATE VIEW vw_velocidad_simple AS
SELECT id, fecha, tipo, importe, vehiculo_id, camara_id
FROM   infraccion
WHERE  tipo = 'velocidad'
WITH   CHECK OPTION;
```

---

### Explicación

- **Vistas no almacenan datos**: cada `SELECT * FROM vista` reejecuta la query subyacente.
- **Vistas materializadas** (`CREATE MATERIALIZED VIEW`, fuera del temario base pero buen extra) sí cachean resultados; se refrescan con `REFRESH MATERIALIZED VIEW`.
- **`WITH CHECK OPTION`**: si alguien hace `INSERT INTO vw_velocidad_simple (..., tipo, ...) VALUES (..., 'estacionamiento', ...)`, la inserción es **rechazada** porque la fila resultante no cumpliría el WHERE de la vista. Útil para enforzar restricciones lógicas vía vistas.
- **Por qué usar vistas:**
  - Simplifican queries repetitivas.
  - Capa de seguridad: dar acceso sólo a la vista, no a la tabla base.
  - Aislamiento del esquema: cambias la tabla, la vista mantiene la interfaz.

---

## Ejercicio 31 — Debugging: encuentra los errores de esta query

**Keywords para buscar:** `debugging`, `error en query`, `bug`, `query rota`, `corrección`, `mistakes`, `código incorrecto`

**Tipo de pregunta:** Debugging (típica de finales ITAM)

**Dificultad:** difícil

**Tablas involucradas:**
- `propietario`, `vehiculo`, `infraccion`

**Patrones relacionados:**
- GROUP BY con columnas no agregadas
- WHERE sobre columna agregada (debe ir en HAVING)
- JOIN con condición incompleta

**Trampas típicas:**
- Mezclar columnas no agregadas en SELECT cuando hay GROUP BY.
- Filtrar `COUNT(*) > 5` en WHERE en vez de HAVING.

**Enunciado:**
Un compañero quiere listar los propietarios con más de 3 infracciones, junto con el modelo del vehículo y el total de infracciones. Escribió esto y le da error / resultados incorrectos. **Encuentra todos los errores y reescribe la query correcta:**

```sql
SELECT p.nombre, p.apellido, v.marca, COUNT(i.id)
FROM   propietario p
JOIN   vehiculo v
JOIN   infraccion i ON i.vehiculo_id = v.id
WHERE  COUNT(i.id) > 3
GROUP  BY p.id;
```

---

### Solución paso a paso

**Error 1 — JOIN sin ON.**
```sql
JOIN vehiculo v   -- falta ON v.propietario_id = p.id
JOIN infraccion i ON i.vehiculo_id = v.id
```
Sin la condición de join entre `propietario` y `vehiculo`, se generaría un cross join (cada propietario con cada vehículo). En algunos motores ni siquiera compila.

**Error 2 — `WHERE COUNT(...)`.**
`COUNT` es agregación; los WHERE filtran **filas individuales antes de agregar**. No se puede usar agregación ahí. Debe ir en **HAVING**.

**Error 3 — Columnas no agregadas en SELECT sin estar en GROUP BY.**
`SELECT p.nombre, p.apellido, v.marca` pero `GROUP BY p.id`. En SQL estándar, `nombre`, `apellido` y `marca` deben estar en GROUP BY (o ser agregadas). PostgreSQL permite `p.nombre, p.apellido` si `p.id` es PK (porque está funcionalmente determinada), pero `v.marca` definitivamente no — un propietario puede tener varios vehículos con marcas distintas.

**Error 4 — `v.marca` no tiene sentido si hay varios vehículos.**
Conceptualmente: si un propietario tiene Tsuru y Civic, ¿qué marca mostrar? Hay que decidir: ¿agregar marcas con `STRING_AGG`? ¿Mostrar una por fila (entonces no es "por propietario")?

**Reescritura correcta — versión "por propietario":**

```sql
SELECT   p.id,
         p.nombre,
         p.apellido,
         STRING_AGG(DISTINCT v.marca, ', ' ORDER BY v.marca) AS marcas,
         COUNT(i.id) AS total_infracciones
FROM     propietario p
JOIN     vehiculo v   ON v.propietario_id = p.id
JOIN     infraccion i ON i.vehiculo_id = v.id
GROUP BY p.id, p.nombre, p.apellido
HAVING   COUNT(i.id) > 3
ORDER BY total_infracciones DESC;
```

**Reescritura correcta — versión "por propietario+vehículo":**

```sql
SELECT   p.id,
         p.nombre,
         p.apellido,
         v.marca,
         COUNT(i.id) AS total_infracciones
FROM     propietario p
JOIN     vehiculo v   ON v.propietario_id = p.id
JOIN     infraccion i ON i.vehiculo_id = v.id
GROUP BY p.id, p.nombre, p.apellido, v.id, v.marca
HAVING   COUNT(i.id) > 3
ORDER BY total_infracciones DESC;
```

---

### Query final (la versión "por propietario" que es la interpretación más natural)

```sql
SELECT   p.id,
         p.nombre,
         p.apellido,
         COUNT(i.id) AS total_infracciones
FROM     propietario p
JOIN     vehiculo v   ON v.propietario_id = p.id
JOIN     infraccion i ON i.vehiculo_id = v.id
GROUP BY p.id, p.nombre, p.apellido
HAVING   COUNT(i.id) > 3
ORDER BY total_infracciones DESC;
```

---

### Explicación

- **Lección 1:** WHERE filtra filas; HAVING filtra grupos (resultados de GROUP BY). `COUNT`, `SUM`, `AVG`, `MAX`, `MIN` van en HAVING (o en subquery).
- **Lección 2:** Cada JOIN necesita su ON (excepto NATURAL JOIN y CROSS JOIN, que son casos especiales). Sin ON, el JOIN se vuelve cross join.
- **Lección 3:** GROUP BY debe incluir todas las columnas no agregadas del SELECT (o sólo aquellas determinadas funcionalmente por la PK incluida).

---

## Ejercicio 32 — MUY DIFÍCIL: top vehículo por alcaldía con desempate

**Keywords para buscar:** `window function`, `RANK`, `PARTITION BY`, `desempate`, `top por grupo`, `ITAM`, `MUY difícil`, `top-N por categoría`

**Tipo de pregunta:** SQL — window function avanzada

**Dificultad:** MUY difícil

**Tablas involucradas:**
- `infraccion`, `vehiculo`, `camara`

**Relaciones usadas del ERD:**
- `infraccion` → `vehiculo` (vehiculo_id)
- `infraccion` → `camara` (camara_id, y de ahí saco alcaldía)

**Patrones relacionados:**
- `RANK() OVER (PARTITION BY alcaldia ORDER BY total DESC)`
- Filtrar por rank = 1 incluyendo empates

**Trampas típicas:**
- `RANK = 1` puede dar varios "top" en una alcaldía si empatan. Si quiero estrictamente uno, uso `ROW_NUMBER` (rompe empate arbitrariamente).
- Si uso `LIMIT 1` ingenuo, sólo me da un vehículo de una alcaldía.

**Enunciado:**
Para cada alcaldía, identifica el (o los) vehículo(s) con **más infracciones registradas en cámaras de esa alcaldía**. Si hay empate, lista todos. Devuelve: alcaldía, placa, total_infracciones.

---

### Solución paso a paso

1. **CTE 1**: contar infracciones por par (vehículo, alcaldía).
2. **Window function**: dentro de cada partición de alcaldía, asignar `RANK` por total de infracciones (DESC).
3. **Filtro**: `rk = 1` me da el top (con empates incluidos por RANK).

---

### Query final

```sql
WITH conteo_por_vehiculo_alcaldia AS (
    SELECT   v.id     AS vehiculo_id,
             v.placa,
             c.alcaldia,
             COUNT(*) AS total_infracciones
    FROM     infraccion i
    JOIN     vehiculo   v ON v.id = i.vehiculo_id
    JOIN     camara     c ON c.id = i.camara_id
    GROUP BY v.id, v.placa, c.alcaldia
),
rankeado AS (
    SELECT *,
           RANK() OVER (PARTITION BY alcaldia
                        ORDER BY total_infracciones DESC) AS rk
    FROM   conteo_por_vehiculo_alcaldia
)
SELECT   alcaldia,
         placa,
         total_infracciones
FROM     rankeado
WHERE    rk = 1
ORDER BY alcaldia, placa;
```

---

### Explicación de la query

- **CTE 1**: pareja `(vehiculo, alcaldia)` con su conteo. Importante: el vehículo puede haberse multado en varias alcaldías; cada combinación es una fila aquí.
- **`RANK() OVER (PARTITION BY alcaldia ORDER BY total DESC)`**:
  - Reinicia el ranking por cada alcaldía.
  - DESC porque queremos mayor a menor.
  - RANK deja empates compartiendo posición (1, 1, 3, 4...). Si quisiera "uno y sólo uno por alcaldía" usaría `ROW_NUMBER`.
- **`WHERE rk = 1`** sólo es válido si el filtro se aplica DESPUÉS de la window function. Por eso necesito la CTE rankeado — no puedo poner `WHERE RANK() = 1` directamente.

---

## Ejercicio 33 — MUY DIFÍCIL: detección de fraude (pagos sospechosos)

**Keywords para buscar:** `HAVING SUM`, `pagos vs adeudo`, `over-payment`, `fraude`, `lógica de negocio`, `MUY difícil`, `combinado`

**Tipo de pregunta:** SQL — combinado complejo

**Dificultad:** MUY difícil

**Tablas involucradas:**
- `infraccion`, `pago`

**Patrones relacionados:**
- Comparar agregación contra valor no agregado
- HAVING con comparación entre dos agregaciones

**Trampas típicas:**
- `infraccion.importe` no es agregado; sin embargo, debe aparecer en GROUP BY o `MAX(i.importe)`.
- Comparar `SUM(p.importe) > MAX(i.importe)` o `> i.importe` (si se agrupa por infraccion.id).

**Enunciado:**
Identifica infracciones cuyo **total pagado excede el importe de la infracción** (posible error de cobro o fraude). Devuelve `id_infraccion`, `importe_original`, `total_pagado`, `excedente`.

---

### Solución paso a paso

1. Agrupar pagos por infracción → suma de pagos.
2. Comparar contra el importe original.
3. Filtrar cuando `suma_pagos > importe`.
4. Calcular `excedente = suma_pagos − importe`.

---

### Query final

```sql
WITH total_pagado AS (
    SELECT   infraccion_id,
             SUM(importe) AS pagado
    FROM     pago
    GROUP BY infraccion_id
)
SELECT   i.id                              AS id_infraccion,
         i.importe                         AS importe_original,
         tp.pagado                         AS total_pagado,
         tp.pagado - i.importe             AS excedente
FROM     infraccion i
JOIN     total_pagado tp ON tp.infraccion_id = i.id
WHERE    tp.pagado > i.importe
ORDER BY excedente DESC;
```

Versión sin CTE (con HAVING):

```sql
SELECT   i.id                                                AS id_infraccion,
         i.importe                                           AS importe_original,
         SUM(p.importe)                                      AS total_pagado,
         SUM(p.importe) - i.importe                          AS excedente
FROM     infraccion i
JOIN     pago p ON p.infraccion_id = i.id
GROUP BY i.id, i.importe
HAVING   SUM(p.importe) > i.importe
ORDER BY excedente DESC;
```

---

### Explicación de la query

- La **versión con CTE** es más legible y eficiente: primero agrego pagos, luego comparo. Una sola pasada por `pago`.
- La **versión con HAVING** mezcla todo en una pasada y usa que `i.importe` esté funcionalmente determinado por `i.id` (que sí es PK) → válido incluso en SQL estándar estricto.
- **Excedente** se calcula sólo en infracciones que pasaron el filtro.
- **Caso borde:** ¿qué pasa con infracciones sin pagos? No aparecen en `total_pagado`, por lo tanto el JOIN los excluye → no son sospechosas y eso es lo correcto.

---

## Ejercicio 34 — MUY DIFÍCIL: cohorts mensuales con porcentaje móvil

**Keywords para buscar:** `LAG`, `LEAD`, `crecimiento porcentual`, `cohort`, `mes sobre mes`, `MoM`, `series temporales`, `ventana móvil`, `MUY difícil`

**Tipo de pregunta:** SQL — análisis temporal con window functions

**Dificultad:** MUY difícil

**Tablas involucradas:**
- `infraccion`

**Patrones relacionados:**
- `DATE_TRUNC('month', fecha)` para agrupar por mes
- `LAG(...) OVER (ORDER BY mes)` para acceder a fila anterior
- Crecimiento porcentual = (actual − anterior) / anterior

**Trampas típicas:**
- Primer mes no tiene mes anterior → LAG da NULL → división produce NULL (no error, pero hay que recordar manejarlo).
- Asumir todos los meses existen aunque no tengan infracciones (¿necesitas `generate_series`?).

**Enunciado:**
Genera un reporte mes a mes con:
- mes (truncado),
- total de infracciones en ese mes,
- total del mes anterior,
- crecimiento absoluto,
- crecimiento porcentual respecto al mes anterior (% con 2 decimales).

---

### Solución paso a paso

1. **CTE 1 (`por_mes`)**: agrupar `infraccion` por `DATE_TRUNC('month', fecha)`.
2. **CTE 2 o SELECT final**: window function `LAG(total) OVER (ORDER BY mes)` para acceder al mes previo.
3. Calcular crecimiento absoluto y porcentual.
4. Usar `NULLIF(prev, 0)` para evitar división por cero (importante el primer mes y meses inactivos).

---

### Query final

```sql
WITH por_mes AS (
    SELECT   DATE_TRUNC('month', fecha)::date AS mes,
             COUNT(*)                         AS total_mes
    FROM     infraccion
    GROUP BY DATE_TRUNC('month', fecha)
)
SELECT
    mes,
    total_mes,
    LAG(total_mes) OVER (ORDER BY mes)                                          AS total_mes_anterior,
    total_mes - LAG(total_mes) OVER (ORDER BY mes)                              AS crecimiento_absoluto,
    ROUND(
        100.0 * (total_mes - LAG(total_mes) OVER (ORDER BY mes))
              / NULLIF(LAG(total_mes) OVER (ORDER BY mes), 0),
        2
    )                                                                           AS crecimiento_pct
FROM        por_mes
ORDER BY    mes;
```

---

### Explicación de la query

- **`DATE_TRUNC('month', fecha)`** convierte `2025-03-17 14:22:31` en `2025-03-01 00:00:00`. Así todas las fechas del mismo mes se agrupan.
- **`LAG(total_mes) OVER (ORDER BY mes)`**: en cada fila, obtengo el `total_mes` de la fila anterior (cronológicamente).
- **`NULLIF(prev, 0)`**: si el mes anterior tuvo 0 infracciones, evito división por cero (regresa NULL).
- **Primera fila**: `LAG` regresa NULL → crecimiento_absoluto y pct son NULL. Esperable.
- **Mejora opcional**: si quieres llenar meses sin infracciones (que no aparecerían en la CTE 1), usa `generate_series(min(fecha), max(fecha), '1 month')` en un LEFT JOIN.

---

## Ejercicio 35 — MUY DIFÍCIL: examen integrador completo (estilo final ITAM)

**Keywords para buscar:** `integrador`, `final ITAM`, `combinado todo`, `transacción`, `ALTER`, `UPDATE`, `agregación`, `CASE`, `MUY difícil`

**Tipo de pregunta:** Integradora (mezcla DDL + DML + análisis)

**Dificultad:** MUY difícil

**Tablas involucradas:**
- `propietario`, `vehiculo`, `infraccion`, `pago`

**Patrones relacionados:**
- Todo lo anterior junto: transacción + ALTER + UPDATE con CASE + JOIN agregado

**Enunciado:**

La Tesorería de la CDMX quiere ejecutar una clasificación masiva de propietarios. Tu tarea, en **una sola transacción atómica**:

1. Agrega a la tabla `propietario` una columna `categoria_morosidad` de tipo VARCHAR(15) con default `'al_corriente'` y NOT NULL.
2. Agrega una columna `total_adeudado` numeric(12, 2) con default 0 y NOT NULL.
3. Para cada propietario, calcula el adeudo total (suma de `infraccion.importe − pagos asociados`, sólo cuando es > 0) y guárdalo en `total_adeudado`.
4. Clasifica:
   - `'al_corriente'` si `total_adeudado = 0`.
   - `'leve'` si `0 < total_adeudado ≤ 1000`.
   - `'medio'` si `1000 < total_adeudado ≤ 5000`.
   - `'grave'` si `total_adeudado > 5000`.
5. Crea un índice sobre `categoria_morosidad` para futuras búsquedas frecuentes.
6. Confirma la transacción.

---

### Solución paso a paso

1. `BEGIN` para abrir transacción.
2. `ALTER TABLE` con dos columnas (puede ser una sentencia o dos).
3. UPDATE complejo que combina:
   - Subquery agregada que calcula `adeudo_total` por propietario (vía vehiculo → infraccion → pago).
   - `COALESCE` para propietarios sin infracciones (adeudo = 0).
4. Segundo UPDATE para `categoria_morosidad` usando `CASE`.
5. `CREATE INDEX`.
6. `COMMIT`.

---

### Query final

```sql
BEGIN;

------------------------------------------------------------------
-- 1 & 2. ALTER TABLE: añadir dos columnas con defaults
------------------------------------------------------------------
ALTER TABLE propietario
    ADD COLUMN categoria_morosidad VARCHAR(15)   NOT NULL DEFAULT 'al_corriente',
    ADD COLUMN total_adeudado      NUMERIC(12,2) NOT NULL DEFAULT 0;

------------------------------------------------------------------
-- 3. Calcular total_adeudado por propietario
------------------------------------------------------------------
WITH pago_por_infraccion AS (
    SELECT   infraccion_id,
             SUM(importe) AS pagado
    FROM     pago
    GROUP BY infraccion_id
),
adeudo_por_propietario AS (
    SELECT   v.propietario_id,
             SUM(GREATEST(i.importe - COALESCE(p.pagado, 0), 0)) AS total
    FROM     vehiculo v
    JOIN     infraccion i ON i.vehiculo_id = v.id
    LEFT     JOIN pago_por_infraccion p ON p.infraccion_id = i.id
    GROUP BY v.propietario_id
)
UPDATE propietario pr
SET    total_adeudado = COALESCE(ap.total, 0)
FROM   adeudo_por_propietario ap
WHERE  pr.id = ap.propietario_id;
-- (los propietarios sin coincidencia conservan el default 0)

------------------------------------------------------------------
-- 4. Clasificar categoria_morosidad con CASE
------------------------------------------------------------------
UPDATE propietario
SET    categoria_morosidad = CASE
           WHEN total_adeudado = 0                           THEN 'al_corriente'
           WHEN total_adeudado >  0    AND total_adeudado <= 1000 THEN 'leve'
           WHEN total_adeudado >  1000 AND total_adeudado <= 5000 THEN 'medio'
           WHEN total_adeudado >  5000                       THEN 'grave'
       END;

------------------------------------------------------------------
-- 5. Índice para queries frecuentes por categoría
------------------------------------------------------------------
CREATE INDEX idx_propietario_categoria_morosidad
ON propietario (categoria_morosidad);

------------------------------------------------------------------
-- 6. Confirmar
------------------------------------------------------------------
COMMIT;
```

---

### Explicación de la query

- **Todo dentro de `BEGIN ... COMMIT`** → atomicidad. Si cualquier paso falla, los ALTER y UPDATE se revierten (en PostgreSQL, las DDL son transaccionales).
- **`GREATEST(x, 0)`**: evita restar negativos si por error hay sobre-pago (ver Ej 33). Sólo cuenta como adeudo cuando hay saldo positivo.
- **`LEFT JOIN` con `COALESCE`**: para infracciones sin pagos, `pagado` es NULL → COALESCE lo trata como 0.
- **Propietarios sin infracciones**: no aparecen en `adeudo_por_propietario`, así que el `UPDATE` no los toca → conservan el default `0` y `'al_corriente'`. ✅ Correcto.
- **CASE en UPDATE**: una sola pasada por la tabla, asigna categoría según el adeudo ya calculado.
- **Índice B-tree** sobre la columna recién creada → futuras queries `WHERE categoria_morosidad = 'grave'` serán rápidas.
- **Orden importa**: primero ALTER, luego UPDATE; no se puede UPDATE una columna que aún no existe.

---


---

# 📋 Plantillas SQL listas para copiar y adaptar en el examen

Esta sección concentra las plantillas más usadas. Memorízalas o ten esta sección abierta en Ctrl+F.

## 🎯 Plantilla 1 — SELECT con JOINs múltiples

```sql
SELECT   <columnas>
FROM     <tabla_1> a1
JOIN     <tabla_2> a2 ON a2.<fk> = a1.<pk>
LEFT     JOIN <tabla_3> a3 ON a3.<fk> = a2.<pk>
WHERE    <condiciones sobre filas individuales>
GROUP BY <columnas no agregadas>
HAVING   <condiciones sobre agregados>
ORDER BY <columnas> [ASC|DESC]
LIMIT    <N>;
```

## 🎯 Plantilla 2 — Top N por grupo con window function

```sql
WITH rankeado AS (
    SELECT   <columnas>,
             RANK() OVER (PARTITION BY <grupo>
                          ORDER BY <métrica> DESC) AS rk
    FROM     <tabla>
)
SELECT *
FROM   rankeado
WHERE  rk <= <N>;
```

Variantes:
- `ROW_NUMBER()` → uno y sólo uno por grupo (desempata arbitrariamente).
- `RANK()` → permite empates con misma posición, salta números (1, 1, 3...).
- `DENSE_RANK()` → permite empates, no salta (1, 1, 2...).

## 🎯 Plantilla 3 — Running total / running count

```sql
SELECT   <columnas>,
         COUNT(*) OVER (ORDER BY <fecha>)            AS conteo_acumulado,
         SUM(<importe>) OVER (ORDER BY <fecha>)      AS suma_acumulada
FROM     <tabla>
ORDER BY <fecha>;
```

Por grupo (ej: por mes):
```sql
COUNT(*) OVER (PARTITION BY DATE_TRUNC('month', fecha) ORDER BY fecha)
```

## 🎯 Plantilla 4 — Anti-join (los X sin Y)

```sql
SELECT x.*
FROM   x
WHERE  NOT EXISTS (
           SELECT 1
           FROM   y
           WHERE  y.x_id = x.id
       );
```

Equivalente:
```sql
SELECT x.*
FROM   x
LEFT   JOIN y ON y.x_id = x.id
WHERE  y.id IS NULL;
```

## 🎯 Plantilla 5 — Agregación condicional

```sql
SELECT   <grupo>,
         COUNT(*) FILTER (WHERE <condicion>)                       AS n_cond,
         SUM(<col>) FILTER (WHERE <condicion>)                     AS suma_cond,
         COUNT(*) FILTER (WHERE <otra>)                            AS n_otra
FROM     <tabla>
GROUP BY <grupo>;
```

Equivalente SQL estándar (sin `FILTER`):
```sql
SUM(CASE WHEN <condicion> THEN 1 ELSE 0 END)
SUM(CASE WHEN <condicion> THEN <col> ELSE 0 END)
```

## 🎯 Plantilla 6 — CREATE TABLE típica de examen

```sql
CREATE TABLE <nombre> (
    id              BIGSERIAL       PRIMARY KEY,
    <campo_obl>     <TIPO>          NOT NULL,
    <campo_único>   <TIPO>          NOT NULL UNIQUE,
    <campo_check>   <TIPO>          NOT NULL CHECK (<condicion>),
    <campo_def>     <TIPO>          NOT NULL DEFAULT <valor>,
    <campo_opc>     <TIPO>,

    <fk_col>        BIGINT          NOT NULL,
    FOREIGN KEY (<fk_col>)
        REFERENCES <tabla_padre>(id)
        ON DELETE CASCADE        -- o RESTRICT, SET NULL, NO ACTION
        ON UPDATE CASCADE
);
```

## 🎯 Plantilla 7 — Transacción ALTER + UPDATE atómica

```sql
BEGIN;
    ALTER TABLE <t> ADD COLUMN <c> <TIPO> NOT NULL DEFAULT <valor>;

    UPDATE <t>
    SET    <c> = CASE
                     WHEN <cond_1> THEN <v1>
                     WHEN <cond_2> THEN <v2>
                     ELSE <v_default>
                 END;
COMMIT;
```

## 🎯 Plantilla 8 — CTE encadenadas

```sql
WITH paso_1 AS (
    SELECT ...
),
paso_2 AS (
    SELECT ... FROM paso_1 ...
),
paso_3 AS (
    SELECT ... FROM paso_2 ...
)
SELECT ...
FROM   paso_3;
```

## 🎯 Plantilla 9 — CREATE INDEX

```sql
-- Índice simple
CREATE INDEX idx_<tabla>_<col>
ON <tabla> (<col>);

-- Índice compuesto (igualdad primero, rango después)
CREATE INDEX idx_<tabla>_<col1>_<col2>
ON <tabla> (<col_igualdad>, <col_rango>);

-- Índice parcial
CREATE INDEX idx_<tabla>_<cond>
ON <tabla> (<col>)
WHERE <condicion>;

-- Índice único
CREATE UNIQUE INDEX uq_<tabla>_<col>
ON <tabla> (<col>);
```

## 🎯 Plantilla 10 — CREATE VIEW

```sql
-- Vista simple (actualizable si es de una tabla, sin agregaciones)
CREATE VIEW vw_<nombre> AS
SELECT <columnas>
FROM   <tabla>
WHERE  <filtro>
WITH   CHECK OPTION;

-- Vista compleja (NO actualizable)
CREATE VIEW vw_<nombre> AS
SELECT <columnas con joins/agregaciones>
FROM   <t1> JOIN <t2> ...
GROUP BY ...;
```

---

# ⚠️ Errores frecuentes en el examen (anti-patrones)

Esta es una lista de errores que el profesor ITAM **suele detectar y penalizar**. Léela el día anterior al examen.

| # | Error | Por qué está mal | Forma correcta |
|---|-------|------------------|----------------|
| 1 | Usar `WHERE` con agregaciones | WHERE filtra antes de agregar | Usar `HAVING` |
| 2 | Olvidar columnas no agregadas en `GROUP BY` | SQL estándar lo prohíbe | Incluir todas las no-agregadas o agregarlas |
| 3 | `NOT IN (subquery con NULLs)` | Devuelve 0 filas si hay NULL | Usar `NOT EXISTS` |
| 4 | `JOIN` sin `ON` | Genera cross join silencioso | Siempre poner ON explícito |
| 5 | Top N con `LIMIT N` sin manejar empates | Corta arbitrariamente | Usar `DENSE_RANK()` y filtrar `<= N` |
| 6 | `SUM(col)` sin `COALESCE(..., 0)` tras LEFT JOIN | Devuelve NULL si no hay filas | Envolver con `COALESCE` |
| 7 | Dividir entre columna que puede ser 0 | Error de división | Usar `NULLIF(x, 0)` |
| 8 | Comparar fechas con strings sin cast | Comparación lexicográfica errónea | `DATE '2025-01-01'` o `CAST(... AS DATE)` |
| 9 | Olvidar `BEGIN`/`COMMIT` en cambios masivos | Si falla a la mitad, queda inconsistente | Envolver siempre en transacción |
| 10 | Tabla pivote sin PK compuesta | Permite duplicados de la relación | `PRIMARY KEY (col_a, col_b)` |
| 11 | Decir "está en 3FN" sin verificar FNBC | FNBC es más estricta | Revisar: ¿toda flecha sale de superllave? |
| 12 | Confundir DF con DMV | Diferente lógica | DF: 1 valor → 1 valor. DMV: 1 valor → conjunto de valores |
| 13 | DF "trivial" mal definida | Reglas: trivial sí Y ⊆ X | Para DMV: trivial si Y ⊆ X **o** X∪Y = atributos totales |
| 14 | `CREATE INDEX` con orden invertido en compuesto | Si rango va primero, el índice no aprovecha la igualdad de la 2ª col | Orden: igualdad → rango |
| 15 | Olvidar `NOT NULL` en FK obligatoria | Permite huérfanos lógicos aunque la FK exista | Combinar `NOT NULL` + `REFERENCES` |
| 16 | `ON DELETE CASCADE` por defecto en todo | A veces es peligroso (borras propietario y se borran todas sus multas históricas) | Pensar caso por caso: CASCADE / RESTRICT / SET NULL |
| 17 | Window function en `WHERE` directamente | No se puede; se evalúan después de WHERE | Encapsular en CTE y filtrar fuera |
| 18 | Asumir orden sin `ORDER BY` | SQL no garantiza orden de salida | Siempre `ORDER BY` cuando importa |
| 19 | `SELECT *` con `GROUP BY` | Casi siempre rompe la regla de columnas | Listar columnas explícitamente |
| 20 | Confundir `EXISTS` con `IN`: pensar que dan lo mismo siempre | Diferencia con NULLs y rendimiento | Preferir `EXISTS` para correlación |

---

# 🗺️ Mapa final de decisión: ¿qué herramienta usar?

```
                          ¿QUÉ NECESITA LA PREGUNTA?
                                    │
        ┌───────────────────────────┼────────────────────────────┐
        ▼                           ▼                            ▼
  CONSULTAR DATOS           MODIFICAR ESQUEMA            DISEÑAR / EVALUAR
        │                           │                            │
   ┌────┼────┐               ┌──────┼──────┐                ┌────┼────┐
   ▼    ▼    ▼               ▼      ▼      ▼                ▼    ▼    ▼
 SELECT JOIN AGREG    CREATE  ALTER  DROP             ER   FN   ÍNDICES
   │    │    │       TABLE   TABLE  TABLE              │    │    │
   ▼    ▼    ▼         │                              │    │    │
una   2+   GROUP      │                              │    │   B-tree vs Hash
tabla tab. BY         │                              │    │
        │   │       constraints                      │  ¿flecha sale de
        │  HAVING   (PK, FK, CHECK,                  │   superllave?
        │           NOT NULL, UNIQUE, DEFAULT)       │       │
       JOIN                                          │     FNBC sí/no
       /│\                                         cardinalidad
      / | \                                       (1-1, 1-N, M-N)
   INNER LEFT RIGHT
   FULL  CROSS
```

```
            ¿NECESITAS HACER "TOP N POR GRUPO"?
                          │
              ┌───────────┴───────────┐
              ▼                       ▼
       ¿ACEPTAS EMPATES?           ¿N FIJO?
              │                       │
        ┌─────┼─────┐                 ▼
        ▼     ▼     ▼              LIMIT N
       sí    no    no              (sin grupo)
        │     │
   ┌────┘     └────┐
   ▼               ▼
RANK()         ROW_NUMBER()
o              (desempata
DENSE_RANK     arbitrario)
   │
filtrar rk <= N
en CTE externa
```

```
        ¿LOS X QUE NO TIENEN Y?
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
  NOT EXISTS  LEFT JOIN  NOT IN
  (preferido) IS NULL   ⚠️ FALLA
                        con NULLs
```

---

# 🎯 Checklist final: 24 horas antes del examen

## ✅ Día anterior (tarde)

- [ ] Repasar el **ERD de foto-multas** hasta poder dibujarlo de memoria con tipos de datos.
- [ ] Memorizar las 6 cardinalidades: propietario→vehiculo (1:N), vehiculo→infraccion (1:N), camara→infraccion (1:N), infraccion→pago (1:N), propietario→pago (vía acreedor_id, 1:N).
- [ ] Memorizar la trampa clave: `pago.acreedor_id` apunta a `propietario.id` (no a "acreedor").
- [ ] Revisar las plantillas SQL de arriba (10 minutos).
- [ ] Resolver los 5 ejercicios MUY difíciles (Ej 28, 32, 33, 34, 35) sin mirar la solución.
- [ ] Releer la sección de "Errores frecuentes" (5 minutos).
- [ ] Dormir mínimo 7 horas.

## ✅ Mañana del examen

- [ ] Desayunar (no exagerar con azúcar/café).
- [ ] Repasar SÓLO los conceptos clave (no aprender nada nuevo):
  - DF vs DMV trivial
  - Cuándo es FNBC
  - Diferencia WHERE vs HAVING
  - Window functions
  - ACID
- [ ] Llegar 15 minutos antes.

## ✅ Durante el examen (estrategia)

1. **Lee TODAS las preguntas primero** (5 minutos). Detecta cuáles son fáciles y atácalas primero.
2. **Asegura puntos fáciles**: preguntas tipo Q1, Q2, Q6, Q7 son las más predecibles.
3. **Marca dudas con asterisco**, no te atores. Vuelve al final.
4. **En SQL**:
   - Identifica tablas necesarias y caminos de join ANTES de escribir.
   - Empieza por el `SELECT FROM`, luego JOINs, luego WHERE, luego GROUP BY, luego HAVING, luego ORDER BY.
   - Si la query usa agregación, pregúntate: ¿estoy filtrando filas (WHERE) o grupos (HAVING)?
   - Si la pregunta dice "top N", pregunta si admite empates → window function o `LIMIT`.
5. **En normalización**:
   - Lista todas las DFs.
   - Encuentra llaves candidatas.
   - Verifica una por una: ¿el lado izquierdo es superllave? Si NO → FNBC violada.
6. **En DDL**:
   - PRIMARY KEY ✅
   - NOT NULL en obligatorias ✅
   - FK con su REFERENCES ✅
   - CHECK donde haya restricción ✅
   - DEFAULT donde aplique ✅
   - Acciones referenciales explícitas (CASCADE / RESTRICT) ✅
7. **Última revisión** (10 minutos): relee tus queries verificando puntuación, comas, alias.

## ✅ Si te quedas en blanco

- Vuelve al ERD. Dibújalo. **Casi cualquier pregunta SQL del examen se resuelve con caminos por el ERD.**
- Si no sabes la teoría, escribe lo que sí sabes. Puntos parciales.
- En normalización, si dudas, **descompón**: nunca pierdes puntos por proponer una descomposición justificada.

---

# 🧠 Resumen visual final (una sola hoja)

## Las 7 verdades del examen ITAM de BD

1. **`pago.acreedor_id → propietario.id`**. NO hay tabla "acreedor".
2. **PK siempre es `id` (artificial)** en este ERD. `placa` NO es PK.
3. **DF trivial:** Y ⊆ X. **DMV trivial:** Y ⊆ X **o** X ∪ Y = todos los atributos.
4. **FNBC:** toda flecha sale de superllave.
5. **WHERE** filtra filas individuales antes de agregar. **HAVING** filtra grupos después.
6. **Índice compuesto:** igualdad antes que rango. Hash NO sirve para rangos.
7. **Transacción ACID:** `BEGIN; ... COMMIT;` envuelve cambios atómicos. Si falla, `ROLLBACK` o crash → todo se deshace.

## Las 5 plantillas más probables

1. **JOIN básico con filtro y orden** (Q6-tipo).
2. **GROUP BY + HAVING + COUNT** umbral (Q7-tipo).
3. **Top N con window function** y empates (Q8-tipo).
4. **Window function: running count o LAG** (Q9-tipo).
5. **ALTER TABLE + UPDATE en transacción** (Q10-tipo) o **CREATE TABLE con FK CASCADE** (Q11-tipo).

## Si te aprendes UN solo párrafo, que sea este:

> Toda query empieza identificando tablas y FKs necesarias, recorre el camino del ERD, agrega filtros con WHERE antes de agregar y HAVING después. Las window functions resuelven "top por grupo" y "acumulados temporales". La normalización a FNBC exige que cada flecha (DF) salga de una superllave. La integridad referencial se garantiza con FKs, opcionalmente con CASCADE para borrado en cadena. Los índices B-tree aceleran igualdad y rango (en ese orden si son compuestos); los Hash sólo igualdad. Toda modificación masiva se envuelve en BEGIN/COMMIT para garantizar atomicidad ACID.

---

# 🚀 Última frase

Tienes el ERD memorizado, las plantillas memorizadas, los 35 ejercicios resueltos. **El examen es tuyo. Vas a romperla.**
