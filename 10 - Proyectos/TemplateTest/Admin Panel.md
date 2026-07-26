---
tags: [admin, cms, frontend, panel]
---
# Admin Panel

**Archivos**: `admin.html` (~337 líneas, estilos inline) + `assets/js/admin.js` (~829 líneas)

CMS completo con 12 pestañas, CRUD genérico, editor de temas en vivo y exportación de datos.

## Login

- **Password por defecto**: `admin123` (validación local con SHA-256 × 1000)
- Rate limiting: 5 intentos fallidos → bloqueo 15 min (persistente en localStorage)
- Sesión en memoria (no persiste en storage al cerrar pestaña)
- CSRF token rotado en cada login
- Audit log de intentos de acceso

## Pestañas

### Dashboard
Resumen visual con cards de: servicios activos, reseñas, total bookings, items en galería.

### Servicios
CRUD completo: nombre, descripción, precio ($), duración (min), imagen URL, activo/inactivo. Preview de imagen en tabla. Search/filtro en vivo. Paginación (10 items/página). Duplicar servicio.

### Galería
CRUD con drag & drop reorder (arrastrar para reordenar). Título, imagen URL, blur placeholder. Lazy loading en landing. Lightbox navegable con teclado.

### Reseñas
CRUD: nombre del cliente, texto, rating (1-5 estrellas), activo/inactivo. Se muestran en grid en landing.

### FAQ
CRUD: pregunta, respuesta (contenteditable rich text), activo/inactivo, orden. Acordeón en landing (solo un item abierto).

### Horarios
Editor por día: toggle abierto/cerrado, hora apertura, hora cierre. Buffer predeterminado 15 min entre citas. Feriados configurables.

### Profesionales
CRUD: nombre, especialidad, biografía, avatar URL. Se asignan a servicios en booking.

### Clientes
Tabla read-only con datos de clientes que han agendado. Nombre, email, teléfono, servicio, profesional, fecha, estado. Exportable a CSV.

### Bookings
Lista de citas agendadas con filtro por fecha/estado. Posibilidad de confirmar, cancelar o marcar completada.

### Theme
Editor visual de tema en vivo con color pickers (primary, secondary, accent, background, surface, text), selectores de fuente, hero overlay gradient, configuración SEO (title, description, keywords), custom CSS/HTML hooks. Vista previa instantánea al cambiar colores. Selector de tema activo entre los 4 predefinidos. Toggle dark/light/system.

### Config
Configuración general: URL de Google Sheets (backend GAS), email de notificaciones, secciones on/off con toggle, orden de secciones drag & drop, password admin (con confirmación). Reset a valores por defecto con confirmación.

### Audit
Historial de acciones administrativas: timestamp, acción, detalle. Botón para limpiar logs.

## UX del admin

| Feature | Detalle |
|---|---|
| Keyboard shortcuts | `Ctrl+S` guardar cambios, `/` focus search |
| Unsaved changes warning | Alerta si hay cambios sin guardar al cambiar de pestaña |
| Auto-save indicator | "Guardado" / "Guardando..." / "Cambios sin guardar" |
| Character count | Contador en inputs de texto largo |
| Image preview | Thumbnail en tablas de servicios, galería, profesionales |
| Search/filter | Filtrado en vivo sobre todas las tablas |
| Pagination | 10 items/página con navegación |
| Duplicate | Clona item y abre modal para editar |
| Preview | Botón que abre landing en nueva pestaña con datos actuales |
| Confirm dialogs | En todas las acciones destructivas (eliminar, reset) |
| Focus trap | En modales (Tab circula dentro, Escape cierra) |
| Toast notifications | Feedback visual en todas las operaciones |
| Aria labels | En todos los botones de solo icono |
