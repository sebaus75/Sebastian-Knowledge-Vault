---
created: 2026-08-19
updated: 2026-08-19
tags: [proyecto, plan, mejoras, pendiente]
---

# Plan — Áreas de Mejora del sistema cerebro

Plan de mejora continua detectado al cierre del plan principal (Fases 1-5, 2026-08-19). **P1 completo (01/02/03) RESUELTO el 2026-08-19**. Resto sin implementar: cada área es candidata a sesión propia. Prioridad restante: P2 (medio), P3 (bajo).

## P1-01 — Validar el acceso MCP real ✅ RESUELTO 2026-08-19

- Cert en store de Windows + `NODE_EXTRA_CA_CERTS` + API key en `opencode.jsonc` ya estaban; faltaba reiniciar opencode.
- Tras reiniciar: tools `obsidian_*` cargados y probados (`vault_list` raíz, `vault_read` dirigido, `tag_list`).
- Decisión: **MCP primario; fallback filesystem documentado** (AGENTS.md de la vault, skill `vault-brain`).

## P1-02 — Backup remoto (GitHub) ✅ RESUELTO 2026-08-19

- creado `https://github.com/sebaus75/Sebastian-Knowledge-Vault` (privado, push hecho).
- Push automático en cada cierre verificado (hook ahora usa `-Push`; prueba manual: commit `20:08` + "Everything up-to-date").
- Respaldo semanal agendado: tarea Task Scheduler `Vault Backup Semanal` (dom 09:00, `backup-vault.ps1 -Push`).

## P1-03 — Métricas de tokens por sesión ✅ RESUELTO 2026-08-19

- Plugin `vault-brain-lifecycle` (session.deleted): consulta mensajes de la sesión (`client.session.messages`, SDK `@opencode-ai/sdk`) y suma `cost`/`input`/`output` de parts `step-finish`; appenda `- [tokens ...]` al Registro del día.
- Verificado contra sesión real: in 243k / out 20.7k / modelo `deepseek-v4-flash-free`. Nota: el evento `session.deleted` no trae tokens; hay que sumarlos por mensaje.

## P2-01 — Modelo por tipo de tarea

- **Detalle**: opcional mencionado en el plan (Fase 4): modelo barato para mantenimiento, caro para diseño.
- **Mejora**: doc en el MANIFEST (columna "modelo sugerido") + config `opencode.json` por proyecto cuando aplique; evaluar si el ahorro real justifica la complejidad.

## P2-02 — Exponer `vault-health` como comando TUI

- **Detalle**: la skill existe pero exige que el agente la cargue.
- **Mejora**: comando `/vault-health` en `~/.config/opencode/commands/` que invoca la skill y muestra el reporte en TUI; útil para inspección manual sin conversar.
- **Verificación**: `/vault-health` responde checklist en cualquier directorio.

## P2-03 — Automatizar renovación del certificado/API key del plugin REST API

- **Detalle**: al reiniciar Obsidian el plugin puede regenerar cert y API key → MCP degrada a filesystem silenciosamente.
- **Mejora**: script `mcp-health.ps1` que verifica el MCP (GET /mcp/ con token) y avisa/actualiza config en `session.created`; o configurar token estático en el plugin.
- **Verificación**: 0 sesiones degradadas por cert en 2 semanas.

## P3-01 — Actualización semestral de skills de terceros

- **Detalle**: las 24 skills de terceros no se auditan (las propias sí, vía INDICE).
- **Mejora**: checklist semestral con `vault-health` (versiones/recencia de autor), promoción de las que el usuario adapte a la vault.

## P3-02 — Portabilidad multi-máquina

- **Detalle**: rutas absolutas (`C:\Users\sebas\...`) en scripts, plugin y skills; otra máquina los rompe.
- **Mejora**: relativizar paths (convención `~vault/` o variable de entorno `VAULT_PATH`) y documentar clonado del setup (config + vault git).
- **Verificación**: clonar en máquina de prueba y ejecutar `sync-skills.ps1`.

## P3-03 — Log semanal de salud automático

- **Detalle**: `vault-health` es on-demand.
- **Mejora**: tarea programada (Task Scheduler) que corre la skill vía `opencode run` y escribe el reporte al Registro de cada lunes.
- **Verificación**: entrada de salud en el registro el lunes siguiente.

## Criterio de priorización

P1 = afecta fiabilidad actual (MCP) o dinero (métricas) o seguridad (backup). P2 = mejora la ergonomía. P3 = higiene a largo plazo. Revisar este plan cada 2-3 meses con `vault-health`.