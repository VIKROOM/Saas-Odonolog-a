# Etapa 2 — Discovery: investigación de mercado (`discovery-research`)

> Documento explicativo de la Etapa 2 del trabajo de integración (SDD + Active Stack).
> Evidencia asociada: ver `evidencia-etapa-2.md` en esta misma carpeta.

## 1. Qué pide la consigna

> **Etapa 2. Discovery: investigación de mercado**
> Es el corazón del trabajo y la etapa donde más tiempo conviene invertir. Se ejecuta con la skill `discovery-research`, que responde un checklist de once puntos: problema, usuarios, casos de uso, competidores, funcionalidades necesarias, funcionalidades opcionales, reglas de negocio, integraciones, restricciones, riesgos y preguntas abiertas. Si le pasan URLs de competidores, la skill puede delegar en `web-scraper` para investigarlas antes de preguntarles.
> Además de esa ronda de preguntas, deben encargarle a su agente la siguiente investigación [consigna larga de analista de mercado: tabla de ≥15 sistemas, matriz ponderada, análisis competitivo, recomendación final].
> **Entregable de la etapa**: el informe de Discovery (`docs/discovery/informe-discovery.md` y su versión en PDF) con las secciones A, B, C y D, más la sección final "Verificación de fuentes". El resultado estructurado de `discovery-research` (checklist de once puntos) se guarda en la misma carpeta.
> Guardar el informe dentro del repositorio es importante: es el insumo que la etapa siguiente va a leer.

Puntos de verificación exigidos:
- Abrir y comprobar **personalmente al menos 5 fuentes** citadas (una de cada tipo) y anotar si lo afirmado está realmente en esa URL.
- Toda celda sin respaldo público debe decir **"No evidenciado"**, no quedar vacía ni completarse por deducción.
- Si aparece una afirmación falsa o no respaldada, **corregirla con Ajustar y registrar el hallazgo**.

## 2. Qué dice el marco teórico

`presentacion-02-flujo-de-trabajo.pdf`:

- **Diap. 6** — Discovery es la etapa opcional de la fundación. "Convierte 'tengo una idea' en 'sé qué voy a construir y por qué' — antes de comprometer ninguna decisión de arquitectura." Responde el **checklist de 11 puntos** (problema, usuarios, casos de uso, competidores, funcionalidades necesarias, funcionalidades opcionales, reglas de negocio, integraciones, restricciones, riesgos, preguntas abiertas). "Si hay URLs de competidores, `discovery-research` subcontrata a `web-scraper` para investigarlas antes de la ronda de preguntas". "El resultado es un relevamiento estructurado que alimenta directamente a `kb-creator` en la etapa siguiente."

`presentacion-video-sdd-openspec.pdf` (diap. 4): el principio troncal — *"un agente no deja huecos sin resolver: los rellena"* — es la razón por la cual el Discovery exige distinguir dato comprobado de dato inventado.

## 3. Qué se hizo en este proyecto

Se ejecutó `discovery-research`, que produjo el **relevamiento estructurado de once puntos** y, a partir de las URLs de competidores, delegó en `web-scraper` (notas por fuente en `discovery/sources/`). Luego se encargó al agente la investigación de mercado según la consigna larga, que produjo el **informe** con las secciones A–D.

Artefactos generados:

| Artefacto | Ubicación | Qué contiene |
|---|---|---|
| Relevamiento estructurado (11 puntos) | `discovery/discovery.md` | Checklist de once puntos (versión original) |
| Checklist en la misma carpeta que el informe | `docs/discovery/checklist-discovery.md` | Copia del relevamiento, con la matriz inválida conservada como registro del error |
| Informe de Discovery (MD) | `docs/discovery/informe-discovery.md` | Secciones A, B, C, D, E (verificación), F (referencias) + Anexo 1 (fichas por sistema) |
| Informe de Discovery (PDF) | `docs/discovery/informe-discovery.pdf` | Versión PDF del informe |
| Verificación de fuentes | `discovery/verificacion-fuentes.md` | Control de trazabilidad de 19 fuentes + hallazgos H-01..H-06 |
| Notas por competidor | `discovery/sources/*.md` | 19 fichas (una por sistema relevado) |

**Alcance del relevamiento:** 19 sistemas del mercado argentino, todos con URL y fecha de consulta (2026-10-03).

**Verificación manual de fuentes:** las 5 fuentes críticas (Órbita, DentalFLOW, Dentatools, DentalSaaS, TurnosUno) fueron abiertas y confirmadas por el autor (Facundo Chacón) el 2026-10-03.

**Hallazgos registrados (protocolo Ajustar):** H-01 a H-06 en la primera pasada (p. ej. H-01: se afirmó que la "agenda por sillón" era diferencial exclusivo → falso; H-05: la matriz inicial tenía 6 criterios en escala 1–5 → se recalculó con los 7 criterios oficiales en escala 0–5). El uso de **Ajustar** y el registro del hallazgo son exactamente lo que pide la consigna.

## 4. Correspondencia con la teoría

| Punto de la teoría / consigna | En el proyecto | ✔ |
|---|---|---|
| Checklist de 11 puntos | `discovery/discovery.md` (los 11) | ✔ |
| Delegación a `web-scraper` si hay URLs | 19 notas en `discovery/sources/` | ✔ |
| Resultado estructurado alimenta `kb-creator` | el informe + checklist son insumo de la Etapa 3 | ✔ |
| Informe con secciones A–D + "Verificación de fuentes" | `informe-discovery.md`: A, B, C, D + E (verificación) | ✔ |
| Checklist de once puntos en la MISMA carpeta que el informe | `docs/discovery/checklist-discovery.md` | ✔ |
| ≥5 fuentes verificadas personalmente | 5 fuentes verificadas por el autor (2026-10-03) | ✔ |
| "No evidenciado" en celdas sin respaldo | usado en informe y checklist | ✔ |
| Hallazgo registrado al corregir con Ajustar | H-01..H-06 + H-07..H-11 | ✔ |

### Nota de reconciliación (trazabilidad)
La consigna exige que el resultado estructurado de `discovery-research` quede en la **misma carpeta** que el informe. Por eso `discovery/discovery.md` se copió a `docs/discovery/checklist-discovery.md`; el original se conserva en `discovery/` como registro del error (matriz con pesos inventados). El propio state lo documenta en `nota_reconciliacion`.

## 5. Protocolo de inspección aplicado

Durante el cierre de la etapa se usó **Ajustar** para corregir afirmaciones no respaldadas (H-01..H-06), dejando el hallazgo registrado. El gate de verificación de fuentes quedó **cerrado**. No se detectaron desvíos respecto del marco teórico.

## 6. Entregables de la etapa

| Entregable | Ubicación | Estado |
|---|---|---|
| Informe de Discovery (MD + PDF) | `docs/discovery/` | ✅ |
| Checklist de once puntos (misma carpeta) | `docs/discovery/checklist-discovery.md` | ✅ |
| Verificación de fuentes + hallazgos | `discovery/verificacion-fuentes.md` | ✅ |
| Notas por competidor (19) | `discovery/sources/` | ✅ |
| Evidencia (commits, extractos) | `etapa 2/evidencia-etapa-2.md` | ✅ |
