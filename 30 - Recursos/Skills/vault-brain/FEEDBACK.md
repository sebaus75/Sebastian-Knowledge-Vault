# FEEDBACK — vault-brain

Registro de lecciones aprendidas al usar la skill. Append-only.

## 2026-08-19 — Implementación Fase 1 del sistema cerebro

- El skill ahora rutea vía `90 - Sistema/MANIFEST.md` (enrutamiento central, no adivinar).
- **Auto-provisioning funciona**: se crearon 4 proyectos (El Legado, Mantenimiento y seguridad, Proyectos CAD, Sentido Creativo) con MOC+STATUS en el mismo turno sin preguntar. Lección: el MOC y el STATUS se escribe solo con hechos verificados del turno; lo desconocido queda como checkbox pendiente (no inventar).
- La regla global ahora también está en `~/.config/opencode/AGENTS.md` — la skill es el detalle operativo, el AGENTS.md global el contrato breve.
- **Ojo**: después de migrar la skill a la vault (30 - Recursos/Skills/), los cambios editables son los del vault; la copia en `~/.config/opencode/skills/` es un snapshot del sync. Editar SIEMPRE en el vault y re-sincronizar.
## 2026-08-19 — Sesión P1 (MCP, métricas, push)

- **vault_patch: `replace` sobre un heading H1 (raíz) pisa TODO el subtree del documento** — ocurrió 2 veces (Plan - Areas de Mejora → 388 B; CONTEXT → 241 B) y hubo que restaurar de la lectura previa. Lección: para editar el cuerpo del H1, usar scope `content` sobre el H1 con SOLO el texto de intro… mejor: nunca tocar el H1 raíz; fijar el target al heading hijo (la ruta debe incluir el H1 + hijos: `["H1", "Heading hijo"]`). Siempre leer el archivo antes de parchear y verificar tamaño tras parchear.
- **Los headings con acentos/paréntesis se resuelven igual** (falla solo si falta el H1 en la ruta del target; con ruta completa funcionó con "Hecho (más reciente primero)").
- **Verificación**: tras cada patch de CONTEXT/STATUS comprobar el tamaño (límites del protocolo) — se detectaron 2052 B y 4644 B fuera de presupuesto en el cierre.
- El evento `session.deleted` de opencode NO expone tokens; el consumo vive en los parts `step-finish` de los mensajes (`p.tokens.input/output`, `p.cost`) — resumir con `client.session.messages({path:{id}})`.