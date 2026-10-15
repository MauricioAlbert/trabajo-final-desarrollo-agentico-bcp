# Plan de pruebas — <nombre del sistema>

- **Versión / commit probado:** <hash>
- **Fecha:** AAAA-MM-DD
- **Alcance:** <módulos / pantallas / endpoints>
- **Fuera de alcance:** <qué no se prueba y por qué>
- **Entorno:** backend `<url>`, frontend `<url>`, navegador Microsoft Edge (Playwright MCP, visible)

## Estrategia

| Nivel | Herramienta | Qué cubre |
|---|---|---|
| Unitario | xUnit (`backend/`) | Reglas de dominio |
| E2E / visual | Playwright MCP | Flujos de usuario y mensajes de error |

## Casos de prueba

| ID | Spec / Historia | Tipo | Precondición | Pasos | Resultado esperado |
|---|---|---|---|---|---|
| CP-001 | S1 / HU-01 | Positivo | ... | 1. ... 2. ... | ... |
| CP-002 | S-ERR-1 | Manejo de errores | ... | ... | Mensaje "<texto exacto de la spec>" |

## Resultados de ejecución

| ID | Resultado | Bug | Evidencia |
|---|---|---|---|
| CP-001 | Pasó | — | `docs/evidencia/CP-001.png` |
| CP-002 | Falló | BUG-001 | `docs/evidencia/BUG-001-1.png` |

## Resumen

Ejecutados: N · Pasaron: N · Fallaron: N · Bloqueados: N
