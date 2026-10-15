# Etapa 5 — Skills y reglas del agente (`find-skill`, `skill-registry`, `agent-instruction`)

> Documento explicativo de la Etapa 5 del trabajo de integración (SDD + Active Stack).
> Evidencia asociada: ver `evidencia-etapa-5.md` en esta misma carpeta.

## 1. Qué pide la consigna

La consigna define la Etapa 5 como:

> **Etapa 5. Skills y reglas del agente (`find-skill`, `skill-registry`, `agent-instruction`)**
> - **find-skill**: solo recomienda. Elijan qué skills instalar (o ninguna) y justifiquen la decisión en una línea por cada recomendación.
> - **skill-registry**: debe quedar generado `.atl/skill-registry.md`.
> - **agent-instruction**: es la única etapa realmente interactiva. Revisen cada regla candidata antes de confirmarla; deben quedar `AGENTS.md` y `CLAUDE.md` en la raíz. Agreguen a mano, si corresponde, al menos una regla propia del dominio (por ejemplo, "nunca almacenar datos reales de pacientes en el repositorio ni en los ejemplos").

La etapa agrupa tres skills que corren en orden dentro de `/active-orchestrator`:
`find-skill` (recomendación) → `skill-registry` (registro) → `agent-instruction` (reglas).

## 2. Sub-etapa `find-skill` (recomendación)

`find-skill` es **solo recomendación**. A partir de la knowledge-base (stack tecnológico, dominios y problema a resolver) propone qué skills adicionales instalar, pero **nunca instala ni escribe archivos por sí misma**: la decisión final siempre queda en manos del usuario (el orquestador es quien instala, y solo lo elegido en el "install gate").

**Formato de salida:** devuelve una **tabla de recomendaciones de tres columnas**:

| Nombre de la skill | Fuente (repositorio de origen) | Por qué encaja con este proyecto |
|---|---|---|

La consigna pide además que la decisión quede **justificada en una línea por cada recomendación** (o que se elija "ninguna").

**Estado en este proyecto:** no hay evidencia persistida de las recomendaciones de `find-skill` ni de la selección final (véase el hallazgo).

> ⚠️ **Hallazgo**: en el repositorio no quedó un artefacto versionado con las recomendaciones ni con su justificación: `.active-orchestrator-state.json` no tiene una sección `find-skill`/`skills` (solo `discovery`, `kb` y `registry`). Es el único punto de la Etapa 5 sin evidencia persistida.

## 3. Sub-etapa `skill-registry` (registro)

`skill-registry` **escanea todas las carpetas de skills posibles** —globales y de proyecto— de **todos los agentes soportados (Claude Code, OpenCode, Gemini CLI, Cursor, Copilot)**. Por cada skill instalada genera un **resumen compacto de 5 a 15 líneas** (solo reglas accionables y patrones clave, sin motivación ni ejemplos largos), todo consolidado en el archivo **`.atl/skill-registry.md`**.

El objetivo es el **"Skill Resolver Protocol"**: los sub-agentes que delegan trabajo no releen cada `SKILL.md` completo, sino que reciben las reglas compactas ya resueltas (menos tokens, más precisión). Se ejecutó la skill `skill-registry` y el resultado quedó versionado.

El registro contiene:

- **User Skills**: tabla `Trigger | Skill | Path` con las 7 skills indexadas.
- **Compact Rules**: resumen pre-digerido por skill (5-15 líneas; para que el delegador lo inyecte a los sub-agentes como `## Project Standards (auto-resolved)`).
- **Excluded**: skills de flujo OpenSpec/SDD (invocadas por `/opsx:*`, no como reglas).
- **Project Conventions**: mapa de archivos que son fuente de verdad (KB, CHANGES.md, estado del orquestador, etc.).

El estado del orquestador confirma la creación:

```json
"registry": {
    "created_by": "skill-registry",
    "file": ".atl/skill-registry.md",
    "skills_indexed": 7,
    "engram": "not available"
}
```

**Skills indexadas (7):** `active-orchestrator`, `agents-md-generator` (dir `agent-instruction`), `criterios-aceptacion-check`, `find-skills` (dir `find-skill`), `kb-creator`, `roadmap-generator`, `skill-creator`.

## 4. Sub-etapa `agent-instruction` (reglas del agente)

Es la **única etapa realmente interactiva** (confirma reglas candidatas con el usuario antes de escribirlas). Deriva las reglas duras **según el stack real** detectado y, antes de escribir nada, **lee el `CLAUDE.md` global ya instalado por Active Stack** para no duplicar las reglas universales que ese archivo ya define. Genera **`AGENTS.md`** y **`CLAUDE.md`** en la raíz, con **contenido idéntico** —una sola fuente de verdad— porque distintos harnesses leen uno u otro según el agente que corra.

Reglas duras stack-aware incluidas en `AGENTS.md` / `CLAUDE.md`:

| Grupo | Ejemplos de regla dura |
|---|---|
| Integridad de datos (PostgreSQL 15) | NUNCA resolver solapamiento en el backend → `EXCLUDE USING gist` + `btree_gist`; NUNCA testear solapamiento contra SQLite → PostgreSQL real en Docker |
| Arquitectura | NUNCA importar `infrastructure/` desde `domain/`; NUNCA saltar validación Pydantic en el borde |
| Seguridad / Privacidad | NUNCA guardar JWT en `localStorage` → cookie httpOnly; NUNCA hardcodear secretos; NUNCA enviar historial clínico al asistente IA |
| Frontend (React 18/Vite/TS) | NUNCA usar `any` → tsconfig estricto; componentes en `PascalCase` |
| Trazabilidad | Toda regla de negocio se referencia por su código `RN-XX` |
| Universales | NUNCA commitear/pushear sin pedido explícito; commits convencionales sin co-autoría IA |

**Reglas propias del dominio** (más allá de las genéricas de stack): no enviar historial clínico al asistente IA (DD-07), auditoría append-only (RN-PRIV-03), anulación de datos de contacto en lugar de borrado (RN-PRIV-04), `token_público` con fuente criptográfica ≥128 bits, etc. Cumple el pedido de "al menos una regla propia del dominio".

## 5. Protocolo de inspección aplicado

- `agent-instruction` es interactiva por diseño: cada regla candidata se revisó antes de confirmarla.
- El estado del orquestador pasó a `step: "done"` tras generar los artefactos de la etapa (commit `a1a2e6b`).

## 6. Entregables de la etapa

| Entregable | Ubicación | Estado |
|---|---|---|
| `.atl/skill-registry.md` | `.atl/` | ✅ generado (7 skills) |
| `AGENTS.md` | raíz | ✅ |
| `CLAUDE.md` | raíz (idéntico a AGENTS.md) | ✅ |
| Justificación `find-skill` | — | ⚠️ no persistida como archivo |
| Evidencia (commits, estado) | `etapa 5/evidencia-etapa-5.md` | ✅ |
