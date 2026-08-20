---
name: vault-brain
description: Procedimiento para usar la vault de Obsidian (Sebastian Knowledge Vault) como memoria de trabajo de OpenCode. Usar al iniciar una sesión sobre cualquier proyecto de la vault, al terminar la sesión, o cuando se pregunte por estado, fase, progreso o qué falta. La vault es local: se accede por sistema de archivos y, si está disponible, por MCP (obsidian-local-rest-api).
---

# vault-brain — Protocolo de memoria

La vault en `C:\Users\sebas\Desktop\Sebastian_Knowledge_Vault\Sebastian Knowledge Vault` es la memoria persistente: qué hay, qué se hizo, qué falta y qué sigue. Reglas completas en su `AGENTS.md`.

## Ruta de acceso

- **MCP disponible** (config global de opencode, requiere `NODE_EXTRA_CA_CERTS` y reinicio de la app): usar herramientas `vault_*`, `search_*`, `tag_list` — prefieren estructura y ahorran tokens.
- **Sin MCP**: leer/escribir directamente por sistema de archivos (misma ruta).
- **Ojo**: si Obsidian se reinicia, el plugin puede regenerar certificado y API key. Si el MCP falla con 401/cert, re-descargar de la UI del plugin, importar el cert al store y actualizar `NODE_EXTRA_CA_CERTS` + las configs `opencode.json` / `opencode.jsonc`.

## 1. Inicio de sesión (siempre)

1. Leer `CONTEXT.md` (estado global, ≤2KB). Si responde la pregunta, parar.
2. Leer `90 - Sistema/MANIFEST.md` solo si el trabajo toca un proyecto (obtener enrutamiento: carpeta de proyecto ↔ carpeta de vault, fase, skills asociadas). Si el proyecto **no aparece** en el MANIFEST → auto-provisioning (§1.1).
3. Leer `10 - Proyectos/<P>/STATUS.md` del proyecto implicado (≤3KB).
4. Solo si se necesita detalle: `vault_get_document_map` sobre la nota → `vault_read` dirigido.
5. Nunca leer carpetas enteras ni volcar proyectos "por contexto".

## 1.1 Auto-provisioning (proyecto nuevo en la vault)

Si el proyecto de código no tiene carpeta en `10 - Proyectos/` ni fila en el MANIFEST:

1. Crear `10 - Proyectos/<Nombre>/MOC.md` (overview + Map of Content, frontmatter `estado: Activo`, `fase: <por definir>`, `created`, `tags`).
2. Crear `10 - Proyectos/<Nombre>/STATUS.md` (plantilla: `90 - Sistema/Plantilla - STATUS.md`; secciones Fase actual / Hecho / En progreso / Bloqueado / Decisiones / Próxima sesión).
3. Añadir la fila al MANIFEST (`90 - Sistema/MANIFEST.md`) con la fase inicial.
4. Completar solo con hechos verificados del turno (leer archivos del proyecto si hace falta, sin volcarlos). Lo desconocido queda como pendiente en STATUS.

## 2. Trabajo (reglas)

- Leer antes de escribir. No sobrescribir sin leer.
- Nunca borrar: mover a `40 - Archivo/` (`vault_move`).
- Cambios en un proyecto → actualizar su `STATUS.md` (una línea en "Hecho" o "En progreso") en el mismo turno.
- Frontmatter: actualizar `updated: YYYY-MM-DD` solo si el contenido de la nota cambió.

## 3. Cierre de sesión (obligatorio)

1. `90 - Sistema/Registros/YYYY-MM-DD.md` — crear o append: qué se hizo, qué falta, decisiones, enlaces. Append-only, no resumir sesiones viejas.
2. `STATUS.md` del/los proyecto(s) tocado(s): mover checkboxes a "Hecho", actualizar "Próxima sesión".
3. `CONTEXT.md` — solo si cambió la foto global (proyectos activos, fases, pendientes urgentes). Máximo 2KB.

## 4. Transición de fase

1. `fase` + `updated` en el MOC del proyecto.
2. Línea en `STATUS.md` → "Decisiones recientes".
3. Si se cierra: mover a `40 - Archivo/`, quitar de `CONTEXT.md` y `Home.md`.

## 5. Consultas comunes (estado / qué falta / qué sigue)

- "¿Qué falta?": leer `STATUS.md` del proyecto → "Bloqueado / Pendiente" + "En progreso".
- "¿Dónde vamos en general?": `CONTEXT.md` → tabla de proyectos.
- "¿Qué se hizo el <fecha>?": `90 - Sistema/Registros/<fecha>.md`.
- "¿Qué sigue?": sección "Próxima sesión" de cada STATUS, o "Pendientes globales" en CONTEXT.

## 6. Capa de memoria según tipo de tarea

Elegir la capa mínima que resuelve la tarea (ahorra tokens; no leer más de lo necesario):

| Tipo de tarea | Qué leer | Qué escribir |
|---|---|---|
| Trabajo en un proyecto | CONTEXT → MANIFEST → STATUS → nota dirigida | STATUS + notas del proyecto + Registro |
| Pregunta transversal (concepto, receta) | CONTEXT → búsqueda dirigida (`search_query`) en `30 - Recursos/` | — (o nota en Recursos si aporta) |
| Decisión de diseño/arquitectura | STATUS (Decisiones) + MOC del proyecto | Sección "Decisiones" del STATUS/MOC + Registro |
| Mantenimiento de la vault | CONTEXT + Inbox + health-check | Registro + índices + `40 - Archivo/` |
| Sesión de documentación | CONTEXT → MANIFEST (destino según tabla del MANIFEST) | Carpeta del proyecto / Recursos / Registro |

## Tokens

- Máximos: CONTEXT ≤2KB, STATUS ≤3KB. Si crecen, mover detalle a notas/registros.
- Leer solo lo necesario; el conocimiento vive en las notas, no en la conversación.
