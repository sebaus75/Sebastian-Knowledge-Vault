---
estado: Activo
fase: sistema-cerebro
created: 2026-08-19
updated: 2026-08-19
tags: [proyecto/activo, sistema, meta, vault, opencode]
---
# Mantenimiento y seguridad

> Proyecto meta-responsable del sistema cerebro: mantenimiento, optimización, mejora continua y seguridad de la vault de Obsidian + integración con OpenCode (protocolo, skills, hooks, backup).

**Estado vivo**: [[10 - Proyectos/Mantenimiento y seguridad/STATUS]] — fase, pendientes y próxima sesión.
**Carpeta de trabajo**: `Proyectos Open Code/Mantenimiento y seguridad/` (AGENTS.md propio + opencode.json).
**Piezas clave**: vault `AGENTS.md`, `CONTEXT.md`, `90 - Sistema/MANIFEST.md`, skill `vault-brain`.

---

## Map of Content

- [[10 - Proyectos/Mantenimiento y seguridad/STATUS|STATUS]] — estado operativo y plan por fases
- [[10 - Proyectos/Mantenimiento y seguridad/Decisiones Técnicas|Decisiones Técnicas]] — ADR del sistema cerebro (001-005)
- [[10 - Proyectos/Mantenimiento y seguridad/Plan - Areas de Mejora|Plan - Áreas de Mejora]] — P1 resuelto (2026-08-19); P2-P3 candidatas
- [[CONTEXT]] — estado global de la vault
- [[90 - Sistema/MANIFEST]] — enrutamiento proyecto → vault
- [[AGENTS]] — contrato y protocolo de la vault

---

## Sistemas de referencia

- `AGENTS.md` de la vault: contrato operativo para agentes.
- Skill `vault-brain` (fuente en vault `30 - Recursos/Skills/`, sync a config global): protocolo de memoria y tokens.
- MCP Obsidian Local REST API (v5.0.2) en `https://127.0.0.1:27124/mcp/`.
- Config global de OpenCode: `~/.config/opencode/` (skills, opencode.jsonc, plugins).

## Pendientes globales del proyecto

- [x] Respaldo automático operativo (2026-08-19): repo GitHub privado + push en cada cierre + tarea semanal `Vault Backup Semanal`. Copia local externa: pendiente (decisión del usuario).
- [ ] Mantener Inbox procesado y health-check periódico de la vault.