# Etapa 1 — Iniciar la fundación (`/active-orchestrator` y `openspec init`)

> Documento explicativo de la Etapa 1 del trabajo de integración (SDD + Active Stack).
> Evidencia asociada: ver `evidencia-etapa-1.md` en esta misma carpeta.

## 1. Qué pide la consigna

> **Etapa 1. Iniciar la fundación (`/active-orchestrator` y `openspec init`)**
> Ejecutar `/active-orchestrator` dentro del repositorio vacío. Debe correr primero `openspec init`, que deja lista la estructura base de OpenSpec.
> Cuando aparezca la pregunta de la bifurcación ("¿hacemos estudio de mercado?"), responder Sí: se decide una sola vez y en este trabajo el Discovery es obligatorio.
> **Evidencia**: el archivo de estado `.active-orchestrator-state.json` con la etapa completada (se incluye en el repositorio).

## 2. Qué dice el marco teórico

`presentacion-02-flujo-de-trabajo.pdf`:

- **Diap. 3** — El comando `/active-orchestrator` se ejecuta sobre un proyecto que todavía no tiene knowledge-base, ni roadmap, ni reglas. **Despacha siete etapas en orden fijo**, cada una resuelta por una skill distinta. "El orquestador coordina — no ejecuta" y "ninguna etapa arranca sin que la anterior esté aprobada".
- **Diap. 4** — La primera de las siete etapas es **OpenSpec Init** ("Inicia la especificación base"). El único momento de decisión es la bifurcación de Discovery, que se elige una sola vez.
- **Diap. 5** — `openspec init` "deja lista la estructura base de OpenSpec sobre el proyecto. Es el punto de partida: sin esta estructura, las etapas siguientes no tienen dónde escribir". Apenas termina, aparece **una única pregunta**: ¿hacemos estudio de mercado antes de los primeros planos? **Sí → se ejecuta `discovery-research`**; No → se salta directo a `kb-creator`.

Complemento (`presentacion-video-sdd-openspec.pdf`, diap. 8-9): OpenSpec es un CLI, la única fuente de verdad del estado de los cambios, guardada en archivos versionables dentro de `openspec/`; `openspec init` genera esa estructura e instala las skills/comandos que el agente detecta automáticamente.

## 3. Qué se hizo en este proyecto

Se ejecutó `/active-orchestrator` sobre el repositorio vacío (el único commit previo era `Initial commit`). La corrida:

1. Corrió **`openspec init`**, que dejó la estructura base de OpenSpec y los harnesses/comandos del ciclo OPSX.
2. Respondió **Sí** en la bifurcación de Discovery (el Discovery es obligatorio en este trabajo), habilitando la etapa siguiente (`discovery-research`).

Todo esto quedó en el commit **`99769fa`** (`chore(funidad): funda el proyecto con OpenSpec y los harnesses OPSX`), que creó:

- `.active-orchestrator-state.json` — la **bitácora compartida** de la fundación.
- `openspec/config.yaml` + `openspec/specs/` + `openspec/changes/archive/` — la estructura base de OpenSpec.
- `.claude/commands/opsx/*` y `.opencode/commands/opsx-*` — los comandos del ciclo OPSX.
- `.claude/skills/openspec-*` y `.opencode/skills/openspec-*` — las skills del ciclo OPSX.

El archivo `openspec/config.yaml` confirma la inicialización (`schema: spec-driven`, idioma `es`).

## 4. Correspondencia con la teoría

| Punto de la teoría | En el proyecto | ✔ |
|---|---|---|
| `/active-orchestrator` corre sobre repo sin KB/roadmap/reglas | repo vacío salvo `Initial commit` | ✔ |
| Primera etapa: `openspec init` deja la estructura base | commit `99769fa`: `openspec/` + comandos/skills OPSX | ✔ |
| Bifurcación única: "¿hacemos estudio de mercado?" → Sí | se respondió Sí (state `discovery` poblado) | ✔ |
| Bitácora compartida `.active-orchestrator-state.json` | presente y versionada | ✔ |

No se detectaron desvíos respecto del marco teórico en esta etapa.

## 5. Protocolo de inspección aplicado

La etapa terminó con la estructura de OpenSpec y la bitácora listas, y la decisión de **Continuar** hacia Discovery (bifurcación respondida "Sí").

## 6. Entregables de la etapa

| Entregable | Ubicación | Estado |
|---|---|---|
| `.active-orchestrator-state.json` (etapa completada) | raíz | ✅ |
| Estructura base de OpenSpec | `openspec/` | ✅ |
| Comandos y skills OPSX instalados | `.claude/`, `.opencode/` | ✅ |
| Evidencia (commit, extractos) | `etapa 1/evidencia-etapa-1.md` | ✅ |
