---
tags: [admin, cms, frontend]
created: 2026-07-24
---
# Admin Panel

**Archivos**: `admin.html` (~489 líneas) + `css/admin.css` + `js/admin.js` (~838 líneas)

CMS completo para gestionar el sitio sin tocar código.

## Login

- **Usuario**: `wolfbarber` / **Contraseña**: `wolfbarber2026` (validación local)
- URL del API se configura **después del login** en la pestaña Config
- Si no hay URL configurada, aparece un **banner amarillo** guiando al usuario
- Sesión en memoria (no persiste en sessionStorage)
- Al salir, se limpian campos y se oculta el panel

## Pestañas

### Servicios
CRUD completo por cada servicio:
- Nombre, descripción, precio, duración
- Imagen (subida a Google Drive vía API)
- Activo/Inactivo, Orden
- Preview de imagen con drag & drop

### Galería
- Subir imágenes con drag & drop
- Asignar categoría (fade, diseños, barba, coloración)
- Preview antes de guardar
- Eliminar items

### Horarios
- CRUD de franjas horarias por día
- Día, hora inicio, hora fin, activo/inactivo
- Ordenado por día de la semana
- Seed data: 12 franjas default

### Clientes
- Tabla con nombre, email, teléfono, servicio, fecha, folio
- Solo lectura (se llena automáticamente con cada booking)
- Ordenado del más reciente al más antiguo

### Reseñas
- CRUD completo
- Campos: nombre, texto, rating (1-5 estrellas), activo, orden
- Se muestran en el carrusel del frontend (solo activas)

### FAQ
- CRUD completo
- Campos: pregunta, respuesta, activo, orden
- Se muestran en el acordeón del frontend (solo activas)

### Configuración
| Feature | Detalle |
|---|---|
| URL del API | Campo + botón **"Confirmar"** → guarda en localStorage |
| Cambiar contraseña | Actualiza `admin_password` en Config sheet |
| Usuarios | Gestión de hasta **3 usuarios** (username + password) |

### Usuarios (en Config)
- Tabla con username, contraseña oculta, acciones (editar/eliminar)
- Botón "Agregar" que se **deshabilita al llegar a 3**
- Validaciones: username ≥ 3 chars, password ≥ 4 chars, username único
- Almacenados en sheet `Usuarios` del backend
- Los passwords de la sheet también permiten login admin

## Upload de imágenes
- Drag & drop o click para seleccionar archivo
- Validación cliente: 10MB máximo
- Subida a Google Drive → URL pública devuelta
- Formatos: jpg, jpeg, png, gif, webp, svg
