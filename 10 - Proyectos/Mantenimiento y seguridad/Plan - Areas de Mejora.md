---
created: 2026-08-19
updated: 2026-08-19
tags: [proyecto, plan, mejoras, pendiente]
---

# Plan — Áreas de Mejora del sistema cerebro

Plan de mejora continua detectado al cierre del plan principal (Fases 1-5, 2026-08-19). **NO implementar ahora**: cada área es candidata a sesión propia. Prioridad: P1 (alto valor), P2 (medio), P3 (bajo).

## P1-01 — Validar el acceso MCP real (hoy se usa filesystem)

- **Detalle**: el plugin Obsidian Local REST API requiere `NODE_EXTRA_CA_CERTS` + cert confiable; la implementación y este cierre usaron sistema de archivos directo.
- **Mejora**: configurar el certificado de una vez (importar al store + variable de entorno permanente), reiniciar opencode y probar `vault_*` en una sesión real; decidir si el fallback filesystem queda como respaldo documentado (sí) o como primario.
- **Verificación**: `vault_list`/`vault_read` responden; sesión con MCP registra menos tokens que la misma vía filesystem.

## P1-02 — Backup remoto (GitHub) ✅ RESUELTO 2026-08-19

- creado `https://github.com/sebaus75/Sebastian-Knowledge-Vault` (privado, push hecho).
- **Restante (menor)**: verificar el push automático del plugin en un cierre de sesión real y agendar respaldo semanal complementario (Task Scheduler).

## P1-03 — Métricas de tokens por sesión (requisito 6 del plan original: modelos de pago)

- **Detalle**: no hay telemetría de consumo por sesión; la optimización existe (límites + presupuesto §7) pero no se mide.
- **Mejora**: ampliar el plugin `vault-brain-lifecycle` para registrar en `session.status`/`session.diff` el consumo de tokens de la sesión en el Registro del día (una línea); comparar sesiones antes/después de mejoras.
- **Verificación**: línea de consumo en `90 - Sistema/Registros/YYYY-MM-DD.md` al cierre de cada sesión.

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