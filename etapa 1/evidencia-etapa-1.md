# Evidencia — Etapa 1 (Iniciar la fundación / `openspec init`)

Esta carpeta es evidencia de la ejecución de la **Etapa 1** del trabajo de integración.
La explicación de la etapa está en `explicacion-etapa-1.md`.

---

## 1. Punto de partida

El repositorio estaba vacío: el único commit previo a la fundación era `Initial commit`
(`6c6fb82`, 2026-10-02). Condición que el marco teórico pide para `/active-orchestrator`
("un proyecto que todavía no tiene ni knowledge-base, ni roadmap, ni reglas").

```powershell
git log --reverse --oneline | Select-Object -First 2
# 6c6fb82 Initial commit
# 99769fa chore(funidad): funda el proyecto con OpenSpec y los harnesses OPSX
```

## 2. Commit de la etapa

| Commit | Fecha | Mensaje |
|---|---|---|
| `99769fa` | 2026-10-03 | `chore(funidad): funda el proyecto con OpenSpec y los harnesses OPSX` |

Salida de `git show --stat 99769fa` (extracto):

```
99769fa chore(funidad): funda el proyecto con OpenSpec y los harnesses OPSX
 .active-orchestrator-state.json                   | 317 +++++++++++++++++++
 .claude/commands/opsx/apply.md                    | 201 ++++++++++++
 .claude/commands/opsx/archive.md                  | 264 ++++++++++++
 .claude/commands/opsx/explore.md                  | 239 ++++++++++++
 .claude/commands/opsx/propose.md                  | 170 ++++++++++++
 .claude/commands/opsx/sync.md                     | 286 ++++++++++++
 .claude/commands/opsx/update.md                   | 105 ++++++++++++
 .claude/skills/openspec-apply-change/SKILL.md     | 205 +++++++++++++
 .claude/skills/openspec-archive-change/SKILL.md   | 221 +++++++++++++
 .claude/skills/openspec-explore/SKILL.md          | 354 ++++++++++++++++
 .claude/skills/openspec-propose/SKILL.md          | 174 ++++++++++++
 .claude/skills/openspec-sync-specs/SKILL.md       | 290 +++++++++++++++
 .claude/skills/openspec-update-change/SKILL.md    | 109 +++++++++
 .opencode/commands/opsx-apply.md                  | 198 ++++++++++++
 ... (equivalentes en .opencode/) ...
 openspec/changes/archive/.gitkeep                 |   0
 openspec/config.yaml                              |  28 ++
 openspec/specs/.gitkeep                           |   0
 28 files changed, 5563 insertions(+)
```

## 3. Estructura base de OpenSpec (resultado de `openspec init`)

```
openspec/
├── config.yaml
├── specs/                     (vacío al init; .gitkeep)
└── changes/
    └── archive/               (vacío al init; .gitkeep)
```

Contenido de `openspec/config.yaml` (extracto):

```yaml
schema: spec-driven

context: |
  Language: es
  All artifacts must be written in es.
  Keep OpenSpec structural headings and SHALL/MUST keywords in English.
```

## 4. Bitácora compartida

Archivo central: `.active-orchestrator-state.json`. Cabecera del archivo:

```json
{
    "version": 4,
    "step": "done",
    "owner": "active-orchestrator",
    ...
}
```

Contiene las secciones de cada skill de la fundación (`discovery`, `kb`, `registry`),
consistente con el modelo de **lectura compartida, escritura aislada** de la teoría
(`presentacion-02`, diap. 14).

## 5. Bifurcación de Discovery respondida "Sí"

La sección `discovery` del state quedó poblada (evidencia de que la bifurcación se
respondió "Sí" y se ejecutó `discovery-research`):

```json
"discovery": {
    "created_by": "discovery-research",
    "fecha": "2026-10-03",
    "consultadas_en": "2026-10-03",
    "informe": "docs/discovery/informe-discovery.md",
    ...
}
```

## 6. Cómo reproducir esta evidencia

```powershell
# Desde la raíz del repositorio turnos-odontologia/
git log --reverse --oneline
git show --stat 99769fa
Get-ChildItem openspec -Recurse
Get-Content openspec/config.yaml
Get-Content .active-orchestrator-state.json
```
