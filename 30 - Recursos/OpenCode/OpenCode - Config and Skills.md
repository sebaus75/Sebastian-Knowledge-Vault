---
tags: [recurso/opencode, configuracion]
created: 2026-07-01
---
# OpenCode - Configuracion y Skills

Herramienta CLI para ingenieria de software asistida por IA.

## Configuracion
Archivo global: `~/.config/opencode/opencode.jsonc` (la vault activa el MCP de Obsidian desde el AGENTS.md global).

Estructura real (2026-08-19):
```jsonc
{
  "plugin": [
    ["@prevalentware/opencode-goal-plugin", { "auto_continue": true, "max_auto_turns": 25, "default_token_budget": 200000 }]
  ],
  "mcp": {
    "obsidian": {
      "type": "remote",
      "url": "https://127.0.0.1:27124/mcp/",
      "enabled": true,
      "apiKey": "<key del plugin Obsidian Local REST API>"
    }
  }
}
```

## Skills Disponibles
- customize-opencode - Configuracion de OpenCode
- (otros segun contexto)

## Proyectos Configurados
### TemplateTest
- Ubicacion: `Proyectos Open Code/TemplateTest/`
- Stack: HTML5 + Tailwind CDN + Vanilla JS + GAS + Sheets + Vercel
- Generado via: `/goal` plugin (@prevalentware/opencode-goal-plugin)
- File count: 27 archivos (~31 KB codigo JS)
- Estado: Desarrollo completado, listo para empaquetar como producto $30k+

### Isaac Torres
- Ubicacion: `Proyectos Open Code/IsaacTorres`
- Skills: `wolf-barber-booking` (skill propia, fuente en vault `30 - Recursos/Skills/`)
- Archivo: opencode.json con MCP Stitch deshabilitado

### Otros proyectos configurados (2026-08-19)
- **SupleHuges** — `Proyectos Open Code/SupleHuges/` — migración Shopify → Supabase + Vercel (F0 commiteada).
- **El Legado** — `Proyectos Open Code/El Legado/` — landing estática (HTML único).
- **Proyectos CAD** — `Proyectos Open Code/Proyectos CAD/` — pipeline Python/ezdxf (DXF → PDF).
- **Sentido Creativo** — `Proyectos Open Code/Sentido Creativo/` — asesoría IA (contexto en `SentidoCreativo - Context.md`).
- **Mantenimiento y seguridad** — `Proyectos Open Code/Mantenimiento y seguridad/` — sistema cerebro (opencode.json con MCP obsidian + AGENTS.md propio).

## Goal Plugin (@prevalentware/opencode-goal-plugin)

Plugin que ejecuta goals complejos de forma autonoma con multiples turnos.

### Configuracion global real (~/.config/opencode/opencode.jsonc, 2026-08-19)
```json
{
  "plugin": [
    [
      "@prevalentware/opencode-goal-plugin",
      {
        "auto_continue": true,
        "max_auto_turns": 25,
        "defer_while_tasks_active": true,
        "default_token_budget": 200000,
        "max_goal_duration_seconds": 3600,
        "no_progress_token_threshold": 50,
        "max_no_progress_turns": 3,
        "restricted_agents": ["plan"],
        "allow_goal_execution_from_plan": false
      }
    ]
  ],
  "mcp": {
    "obsidian": {
      "type": "remote",
      "url": "https://127.0.0.1:27124/mcp/",
      "enabled": true,
      "apiKey": "933565a1fb... (vault: .obsidian/plugins/*/data.json)"
    }
  }
}
```

### Agentes personalizados
| Archivo | Proposito |
|---|---|
| `~/.config/opencode/agents/goal-orch.md` | Orquestador: analiza, divide en fases, delega a goal-worker, verifica checklist |
| `~/.config/opencode/agents/goal-worker.md` | Worker: implementa tareas individuales con modelo deepseek-v4-flash-free |
| `~/.config/opencode/commands/goal-orch.md` | Comando `/goal-orch` — version manual del orquestador |

### Uso
```
/goal <instruccion completa del objetivo>
```
El plugin ejecuta hasta 25 turnos autonomos, con pausa si no hay progreso.

## Mejores Practicas
- Configurar skills para estandarizar prompts
- Usar AGENTS.md para instrucciones de contexto
- .opencode/ para configuracion local
- Permission rules para seguridad
- Prompts de goal deben incluir: stack, directorio, archivos a modificar, checklist de verificacion
- Separar goals grandes en rondas (R1 base, R2 mejoras, R3 bugfixes, etc.)