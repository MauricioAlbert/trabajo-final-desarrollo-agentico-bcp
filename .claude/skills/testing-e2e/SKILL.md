---
name: testing-e2e
description: "Trigger: plan de pruebas, probar la app, pruebas e2e, Playwright, buscar bugs, QA. Genera el plan desde specs y código, lo ejecuta en navegador visible y registra bugs con evidencia."
license: Apache-2.0
metadata:
  author: "mauricio"
  version: "1.0"
---

## Activation Contract

Usar al generar o ejecutar el plan de pruebas, o al buscar y documentar bugs de la aplicación (backend + frontend).

## Hard Rules

- Leer `docs/specs/` y `docs/historias/` y el código real (`backend/`, `frontend/`) ANTES de escribir un caso. Cada caso cita su spec (`S#`/archivo) o historia.
- Ejecutar con el MCP `playwright` (Edge visible; nunca `--headless`). Si sus herramientas `browser_*` no están disponibles, detenerse y pedir reiniciar la sesión.
- Rutas de evidencia relativas a la raíz del repo: `docs/evidencia/...`. No dejar archivos en otras carpetas.
- Un bug = un archivo `docs/bugs/BUG-NNN-<slug>.md` con caso asociado, pasos reproducibles, esperado vs. obtenido y enlaces a su evidencia.
- Reproducir cada bug dos veces antes de registrarlo. Fallo del entorno (API caída, puerto ocupado) NO es bug: se reporta como bloqueo.
- No corregir código: esta skill solo prueba y documenta.
- Textos en español.

## Decision Gates

| Situación | Acción |
|---|---|
| No existe `docs/pruebas/plan-pruebas.md` | Generarlo con `assets/plan-pruebas.md` |
| Plan existe y specs cambiaron | Actualizar solo los casos afectados |
| Resultado ≠ esperado y reproducible | Registrar bug |
| Caso no ejecutable por UI (solo API) | Ejecutarlo con `browser_navigate`/`fetch` en consola o marcarlo "cubierto por xUnit" |

## Execution Steps

1. Leer specs, historias y código; listar endpoints, pantallas y reglas de error.
2. Escribir/actualizar `docs/pruebas/plan-pruebas.md` (casos `CP-NNN`: positivos, negativos, bordes, manejo de errores).
3. Verificar que backend y frontend estén levantados (URLs del README o `launchSettings.json`/`vite.config.ts`).
4. Por cada caso: `browser_navigate` → `browser_snapshot` → interactuar (`browser_click`, `browser_type`, `browser_fill_form`) → comparar con lo esperado.
5. Al terminar cada caso: `browser_take_screenshot` con `filename: "docs/evidencia/CP-NNN.png"`; `browser_console_messages` y guardar su texto en `docs/evidencia/CP-NNN-consola.log`; para fallos de red, `browser_network_requests` en el mismo log.
6. Si falla: crear el bug con `assets/bug.md`, evidencia nombrada `BUG-NNN-*.png/.log`.
7. Actualizar la tabla de resultados del plan (Pasó / Falló → BUG-NNN / Bloqueado).
8. `browser_close` y guardar un resumen en Engram.

## Output Contract

Devolver: casos ejecutados, pasados, fallidos, bloqueados; lista de bugs (`ID — título — severidad — archivo`); bloqueos del entorno.

## References

- `assets/plan-pruebas.md` — plantilla del plan.
- `assets/bug.md` — plantilla de bug.
