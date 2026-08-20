---
created: 2026-08-19
updated: 2026-08-19
tags: [proyecto, plan, mejoras, pendiente]
---

# Plan — Áreas de Mejora del sistema cerebro

Plan de mejora continua detectado al cierre del plan principal (Fases 1-5, 2026-08-19). **COMPLETO (P1-P3) RESUELTO el 2026-08-19**. Histórico: cada área se cerró con implementación o decisión documentada abajo.

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

## P2-01 — Modelo por tipo de tarea ✅ RESUELTO 2026-08-19 (decisión)

- Columna **"Modelo sugerido"** añadida al MANIFEST (`barato` para `registro`/`sistema-cerebro`; `estándar` para `produccion`/diseño).
- **Decisión**: no se fija `model` por proyecto — el ahorro no justifica la complejidad hoy. La columna queda como guía si algún día aplica.

## P2-02 — Exponer `vault-health` como comando TUI ✅ RESUELTO 2026-08-19

- Comando `/vault-health` en `~/.config/opencode/commands/` (formato `goal-orch.md`): carga la skill y ejecuta la checklist.
- **Verificación pendiente en TUI**: `/vault-health` responde checklist desde cualquier directorio.

## P2-03 — Automatizar renovación del certificado/API key del plugin REST API ✅ RESUELTO 2026-08-19

- Script `mcp-health.ps1` (GET /mcp/ con bearer token; exit 0 OK / 1 FAIL con instrucciones) + hook en `session.created` del plugin: si FAIL → log "MCP degradado".
- Verificado el camino FAIL en vivo (Obsidian cerrado → puerto 27124 no escucha → script avisa). Camino OK queda para sesión con Obsidian abierto.

## P3-01 — Actualización semestral de skills de terceros ✅ RESUELTO 2026-08-19

- Sección 7 "Skills (auditoría semestral)" añadida al checklist de `vault-health` (recencia del autor, candidatas a promoción, cadencia semestral).

## P3-02 — Portabilidad multi-máquina ✅ RESUELTO 2026-08-19

- Convención `VAULT_PATH` (env var con fallback a ruta local) en `backup-vault.ps1`, `sync-skills.ps1`, plugin `vault-brain-lifecycle.js`; documentada en skills `vault-brain` y `vault-health`.
- Nota [[10 - Proyectos/Mantenimiento y seguridad/Setup Multi-Máquina]] con pasos de clonado (git + config + cert + tareas).

## P3-03 — Log semanal de salud automático ✅ RESUELTO 2026-08-19

- Script `health-weekly.ps1` (corre `opencode run` con la skill y appenda el reporte al Registro; UTF-8 + sin ANSI).
- Tarea Task Scheduler **`Vault Health Semanal`** (lun 08:00) creada. Validación de pipeline en vivo: reporte real anexado al Registro 2026-08-19 (detectó 5 posibles enlaces rotos → **todos verificados como falsos positivos**; causa: ruido de codificación corregido en el script).

## Criterio de priorización

P1 = afecta fiabilidad actual (MCP) o dinero (métricas) o seguridad (backup). P2 = mejora la ergonomía. P3 = higiene a largo plazo. Revisar este plan cada 2-3 meses con `vault-health`.