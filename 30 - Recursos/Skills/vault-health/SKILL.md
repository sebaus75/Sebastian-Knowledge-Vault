---
name: vault-health
description: Auditoria de salud de la vault de Obsidian (Sebastian Knowledge Vault). Usar al iniciar sesiones de mantenimiento, cuando se pida "health-check", "auditar la vault", "revisar enlaces", "verificar estado del sistema cerebro", "mantenimiento de la vault" o como parte de revisiones periodicas. Ejecuta checklist: enlaces rotos, frontmatter, STATUS frescos, limites de tokens, inbox, indice de skills.
---

# vault-health — Auditoría de la vault

Fuente de verdad: `C:\Users\sebas\Desktop\Sebastian_Knowledge_Vault\Sebastian Knowledge Vault`. Ejecutar la checklist completa; reportar solo problemas (con ruta y acción). No corregir ni documentar sin leer antes.

## Checklist

### 1. Enlaces internos

- Buscar referencias rotas: `[[...]]` y links markdown con rutas `10 -`, `30 -`, `40 -`, `90 -` que no existan (usar `search_query` o grep por ruta completa).
- Orfandad inversa: notas en `10 - Proyectos/` no referenciadas ni por su MOC.
- **Acción**: reparar enlaces con `vault_move`/`vault_patch`, o mover la nota a `40 - Archivo/` si cerró.

### 2. Frontmatter y convenciones

- Toda nota con `created`; `updated` presente y con fecha de la última edición real (no tocar si el contenido no cambió).
- Naming `Nombre - Descripcion.md`; MOCs con `estado`/`fase`; STATUS con `actualizado`.
- **Acción**: normalizar sin reescribir contenido.

### 3. STATUS y CONTEXT

- `CONTEXT.md` ≤ **2 KB** y `STATUS.md` de cada proyecto ≤ **3 KB** (medir; si crecen, mover detalle a notas/registros).
- `STATUS.md` con `actualizado` ≥ 14 días → marcar "revisar" y proponer próxima sesión.
- Proyectos en `CONTEXT.md` que no estén en `10 - Proyectos/` (o viceversa) → alinear vía MANIFEST.

### 4. MANIFEST e índices

- Todo proyecto de `Proyectos Open Code/` con fila en `90 - Sistema/MANIFEST.md` y carpeta en `10 - Proyectos/` (auto-provisioning si falta).
- `30 - Recursos/Skills/INDICE.md` al día con las skills reales de la carpeta.

### 5. Inbox y archivo

- `00 - Inbox/` vacío o con plan de procesado (procesar antes de otra tarea, según AGENTS.md).
- `40 - Archivo/` sin duplicados.

### 6. Backup y sync

- `.git` de la vault: `git status` limpio (después de backup) y remote configurado; si no, avisar (backup semanal GitHub pendiente hasta configurar remote).
- Skills: correr `sync-skills.ps1` y verificar que `~/.config/opencode/skills/<vault-*>` coinciden con la vault.

## Reporte

Salida compacta por sección: `OK` o `⚠️ <ruta>: <problema> -> <acción>` . Si hay correcciones, aplicarlas (lectura previa) y anotar en el registro del día.

## FEEDBACK

Lecciones aprendidas al usar esta skill se anotan en `FEEDBACK.md` de esta misma carpeta (append-only).