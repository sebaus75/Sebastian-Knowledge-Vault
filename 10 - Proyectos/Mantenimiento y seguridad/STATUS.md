---
proyecto: "Mantenimiento y seguridad"
fase: "sistema-cerebro"
actualizado: 2026-08-19
estado: Activo
tags: [proyecto, status, sistema, vault]
---

# STATUS — Mantenimiento y seguridad

## Fase actual

`sistema-cerebro` — Implementación del plan "Obsidian como cerebro de todos los agentes" (5 fases).

## Hecho (más reciente primero)

- [2026-08-19] **Fase 3 completada** — Plugin `vault-brain-lifecycle` (session.created → sync skills; session.deleted → backup git; validado), script `backup-vault.ps1` (primer commit real de la vault), skill `vault-health` (checklist completa). **Ojo**: vault sin remote de GitHub (pendiente desde 2026-08-10). Detalle: [[90 - Sistema/Registros/2026-08-19]].
- [2026-08-19] **Fases 2A y 2B completadas** — Auditoría de skills (42 → 26: 16 eliminadas a respaldo, 2 migradas) y skills en la vault (`30 - Recursos/Skills/` + `sync-skills.ps1` probado + `INDICE.md` + `FEEDBACK.md`). Detalle: [[90 - Sistema/Registros/2026-08-19]].
- [2026-08-19] **Fase 1 completada** — Universalidad y enrutamiento: AGENTS.md global creado (`~/.config/opencode/AGENTS.md`), MANIFEST.md creado (mapa de 7 proyectos), skill `vault-brain` refinado (enrutamiento por tipo de tarea + auto-provisioning), auto-provisioning de 4 proyectos (El Legado, Mantenimiento y seguridad, Proyectos CAD, Sentido Creativo). Detalle: [[90 - Sistema/Registros/2026-08-19]].
- [2026-08-10] Instalación del sistema cerebro (AGENTS.md, CONTEXT, STATUS, registros) + conexión MCP + auditoría de enlaces. Detalle: [[90 - Sistema/Registros/2026-08-10]].

## En progreso

- [ ] **Fase 3 cierre** — Configurar remote de GitHub para la vault (respaldo semanal real; pendiente desde 2026-08-10).

## Bloqueado / Pendiente

- [ ] **Fase 4** — Auditoría de límites de tokens (CONTEXT/STATUS) + ADR por proyecto (sección "Decisiones" en MOCs).
- [ ] **Fase 5** — Validación end-to-end (sesión desde directorio neutro) y métricas de tokens antes/después.

## Decisiones recientes

- [2026-08-19] La vault es el cerebro de **toda** sesión de OpenCode vía AGENTS.md global (no solo proyectos con AGENTS.md propio).
- [2026-08-19] Enrutamiento centralizado en `90 - Sistema/MANIFEST.md`; proyectos sin carpeta en vault se auto-provisionan sin preguntar.
- [2026-08-19] Sync de skills: script PowerShell + hook de inicio (fuente de verdad: vault). Hooks: plugin propio mínimo.
- [2026-08-19] Las 42 skills actuales se auditan antes de migrar (fusionar/eliminar/mejorar).

## Próxima sesión

- **Fase 2A**: auditar las 42 skills (leer descripciones/estructura, detectar redundancias) y presentar factura de cambios.

---
_Actualizar al final de cada sesión. Ver `AGENTS.md` (protocolo) y `90 - Sistema/Registros/`._