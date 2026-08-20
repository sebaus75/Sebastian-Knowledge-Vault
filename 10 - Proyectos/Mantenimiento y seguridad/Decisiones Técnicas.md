---
created: 2026-08-19
updated: 2026-08-19
tags: [proyecto, adr, decisiones, sistema]
---

# Decisiones Técnicas — Mantenimiento y seguridad

Registro de decisiones de arquitectura y configuración del sistema cerebro. Append-only: cada entrada es un ADR corto (contexto → decisión → consecuencia).

## ADR-001 — La vault es el cerebro de toda sesión de OpenCode

- **Fecha**: 2026-08-19
- **Contexto**: los agentes solo cargaban el protocolo cuando el proyecto tenía `AGENTS.md` propio; sesiones en directorios neutros quedaban sin memoria.
- **Decisión**: `~/.config/opencode/AGENTS.md` global; enrutamiento centralizado en `90 - Sistema/MANIFEST.md`; skill `vault-brain` como protocolo operativo.
- **Consecuencia**: toda sesión arranca con el protocolo (CONTEXT → MANIFEST → STATUS → detalle dirigido) y cierra documentando (Registro + STATUS). Auto-provisioning si un proyecto no existe en la vault.

## ADR-002 — Skills: la vault es la fuente de verdad; config es snapshot

- **Fecha**: 2026-08-19
- **Contexto**: las skills vivían solo en `~/.config/opencode/skills/`; no se compartían entre proyectos ni se versionaban; la auditoría dejó 26 activas.
- **Decisión**: `30 - Recursos/Skills/` (vault) = fuente de verdad; `sync-skills.ps1` copia vault → config global en cada `session.created` (plugin `vault-brain-lifecycle`). Formato `SKILL.md` + `FEEDBACK.md` (lecciones que se promueven al skill).
- **Consecuencia**: editar siempre en la vault; la copia en config es snapshot. Eliminación de skills de terceros → respaldo en `%LOCALAPPDATA%\Temp\opencode\skills-backup-2026-08-19\`.

## ADR-003 — Backup git automático en cierre de sesión

- **Fecha**: 2026-08-19
- **Contexto**: la vault tenía git local sin remote y sin automatismo; respaldo GitHub pendiente desde 2026-08-10.
- **Decisión**: `backup-vault.ps1` (commit local; push si hay remote) ejecutado por el plugin en `session.deleted`. Pendiente: crear remote (ver STATUS).
- **Consecuencia**: historial por sesión garantizado; el push a GitHub queda activo automáticamente en cuanto exista remote.

## ADR-004 — Límites de tokens y lectura mínima

- **Fecha**: 2026-08-19
- **Contexto**: garantizar eficiencia con modelos de pago sin perder rendimiento.
- **Decisión**: CONTEXT ≤2KB, STATUS ≤3KB (verificado y Suplehuges estabilizado a 2.43KB); en el skill `vault-brain` sección "Presupuesto de lectura" (elegir la operación más barata que resuelva la tarea: STATUS antes que notas; `document_map` antes que `read`; `search` para localizar).
- **Consecuencia**: sesiones de consulta leen pocos KB; el detalle vive en notas/registros, no en la conversación.

## ADR-005 — Validación end-to-end del sistema (Fase 5)

- **Fecha**: 2026-08-19
- **Contexto**: cerrar el plan con evidencia de que el protocolo funciona en condiciones reales.
- **Decisión**: prueba con `opencode run` desde directorio neutro (sin AGENTS.md, sin git). Resultado: AGENTS.md global cargado (cita correcta de ruta y regla 1), lectura mínima respetada (el agente no inventó datos del MANIFEST sin leerlo), skills automáticas correctas (`vault-brain`, `vault-health`). Auditoría final: CONTEXT 2,019 B, todos los STATUS ≤2.5 KB.
- **Consecuencia**: plan 1-5 cerrado; el sistema queda operativo y autosostenible (sync de skills y backup en cada sesión).