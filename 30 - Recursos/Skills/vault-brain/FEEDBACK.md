# FEEDBACK — vault-brain

Registro de lecciones aprendidas al usar la skill. Append-only.

## 2026-08-19 — Implementación Fase 1 del sistema cerebro

- El skill ahora rutea vía `90 - Sistema/MANIFEST.md` (enrutamiento central, no adivinar).
- **Auto-provisioning funciona**: se crearon 4 proyectos (El Legado, Mantenimiento y seguridad, Proyectos CAD, Sentido Creativo) con MOC+STATUS en el mismo turno sin preguntar. Lección: el MOC y el STATUS se escribe solo con hechos verificados del turno; lo desconocido queda como checkbox pendiente (no inventar).
- La regla global ahora también está en `~/.config/opencode/AGENTS.md` — la skill es el detalle operativo, el AGENTS.md global el contrato breve.
- **Ojo**: después de migrar la skill a la vault (30 - Recursos/Skills/), los cambios editables son los del vault; la copia en `~/.config/opencode/skills/` es un snapshot del sync. Editar SIEMPRE en el vault y re-sincronizar.