# Etapa 3 — Base de conocimiento (`kb-creator`)

> Documento explicativo de la Etapa 3 del trabajo de integración (SDD + Active Stack).
> Evidencia asociada: ver `evidencia-etapa-3.md` en esta misma carpeta.

## 1. Qué pide la consigna

> **Etapa 3. Base de conocimiento (`kb-creator`)**
> Ejecutar la etapa. Al existir documentación fuente en `docs/`, la skill puede trabajar en modo silencioso; si les hace preguntas (modo interactivo), respóndanlas con criterio y en base a lo investigado, no con respuestas al azar.
> **Resultado esperado**: la carpeta `knowledge-base/` con los diez archivos canónicos: visión, descripción, actores, modelos de datos, reglas de negocio, features, flujos, arquitectura, decisiones y preguntas abiertas.
> **Revisión obligatoria (Ajustar si corresponde)**: verificar que la knowledge-base refleje el informe de Discovery (competidores, MVP recomendado, vacíos del mercado) y no un producto genérico. Como mínimo, comprobar que las reglas de negocio incluyan las de agenda (duración de prestaciones, sillones o boxes, prevención de solapamientos) y que "preguntas abiertas" contenga los puntos que el Discovery dejó como "No evidenciado".

## 2. Qué dice el marco teórico

`presentacion-02-flujo-de-trabajo.pdf`:

- **Diap. 4 y 7** — `kb-creator` "Construye la base de conocimiento". Tiene **dos modos**:
  - **Modo silencioso**: si ya hay documentación fuente en `docs/`, "genera toda la knowledge-base directo, sin preguntar nada".
  - **Modo interactivo**: si no hay nada previo, "actúa como un arquitecto senior y hace de 3 a 5 preguntas estratégicas por ronda".
- **Resultado (diap. 7):** una carpeta `knowledge-base/` con **10 archivos canónicos obligatorios** (visión, descripción, actores, modelos de datos, reglas de negocio, features, flujos, arquitectura, decisiones y preguntas abiertas), más archivos opcionales del dominio cuando hacen falta.

## 3. Qué se hizo en este proyecto

Se ejecutó `kb-creator` en **Modo A (silencioso / ingest)**: al existir documentación fuente en `docs/` (el informe de Discovery), la skill leyó los documentos y generó la base de conocimiento **sin preguntar nada**.

Resultado: la carpeta `knowledge-base/` con los **10 archivos canónicos + `README.md`**:

| Archivo | Contenido (según el README de la KB) |
|---|---|
| `01_vision_y_objetivos.md` | Propósito, objetivos por actor, alcance v1, fuera de alcance, métricas |
| `02_descripcion_general.md` | Stack decidido, arquitectura, integraciones, API REST |
| `03_actores_y_roles.md` | Actores, matriz RBAC, rutas públicas y privadas |
| `04_modelo_de_datos.md` | 5 dominios, ERD, 11 entidades, seed, restricción de exclusión |
| `05_reglas_de_negocio.md` | 4 dominios de reglas con códigos RN, más excepciones globales |
| `06_funcionalidades.md` | 7 épicas, 18 historias de usuario con criterios de aceptación |
| `07_flujos_principales.md` | 8 flujos extremo a extremo, incluido el intento de doble reserva |
| `08_arquitectura_propuesta.md` | Patrones, estructura de directorios, seguridad, variables de entorno |
| `09_decisiones_y_supuestos.md` | 8 decisiones documentadas y 8 supuestos con su riesgo |
| `10_preguntas_abiertas.md` | 4 inconsistencias, 10 puntos no evidenciados, 12 preguntas priorizadas |
| `README.md` | Índice, quick start, resumen ejecutivo y advertencia de honestidad |

El `README.md` de la KB declara el modo: *"Generada con la skill `kb-creator` en **Modo A (silencioso)**, a partir de documentos existentes. `source: "ingest"`."*

## 4. Revisión obligatoria (correspondencia Discovery ↔ KB)

La consigna exige que la KB refleje el Discovery y no un producto genérico. Verificación:

| Requisito de la consigna | En la KB | ✔ |
|---|---|---|
| Refleja competidores / MVP / vacíos del Discovery | `README.md` afirma que el diferencial no es la agenda sino el borde; `06_funcionalidades.md` deriva del MVP | ✔ |
| Reglas de negocio incluyen agenda (duración, sillón/box, no solapamiento) | `05_reglas_de_negocio.md` (dominio Agenda, RN-AGE-01..RN-AGE-07) | ✔ |
| "Preguntas abiertas" contiene los "No evidenciado" del Discovery | `10_preguntas_abiertas.md` (10 puntos no evidenciados) | ✔ |

### Advertencia de honestidad registrada
La KB deja explícito un punto clave de trazabilidad: el stack **no es un hallazgo del Discovery** sino una decisión del equipo (DD-11). El `README.md` lo advierte: *"Discovery no eligió tecnologías, porque la consigna las deja libres... una decisión nuestra no es un hallazgo de la investigación"*. Y: *"Ninguno [de los 10 puntos no evidenciados] se rellenó con una estimación."*

## 5. Correspondencia con la teoría

| Punto de la teoría | En el proyecto | ✔ |
|---|---|---|
| Dos modos (silencioso si hay `docs/`, interactivo si no) | Modo A silencioso (`source: ingest`) | ✔ |
| Resultado: `knowledge-base/` con 10 canónicos | `01`..`10` + `README.md` | ✔ |
| Archivos opcionales de dominio | no aplicó (no hicieron falta) | N/A |

No se detectaron desvíos respecto del marco teórico en esta etapa.

## 6. Protocolo de inspección aplicado

Se usó **Ajustar** en el cierre de la etapa para corregir la KB contra el Discovery: ortografía/enlaces/deuda de diseño (commit `caf878e`), cifras de competencia (`80fb3d4`) y marcado de inconsistencias resueltas IN-01/02/03 (`503cfb9`). Los hallazgos quedaron registrados.

## 7. Entregables de la etapa

| Entregable | Ubicación | Estado |
|---|---|---|
| `knowledge-base/` (10 canónicos + README) | raíz | ✅ |
| Evidencia (commits, state) | `etapa 3/evidencia-etapa-3.md` | ✅ |
