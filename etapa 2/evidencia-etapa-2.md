# Evidencia — Etapa 2 (Discovery / `discovery-research`)

Esta carpeta es evidencia de la ejecución de la **Etapa 2** del trabajo de integración.
La explicación de la etapa está en `explicacion-etapa-2.md`.

---

## 1. Artefactos generados

| Artefacto | Ruta | Tamaño |
|---|---|---|
| Relevamiento estructurado (11 puntos) | `discovery/discovery.md` | 261 líneas |
| Checklist de once puntos (misma carpeta que el informe) | `docs/discovery/checklist-discovery.md` | 268 líneas |
| Informe de Discovery (MD) | `docs/discovery/informe-discovery.md` | 658 líneas |
| Informe de Discovery (PDF) | `docs/discovery/informe-discovery.pdf` | 460 líneas |
| Verificación de fuentes | `discovery/verificacion-fuentes.md` | 146 líneas |
| Notas por competidor | `discovery/sources/*.md` | 19 archivos |

## 2. Commits asociados

| Commit | Fecha | Mensaje |
|---|---|---|
| `7890bf8` | 2026-10-03 | `docs(discovery): agrega el informe de Discovery y la base de conocimiento` |
| `dc3fd4e` | 2026-10-05 | `fix(discovery): corrige contradicción D.3/D.4 sobre lista de espera y sobreturnos` |
| `f4772ce` | 2026-10-05 | `fix(audit): registra hallazgos H-07..H-11 con fecha y protocolo Ajustar` |

Salida de `git show --stat 7890bf8` (extracto):

```
7890bf8 docs(discovery): agrega el informe de Discovery y la base de conocimiento
 discovery/discovery.md                      | 261 +++++++++++
 discovery/sources/benty.md                  |  14 +
 ... (19 notas de fuentes) ...
 discovery/verificacion-fuentes.md           | 146 +++++++
 docs/discovery/checklist-discovery.md       | 268 +++++++++++
 docs/discovery/informe-discovery.md         | 658 ++++++++++++++++++++++++++++
 docs/discovery/informe-discovery.pdf        | 460 +++++++++++++++++++
 ... (la base de conocimiento se agregó en el mismo commit) ...
 38 files changed, 3941 insertions(+)
```

## 3. Relevamiento estructurado — checklist de once puntos

`discovery/discovery.md` contiene exactamente los once puntos que pide la teoría
(`presentacion-02`, diap. 6):

```
## 1. Problema que resuelve
## 2. Usuarios / roles
## 3. Casos de uso
## 4. Competidores / soluciones existentes
## 5. Funcionalidades necesarias (MVP)
## 6. Funcionalidades opcionales (backlog post-lanzamiento)
## 7. Reglas de negocio
## 8. Integraciones
## 9. Restricciones
## 10. Riesgos
## 11. Preguntas abiertas
```

## 4. Informe de Discovery — estructura (secciones A–D + verificación)

`docs/discovery/informe-discovery.md`:

```
## Resumen ejecutivo
## A. Tabla comparativa de sistemas          (≥15 sistemas)
## B. Matriz de evaluación ponderada          (+ B.1 nota metodológica)
## C. Análisis competitivo                    (C.1..C.5)
## D. Recomendación final                     (D.1..D.8: demo, UX, MVP, precios, riesgos)
## E. Verificación de fuentes y afirmaciones no verificadas  (E.1..E.5)
## F. Referencias
## Anexo 1. Fichas por sistema                (19 fichas)
```

Alcance: **19 sistemas relevados**, todos con URL y fecha de consulta **2026-10-03**.

## 5. Verificación manual de fuentes (mínimo 5)

De `discovery/verificacion-fuentes.md`, tabla de registro:

| # | Fuente | URL abierta | Dato confirmado | Fecha |
|---|---|---|---|---|
| 1 | Órbita Gestión | Sí | Sí | 2026-10-03 |
| 2 | DentalFLOW | Sí | Sí | 2026-10-03 |
| 3 | Dentatools | Sí | Sí | 2026-10-03 |
| 4 | DentalSaaS | Sí | Sí | 2026-10-03 |
| 5 | TurnosUno | Sí | Sí | 2026-10-03 |

Estado del gate: **cerrado** (5 fuentes abiertas y verificadas por el autor el 2026-10-03).

## 6. Hallazgos registrados (protocolo Ajustar)

De `discovery/verificacion-fuentes.md` (H-01..H-06, más H-07..H-11 en el informe):

| ID | Qué se afirmó (falso/impreciso) | Estado |
|---|---|---|
| H-01 | La "agenda por sillón" era diferencial exclusivo | Corregido |
| H-02 | DentalSaaS no publica precios | Corregido |
| H-03 | DentalFLOW tenía recordatorios automáticos | Corregido |
| H-04 | Dentatools cubría obras sociales/prepagas | Corregido |
| H-05 | La matriz del Discovery cumplía la consigna | Corregido (recalculada a 7 criterios, escala 0–5) |
| H-06 | Órbita no publica precios y es el único con agenda por sillón | Corregido |

## 7. "No evidenciado" y afirmación comercial

El criterio aplicado (extracto de `verificacion-fuentes.md`):

> "Ninguna fuente citada proviene de un artículo agregador, un blog de comparación de software sin datos propios, ni de un perfil de red social. Todas son páginas del producto mismo. Cuando el producto no publica un dato (precio, cantidad de usuarios), se escribió «no declarado en el sitio» en vez de completar el dato con una estimación."

## 8. Trazabilidad con el estado del orquestador

`.active-orchestrator-state.json`, sección `discovery` (extracto):

```json
"discovery": {
    "created_by": "discovery-research",
    "fecha": "2026-10-03",
    "consultadas_en": "2026-10-03",
    "informe": "docs/discovery/informe-discovery.md",
    "verificacion_fuentes": "discovery/verificacion-fuentes.md",
    ...
    "fuentes_a_verificar_por_el_autor": {
        "estado": "verificadas",
        "verificadas_por": "Facundo Chacon",
        "fecha": "2026-10-03"
    },
    ...
    "nota_reconciliacion": "La consigna exige que el resultado estructurado de discovery-research (checklist de once puntos) quede en la MISMA carpeta que el informe. Por eso discovery/discovery.md se copio a docs/discovery/checklist-discovery.md ..."
}
```

## 9. Cómo reproducir esta evidencia

```powershell
# Desde la raíz del repositorio turnos-odontologia/
git show --stat 7890bf8
Get-ChildItem discovery -Recurse
Get-Content discovery\discovery.md
Get-Content discovery\verificacion-fuentes.md
Get-Content docs\discovery\informe-discovery.md
```
