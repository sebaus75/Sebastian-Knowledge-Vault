# AGENTS.md — Sebastian Knowledge Vault

Contrato operativo para agentes de IA (OpenCode/Claude) que trabajen con esta vault.
La vault es la memoria de trabajo: qué hay, qué se hizo, qué falta y qué sigue.

## 1. Mapa de carpetas (método PARA)

- `00 - Inbox/` — notas sin procesar. Revisar al inicio; si hay notas, procesarlas antes de otra tarea.
- `10 - Proyectos/<Proyecto>/` — proyectos con objetivo y fecha de fin. Cada proyecto tiene `MOC.md` (índice), `STATUS.md` (estado) y sus notas.
- `20 - Areas/` — responsabilidades continuas (sin fecha de fin).
- `30 - Recursos/` — material de referencia y conocimiento permanente.
- `40 - Archivo/` — todo lo cerrado/obsoleto. **Nunca borrar**: archivar aquí.
- `90 - Sistema/` — infraestructura de la vault: `MANIFEST.md` (enrutamiento proyecto→carpeta de vault), `Registros/` (log de sesiones), `Panel de Estado.md` (dashboard), plantillas.
- Raíz: `Home.md` (MOC raíz), `CONTEXT.md` (estado global ≤2KB), `VAULT.md` (guía del vault), este archivo.

## 2. Reglas de oro

1. **Nunca borrar notas**: mover a `40 - Archivo/` con `vault_move`.
2. **Append-only** en `90 - Sistema/Registros/`: cada sesión es un archivo `YYYY-MM-DD.md`.
3. **Estado siempre al día**: todo cambio en un proyecto actualiza su `STATUS.md` (una línea) el mismo turno.
4. **No duplicar conocimiento**: si una nota existe, enlazarla; no recrearla.
5. **Leer antes de escribir**: nunca sobrescribir sin haber leído el archivo.

## 3. Protocolo de lectura (ahorrar tokens)

Orden estricto, de lo pequeño a lo grande:

1. `CONTEXT.md` — snapshot global (2KB). No leer más si responde la pregunta.
2. `90 - Sistema/MANIFEST.md` — enrutamiento: qué proyecto se documenta en qué carpeta de la vault.
3. `10 - Proyectos/<P>/STATUS.md` — estado del proyecto (3KB).
3. Nota específica vía MCP dirigido: `vault_get_document_map` para headings/frontmatter → `vault_read` de la sección exacta.
4. `search_query`/`search_simple` para localizar, `tag_list` para inventarios.

**Prohibido**: leer carpetas completas, volcar proyectos enteros o leer todas las notas "para tener contexto". Si necesitas contexto general, usa `Panel de Estado.md` y los MOCs.

## 4. Protocolo de escritura

- Fin de cada sesión de trabajo (humano o IA):
  - Añadir a `90 - Sistema/Registros/YYYY-MM-DD.md` (crear si no existe): qué se hizo, qué falta, decisiones, enlaces.
  - Actualizar `STATUS.md` del/los proyecto(s) tocados (sección "Hecho", "Próxima sesión").
  - Actualizar `CONTEXT.md` solo si cambia la foto global (proyectos activos, fases, pendientes urgentes).

## 5. Transición de fase de proyecto

Al mover un proyecto a otra fase (`fase` en frontmatter del MOC):

1. Actualizar `fase` y `updated` en `10 - Proyectos/<P>/<MOC>.md`.
2. Escribir el cambio en `STATUS.md` (sección "Decisiones").
3. Si se cierra: mover a `40 - Archivo/` y quitarlo de `CONTEXT.md` + `Home.md`.

## 6. Convenciones

- **Frontmatter** (en notas): `created: YYYY-MM-DD`, `updated: YYYY-MM-DD` (editar solo al cambiar el contenido), `tags`, y en MOCs de proyecto: `estado: Activo|Pausado|Archivado`, `fase: <libre por proyecto>`.
- **Fases por proyecto** (ejemplos): Wolf Barber → `produccion`; Suplehuges → `propuesta-comercial`; TemplateTest → `listo-empaquetar`.
- **Checkboxes**: `- [ ]` pendiente, `- [x]` hecho. STATUS usa esta forma.
- **Fechas** ISO `YYYY-MM-DD` siempre.
- **Naming**: `Nombre - Descripcion.md`; enlaces a ruta completa desde raíz (`[[10 - Proyectos/...]]`) cuando haya basenames duplicados.

## 7. Límites de tamaño (diseño token-eficiente)

- `CONTEXT.md` ≤ 2KB, `STATUS.md` ≤ 3KB (si crece, mover detalle a notas/registros).
- Notas en pirámide invertida: conclusión primero, detalle abajo.
- Registros de sesión no se resumen: son historial append-only.

## 8. Acceso MCP (obsidian-local-rest-api)

`vault_list`, `vault_read`, `vault_write`, `vault_append`, `vault_patch`, `vault_delete` (→ papelera), `vault_move`, `vault_copy`, `vault_get_document_map`, `active_file_get_path`, `search_query`, `search_simple`, `tag_list`, `command_list`, `command_execute`, `open_file`.
Preferir MCP sobre el sistema de archivos directo cuando esté disponible.
