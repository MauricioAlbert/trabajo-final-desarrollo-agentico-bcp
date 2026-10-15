# Trabajo final — Desarrollo Agéntico BCP

Proceso completo ejecutado con el arnés (Gentle AI + Engram), sin código escrito a mano.

| Carpeta | Contenido |
|---|---|
| `docs/historias/` | Historias de usuario y preguntas de ambigüedad sobre la especificación |
| `docs/adr/` | Decisiones de arquitectura (ADR) |
| `docs/arquitectura/` | Diagramas de arquitectura |
| `docs/specs/` | Especificaciones por módulo (incluye manejo de errores) |
| `docs/pruebas/` | Plan de pruebas de backend y frontend |
| `docs/bugs/` | Un archivo por bug encontrado por la IA, con su caso asociado |
| `docs/evidencia/` | Capturas y logs de consola de las pruebas |
| `backend/` | API en ASP.NET Core 8 con pruebas xUnit |
| `frontend/` | React + Vite + TypeScript con pruebas visuales (Playwright) |

## MCP de Playwright

Configurado con ámbito de proyecto en `.mcp.json`:

```json
{
  "mcpServers": {
    "playwright": {
      "type": "stdio",
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@playwright/mcp@0.0.83", "--browser", "msedge"]
    }
  }
}
```

- `cmd /c`: en Windows, `npx` necesita este envoltorio para arrancar como servidor MCP.
- `@playwright/mcp@0.0.83`: versión fija para resultados reproducibles.
- `--browser msedge`: usa Microsoft Edge del sistema, sin descargar navegadores. El navegador se abre visible (modo por defecto).

Requisitos: Node.js 18 o superior y Microsoft Edge. Al abrir el proyecto, Claude Code pide aprobar el servidor `playwright`; sus herramientas (`browser_*`) quedan disponibles tras aprobarlo y reiniciar la sesión.

### Skill de pruebas

`.claude/skills/testing-e2e/` usa este MCP para generar el plan en `docs/pruebas/`, ejecutarlo en el navegador y registrar cada bug en `docs/bugs/` con capturas y logs de consola en `docs/evidencia/`. Las rutas de evidencia son relativas a la raíz del repositorio.
