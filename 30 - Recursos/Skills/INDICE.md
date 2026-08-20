---
created: 2026-08-19
updated: 2026-08-19
tags: [meta, skills, sistema]
---

# ÍNDICE — Skills de la vault

Fuente de verdad de las skills propias del sistema. Cada carpeta = 1 skill (`SKILL.md` + opcional `FEEDBACK.md`). El script `sync-skills.ps1` (~/.config/opencode/scripts/) las copia a la config global de OpenCode al iniciar sesión, donde se descubren **automáticamente** por su `description`.

## Skills propias (en la vault)

| Skill | Descripción | Cuándo se usa (automático) | Carpeta |
|---|---|---|---|
| `vault-brain` | Protocolo de memoria: la vault como cerebro de toda sesión (inicio, enrutamiento vía MANIFEST, cierre, tokens). | En toda sesión que toque proyectos, estado, progreso o documentación de la vault. | `30 - Recursos/Skills/vault-brain/` |
| `vault-health` | Auditoría de salud de la vault: enlaces, frontmatter, límites, MANIFEST, inbox, backup/sync. | Mantenimiento, health-check, auditorías o revisiones periódicas de la vault. | `30 - Recursos/Skills/vault-health/` |
| `wolf-barber-booking` | Sistema completo de booking + admin de Wolf Barber (GAS + Calendar + Sheets). | Cualquier trabajo sobre el sitio/admin/backend de Isaac Torres. | `30 - Recursos/Skills/wolf-barber-booking/` |

## Reglas del sistema de skills

1. **Crear**: toda skill nueva se crea en `30 - Recursos/Skills/<nombre>/SKILL.md` (frontmatter `name` + `description` obligatorios; nombre en kebab-case). El sync la hace visible a OpenCode.
2. **Mejorar**: cada uso deja lecciones en `FEEDBACK.md` de la skill. Correcciones repetidas → promovidas al `SKILL.md`.
3. **Eliminar/fusionar**: mover a `40 - Archivo/Skills/` (nunca borrar) y actualizar este índice + el sync (el script no sincroniza lo archivado).
4. **Skills de terceros** (web, docs, pdf, vercel, etc.): viven en `~/.config/opencode/skills/` directamente, NO se versionan aquí.

## Procedimiento de sync (manual)

```powershell
powershell -ExecutionPolicy Bypass -File "$env:USERPROFILE\.config\opencode\scripts\sync-skills.ps1"
```

El hook de inicio de sesión (Fase 3) lo ejecutará automáticamente. Verificar: `Get-ChildItem ~/.config/opencode/skills`.