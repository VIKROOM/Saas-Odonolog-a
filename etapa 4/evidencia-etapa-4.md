# Evidencia — Etapa 4 (Roadmap / `roadmap-generator`)

Esta carpeta es evidencia de la ejecución de la **Etapa 4** del trabajo de integración.
La explicación de la etapa está en `explicacion-etapa-4.md`.

---

## 1. Artefacto generado

- **Archivo:** `CHANGES.md`
- **Ubicación:** raíz del repositorio `turnos-odontologia/`
- **Tamaño en el commit de creación:** 233 líneas insertadas
- **Tamaño actual:** 249 líneas (creció por correcciones posteriores de auditoría)

## 2. Commits asociados (historial del repositorio)

| Commit | Fecha | Mensaje |
|---|---|---|
| `71dd6f1` | 2026-10-05 | `docs: agrega CHANGES.md con plan operativo (roadmap) e integra deuda Turno vs Bloqueo` |
| `456877e` | 2026-10-05 | `chore(state): confirma stack y marca listo para etapa 4 (CHANGES.md)` |

Salida de `git show --stat 71dd6f1`:

```
71dd6f1 docs: agrega CHANGES.md con plan operativo (roadmap) e integra deuda Turno vs Bloqueo
 CHANGES.md | 233 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 233 insertions(+)
```

## 3. Trazabilidad con el estado del orquestador

`.active-orchestrator-state.json` confirma el stack decidido y el avance de la fase,
consistente con lo reflejado en `CHANGES.md`:

```json
"system_info": {
    "system_type": "web_app",
    "domain": "salud / gestion de consultorios odontologos",
    "scale": "public_multi_user",
    "stack": "FastAPI 3.11 + PostgreSQL 15 + React 18 (Vite) + Docker Compose",
    "needs_infra": true,
    "stack_confianza": "alta (decision del equipo, registrada como DD-11)"
}
```

## 4. Contenido clave verificado en `CHANGES.md`

- **Total de changes:** 11 (`C-01` … `C-11`).
- **Fases:** 4.
- **Gates de paralelismo:** 6 (GATE 0 a GATE 5).
- **Camino crítico:** `C-01 → C-02 → C-03 → C-04 → C-05 → C-09 → C-10`.
- **Primer change recomendado:** `C-01` (`foundation-setup`).

### Árbol de dependencias (extracto textual)

```
C-01-foundation-setup
│
├── C-02-core-models-schema
│   ├── C-03-auth-users-roles
│   │   └── C-04-pacientes-turnos-core
│   │       ├── C-05-disponibilidad-bloqueos
│   │       └── C-06-historia-clinica-odontograma
│   └── C-07-ui-base-frontend
│       └── C-08-agenda-ui-reserva
│
└── C-09-tests-integracion-solapamientos
    └── C-10-seed-datos-iniciales
```

### Declaración de alineación con el MVP (extracto textual)

> *"Los changes de este roadmap derivan del MVP imprescindible definido en la sección D.3 del informe de Discovery (`docs/discovery/informe-discovery.md`). Cada change se alinea con ese alcance."*

## 5. Cómo reproducir esta evidencia

```powershell
# Desde la raíz del repositorio turnos-odontologia/
git log --oneline -30
git show --stat 71dd6f1
git show --stat 456877e
Get-Content CHANGES.md
Get-Content .active-orchestrator-state.json
```
