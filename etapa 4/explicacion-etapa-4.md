# Etapa 4 — Roadmap (`roadmap-generator`)

> Documento explicativo de la Etapa 4 del trabajo de integración (SDD + Active Stack).
> Evidencia asociada: ver `evidencia-etapa-4.md` en esta misma carpeta.

## 1. Qué pide la consigna

La consigna define la Etapa 4 como:

> **Etapa 4. Roadmap (`roadmap-generator`)**: Generar `CHANGES.md` a partir de la knowledge-base: dependencias entre tareas, asignación con contexto suficiente, camino crítico y riesgos.
>
> **Revisión obligatoria**: el roadmap debe estar alineado con el MVP recomendado en la sección D del informe. Si incluye funcionalidades que el propio Discovery dejó para etapas posteriores, o si omite una imprescindible, usen Ajustar.

Es decir, el resultado de esta etapa es un **único artefacto versionable**: `CHANGES.md` en la raíz del repositorio, generado a partir de `knowledge-base/` (los 10 archivos canónicos).

## 2. Qué se hizo en este proyecto

Se ejecutó la skill `roadmap-generator`, que:

- Verificó las precondiciones (existe `knowledge-base/` con los 10 canónicos y existe `openspec/`).
- Leyó la KB priorizando `04_modelo_de_datos.md`, `06_funcionalidades.md`, `07_flujos_principales.md` y `08_arquitectura_propuesta.md`.
- Generó **un único archivo `CHANGES.md`** en la raíz del proyecto (no dentro de `openspec/`).

El roadmap quedó compuesto por **11 changes atómicos** (`C-01` … `C-11`), agrupados en 4 fases, y contiene:

| Sección obligatoria | Contenido en `CHANGES.md` |
|---|---|
| Cómo usar este documento | Flujo de 5 pasos para tomar un change |
| Árbol de dependencias | Árbol ASCII `C-01 → … → C-10` (+ `C-11`) |
| Paralelismo por fase | GATES 0 a 5 y qué puede correr en paralelo |
| Camino crítico y riesgos | Camino: `C-01 → C-02 → C-03 → C-04 → C-05 → C-09 → C-10`. Riesgo: se expresa por el nivel `Governance` de cada change (BAJO/MEDIO/ALTO/CRITICO) y por la nota de deuda de diseño Turno vs Bloqueo; los changes CRITICO marcan las dependencias de mayor riesgo de la cadena |
| Plan óptimo con 3 agentes | Tabla de asignación Agente A / B / C por paso |
| Secciones FASE N | Scope operativo, dependencias, governance y "Leer antes" por change |

Cada change incluye: `Estado` (`[ ]` / `[x]`), `Scope` (bullets operativos), `Dependencias`, `Governance` (BAJO/MEDIO/ALTO/CRITICO) y punteros "Leer antes" a los archivos de la KB con su sección (`§`).

## 3. Alineación con el MVP (revisión obligatoria)

El encabezado del roadmap declara explícitamente su origen:

> *"Los changes de este roadmap derivan del MVP imprescindible definido en la sección D.3 del informe de Discovery (`docs/discovery/informe-discovery.md`). Cada change se alinea con ese alcance."*

Puntos de alineación verificados:

- **Stack coherente con la KB (`02_descripcion_general.md` / DD-11):** FastAPI 3.11 + PostgreSQL 15 + React 18 (Vite) + Docker Compose.
- **Regla dura de la KB reflejada:** la restricción `EXCLUDE USING gist` (DD-05) aparece como obligación en `C-01`, `C-02` y `C-09`.
- **Deuda de diseño registrada:** la decisión Opción A (tabla única `reserva_agenda`) vs Opción B (tablas separadas) se fuerza como decisión obligatoria en `C-01`, resolviéndose a favor de la Opción A.
- **Riesgos del Discovery cubiertos:** los changes `C-05` (disponibilidad/bloqueos) y `C-09` (tests de solapamiento) atacan directamente RN-AGE-03 y RN-AGE-05, el diferencial de "no solapamiento" del producto.

## 4. Protocolo de inspección aplicado

Según el marco del trabajo, al cerrar cada etapa se decide **Continuar / Ajustar / Parar acá**. En esta etapa:

- Se usó **Ajustar** durante la generación para integrar la **deuda explícita Turno vs Bloqueo** en `C-01` (mensaje del commit: *"integra deuda Turno vs Bloqueo"*).
- El *hallazgo de auditoría* posterior (commit `226feab`) registró correcciones sobre KB, roadmap y mapeo spec-tests, confirmando el uso real del protocolo.

## 5. Entregables de la etapa

| Entregable | Ubicación | Estado |
|---|---|---|
| `CHANGES.md` (roadmap operativo) | raíz del repo | ✅ generado |
| Evidencia (commits, estado) | `etapa 4/evidencia-etapa-4.md` | ✅ |
