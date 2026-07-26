---
tags: [recurso/opencode, configuracion]
created: 2026-07-01
---
# OpenCode - Configuracion y Skills

Herramienta CLI para ingenieria de software asistida por IA.

## Configuracion
Archivo: `opencode.json`

Estructura:
```json
{
  "permission": { "*": "allow" },
  "mcp": {
    "stitch": {
      "type": "remote",
      "enabled": false
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
- Skills: Ninguno configurado aun
- Archivo: opencode.json con MCP Stitch deshabilitado

### Sentido Creativo
- Ubicacion: `Proyectos Open Code/Sentido Creativo`
- Contexto disponible en SentidoCreativo - Context.md

## Goal Plugin (@prevalentware/opencode-goal-plugin)

Plugin que ejecuta goals complejos de forma autonoma con multiples turnos.

### Configuracion global (~/.config/opencode/opencode.jsonc)
```json
{
  "plugins": {
    "goals": {
      "auto_continue": true,
      "max_auto_turns": 25,
      "max_execution_time_minutes": 60,
      "no_progress_pause": "Whats the status?"
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