# Evidencia — Etapa 3 (Base de conocimiento / `kb-creator`)

Esta carpeta es evidencia de la ejecución de la **Etapa 3** del trabajo de integración.
La explicación de la etapa está en `explicacion-etapa-3.md`.

---

## 1. Artefactos generados

Carpeta `knowledge-base/` con los **10 archivos canónicos** + `README.md`:

```
knowledge-base/
├── 01_vision_y_objetivos.md
├── 02_descripcion_general.md
├── 03_actores_y_roles.md
├── 04_modelo_de_datos.md
├── 05_reglas_de_negocio.md
├── 06_funcionalidades.md
├── 07_flujos_principales.md
├── 08_arquitectura_propuesta.md
├── 09_decisiones_y_supuestos.md
├── 10_preguntas_abiertas.md
└── README.md
```

## 2. Modo de ejecución (silencioso / ingest)

`knowledge-base/README.md` (extracto textual):

> "Base de conocimiento generada a partir de los documentos de Discovery del proyecto (`docs/discovery/` y `.active-orchestrator-state.json`). Generada con la skill `kb-creator` en **Modo A (silencioso)**, a partir de documentos existentes. `source: "ingest"`."

## 3. Commits asociados

| Commit | Fecha | Mensaje |
|---|---|---|
| `7890bf8` | 2026-10-03 | `docs(discovery): agrega el informe de Discovery y la base de conocimiento` |
| `caf878e` | 2026-10-05 | `fix(kb): corrige ortografía, enlaces y deuda de diseño` |
| `80fb3d4` | 2026-10-05 | `fix(kb): corrige las cifras de competencia` |
| `503cfb9` | 2026-10-05 | `fix(kb): marca IN-01/02/03 como resueltas (H-09)` |

Salida de `git show --stat 80fb3d4`:

```
80fb3d4 fix(kb): corrige las cifras de competencia
 knowledge-base/01_vision_y_objetivos.md     |  8 ++++++--
 knowledge-base/02_descripcion_general.md    | 23 ++++++++++++++++++---
 knowledge-base/09_decisiones_y_supuestos.md | 14 +++++++++++---
 3 files changed, 37 insertions(+), 8 deletions(-)
```

## 4. Trazabilidad con el estado del orquestador

`.active-orchestrator-state.json`, sección `kb` (extracto):

```json
"kb": {
    "created_by": "kb-creator",
    "source": "ingest",
    "discovery": { ... },
    "files": [
        "knowledge-base/01_vision_y_objetivos.md",
        "knowledge-base/02_descripcion_general.md",
        "knowledge-base/03_actores_y_roles.md",
        "knowledge-base/04_modelo_de_datos.md",
        "knowledge-base/05_reglas_de_negocio.md",
        "knowledge-base/06_funcionalidades.md",
        "knowledge-base/07_flujos_principales.md",
        "knowledge-base/08_arquitectura_propuesta.md",
        "knowledge-base/09_decisiones_y_supuestos.md",
        "knowledge-base/10_preguntas_abiertas.md",
        "knowledge-base/README.md"
    ]
}
```

## 5. Revisión obligatoria — verificaciones de correspondencia

### 5.1 Reglas de negocio de agenda presentes
`knowledge-base/05_reglas_de_negocio.md` contiene el dominio de agenda (códigos RN-AGE):
duración por práctica, sillón/box como recurso y prevención de solapamientos.
(Referenciados luego por el roadmap: `CHANGES.md` cita `RN-AGE-01..RN-AGE-05`, `RN-AGE-03`, `RN-AGE-05`.)

### 5.2 "Preguntas abiertas" contiene los "No evidenciado"
`knowledge-base/README.md`:

> "Los diez puntos que el relevamiento no pudo responder están en `10_preguntas_abiertas.md`, y se repiten como supuestos o como 'No evidenciado' en los archivos que los usan. **Ninguno se rellenó con una estimación.**"

### 5.3 Advertencia de honestidad (KB vs Discovery)
`knowledge-base/README.md`:

> "El stack tecnológico **está decidido** (FastAPI + PostgreSQL + React + Docker, DD-11), pero esa decisión la tomó el equipo el 2026-10-03: **Discovery no eligió tecnologías**, porque la consigna las deja libres. Conviene tener presente la diferencia, porque una decisión nuestra no es un hallazgo de la investigación."

### 5.4 Contenido por archivo (según el índice del README)

| Archivo | Resumen |
|---|---|
| `01_vision_y_objetivos.md` | Propósito, objetivos por actor, alcance v1, fuera de alcance, métricas |
| `02_descripcion_general.md` | Stack decidido, arquitectura, integraciones, API REST |
| `03_actores_y_roles.md` | Actores, matriz RBAC, rutas públicas y privadas |
| `04_modelo_de_datos.md` | 5 dominios, ERD, 11 entidades, seed, restricción de exclusión |
| `05_reglas_de_negocio.md` | 4 dominios de reglas con códigos RN, más excepciones globales |
| `06_funcionalidades.md` | 7 épicas, 18 historias de usuario con criterios de aceptación |
| `07_flujos_principales.md` | 8 flujos extremo a extremo (incluye intento de doble reserva) |
| `08_arquitectura_propuesta.md` | Patrones, estructura de directorios, seguridad, env vars |
| `09_decisiones_y_supuestos.md` | 8 decisiones documentadas y 8 supuestos con su riesgo |
| `10_preguntas_abiertas.md` | 4 inconsistencias, 10 puntos no evidenciados, 12 preguntas |

## 6. Cómo reproducir esta evidencia

```powershell
# Desde la raíz del repositorio turnos-odontologia/
git show --stat 7890bf8
git show --stat caf878e
git show --stat 80fb3d4
git show --stat 503cfb9
Get-ChildItem knowledge-base
Get-Content knowledge-base\README.md
```
