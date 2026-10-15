# Evidencia — Etapa 5 (Skills y reglas: `find-skill`, `skill-registry`, `agent-instruction`)

Esta carpeta es evidencia de la ejecución de la **Etapa 5** del trabajo de integración.
La explicación de la etapa está en `explicacion-etapa-5.md`.

---

## 1. Artefactos generados

| Artefacto | Ruta | Líneas |
|---|---|---|
| Registro de skills | `.atl/skill-registry.md` | 140 |
| Reglas del agente | `AGENTS.md` | 44 |
| Reglas del agente (copia) | `CLAUDE.md` | 44 (idéntico a `AGENTS.md`) |

## 2. Commits asociados (historial del repositorio)

| Commit | Fecha | Mensaje |
|---|---|---|
| `ac09d1b` | 2026-10-05 | `docs: agrega AGENTS.md/CLAUDE.md y actualiza skill-registry (etapa 5)` |
| `a1a2e6b` | 2026-10-05 | `chore(state): actualiza state tras generar artefactos etapa 5` |

Salida de `git show --stat ac09d1b`:

```
ac09d1b docs: agrega AGENTS.md/CLAUDE.md y actualiza skill-registry (etapa 5)
 .atl/skill-registry.md | 140 +++++++++++++++++++++++++++++++++++++++++++++++++
 AGENTS.md              |  44 ++++++++++++++++++++++++
 CLAUDE.md              |  44 ++++++++++++++++++++++++
 3 files changed, 228 insertions(+)
```

## 3. Trazabilidad con el estado del orquestador

`.active-orchestrator-state.json` registra la creación del registro:

```json
"registry": {
    "created_by": "skill-registry",
    "file": ".atl/skill-registry.md",
    "skills_indexed": 7,
    "engram": "not available"
}
```

Además, el `step` general quedó cerrado tras la etapa:

```json
"step": "done",
"owner": "active-orchestrator"
```

## 4. Contenido clave verificado

### 4.1 `.atl/skill-registry.md` — skills indexadas (7)

| Trigger (resumen) | Skill | Path |
|---|---|---|
| `/active-orchestrator:*` / fundar proyecto desde cero | active-orchestrator | `...\active-orchestrator\SKILL.md` |
| crear/actualizar AGENTS.md o CLAUDE.md | agents-md-generator | `...\agent-instruction\SKILL.md` |
| verificar criterios antes de "terminado" | criterios-aceptacion-check | `...\criterios-aceptacion-check\SKILL.md` |
| "find a skill for X" | find-skills | `...\find-skill\SKILL.md` |
| "crear base de conocimiento" | kb-creator | `...\kb-creator\SKILL.md` |
| "armar CHANGES / roadmap" | roadmap-generator | `...\roadmap-generator\SKILL.md` |
| crear/editar/optimizar skills | skill-creator | `...\skill-creator\SKILL.md` |

El registro también contiene bloques de **Compact Rules** por skill y una sección
**Excluded** para las skills de flujo OpenSpec (`openspec-propose`, `openspec-apply-change`,
`openspec-update-change`, `openspec-sync-specs`, `openspec-archive-change`, `openspec-explore`).

### 4.2 `AGENTS.md` / `CLAUDE.md` — reglas duras (extracto textual)

```
### Integridad de datos (PostgreSQL 15 / DD-05, DD-10, DD-11)
- NUNCA resolver el solapamiento de turnos en el backend → dejá la garantía a `EXCLUDE USING gist` + `btree_gist`; el motor de disponibilidad es UX, no integridad.
- NUNCA testear solapamiento contra SQLite o un doble en memoria → PostgreSQL real en Docker.
- NUNCA cambiar la base de datos → sin `EXCLUDE USING gist` no hay DD-05.

### Seguridad / Privacidad (RN-AU-02, RN-PRIV-*)
- NUNCA guardar el JWT en `localStorage` → cookie `httpOnly` + `SameSite` + validación de `Origin`/CSRF en escrituras (DD-09).
- NUNCA generar `token_público` con `uuid4()`/`random()` → fuente criptográfica, ≥128 bits medidos.
- NUNCA enviar historial clínico al asistente IA → solo disponibilidad (DD-07).
```

## 5. Hallazgo: `find-skill` sin evidencia persistida

La consigna pide justificar por escrito las recomendaciones de `find-skill`.
Verificación de que **no** quedó artefacto:

- `.active-orchestrator-state.json` → secciones presentes: `discovery`, `kb`, `registry`. **No** existe sección `find-skill` ni `skills`.
- Búsqueda en el repo de `find-skill` / `npx skills`: solo aparece la **definición** de la skill dentro de `.atl/skill-registry.md` (líneas 18 y 68-75), no una salida de recomendaciones.

Búsqueda ejecutada:

```powershell
# No produce un archivo de recomendaciones de la etapa:
Select-String -Path (Get-ChildItem -Recurse -File -Exclude *.lock) -Pattern "find-skill|npx skills"
```

Conclusión: la Etapa 5 está completa en `skill-registry` y `agent-instruction`,
pero la justificación de `find-skill` es el único punto sin respaldo versionado.

## 6. Cómo reproducir esta evidencia

```powershell
# Desde la raíz del repositorio turnos-odontologia/
git log --oneline -30
git show --stat ac09d1b
git show --stat a1a2e6b
Get-Content .atl/skill-registry.md
Get-Content AGENTS.md
Get-Content CLAUDE.md
Get-Content .active-orchestrator-state.json
```
