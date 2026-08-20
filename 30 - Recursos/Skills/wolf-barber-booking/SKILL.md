---
name: wolf-barber-booking
description: >-
  Sistema completo de agendado de citas + panel admin para Wolf Barber (Isaac
  Torres). Frontend: booking modal multi-paso con horarios dinámicos, folios,
  cancelación, notificaciones WhatsApp, carrusel de reseñas, FAQ acordeón,
  animación hero. Backend: Google Apps Script (GAS) con Calendar, Drive,
  MailApp, auth local + por usuarios, CRUD servicios/galería/horarios/
  reseñas/FAQ/usuarios, upload de imágenes a Drive. Admin: panel con login
  local (usuario+pass), gestión completa del sitio. Usar siempre que se
  trabaje con el booking system, admin console, Code.gs, o se necesite
  configurar/replicar cualquiera de estos componentes.
---

# Wolf Barber — Sistema de Citas + Panel Admin

## Stack

### Frontend
- **HTML + CSS + JS vanilla**, Tailwind CDN (`tailwind.config` custom con colores gold, surface, cream)
- **Hero text-based**: gradiente vertical, "Isaac Torres" h1, `ᛟ WOLF BARBER ᛟ`, línea dorada, "Est. 2020". **Animación escalonada CSS**: fade-up 80px + blur + slide-line desde left
- **Booking modal**: 4-step wizard (servicio → fecha/hora dinámico desde horarios → datos con email → confirmar)
- **Horarios dinámicos**: fetch `?action=schedule` → slots según día, con fallback a 10:00-19:00
- **Reviews carrusel**: testimonios con auto-play 5s, dots, prev/next, touch support
- **FAQ acordeón**: preguntas frecuentes con toggle, solo una abierta a la vez
- **Admin console**: `admin.html` con login local, 7 pestañas de gestión
- **Móvil**: country selector + WhatsApp flotante + menú fullscreen

### Backend
- **Google Apps Script** (`Code.gs`) — web app "Ejecutar como: Yo, Acceso: Cualquiera"
- **Google Calendar** (`CalendarApp`) — crear/leer/cancelar eventos de cita
- **Google Drive** (`DriveApp`) — subir imágenes para servicios y galería
- **MailApp** — notificaciones al dueño al agendar cita
- **Sheets** (`SpreadsheetApp`) — 8 sheets: Servicios, Galeria, Config, Horarios, Clientes, Resenas, FAQ, Usuarios

## Archivos clave

| Archivo | Propósito |
|---------|-----------|
| `index.html` | Landing page: hero animado, servicios dinámicos, galería, booking modal, cancel modal, reviews carrusel, FAQ acordeón |
| `js/script.js` | Booking wizard con horarios dinámicos, render reviews/FAQ, fetch API, gallery filters, scroll-reveal, hero animación |
| `admin.html` | Panel admin: login local (usuario+pass), 7 pestañas (Servicios, Galería, Horarios, Clientes, Reseñas, FAQ, Config) |
| `js/admin.js` | API wrapper, CRUD completo para 6 entidades, login/logout local, upload imágenes, confirmar URL |
| `css/style.css` | Estilos: glass-nav, scroll-reveal, shimmer, booking modal, time-slots, country-selector, gallery filters, hero animation, carrusel, accordion |
| `css/admin.css` | Estilos del panel admin: tabs, scrollbar, tipografía Cinzel + DM Sans |
| `Code.gs` | Backend GAS: auth local + usuarios, 22 endpoints CRUD, calendar/booking, image upload, notifications, rate limiting |

## Flujo de agendado (usuario)

1. Usuario abre modal → selecciona servicio (paso 1) — servicios cargados dinámicamente desde GAS
2. Selecciona fecha (paso 2) → consulta horarios del día vía `?action=schedule`
3. Slots disponibles se generan según franjas horarias + duración del servicio
4. Slots ocupados se marcan `.time-slot.occupied` (consultados vía `?date=`)
5. Datos personales con country selector + campo email (paso 3) → resumen (paso 4)
6. `confirmBooking()`:
   - Genera folio `WB-XXXXXX` (6 chars sin vocales)
   - POST a GAS que crea evento en Calendar + envía email + guarda en Clientes
   - Guarda en `localStorage` (fallback offline)
   - Abre WhatsApp con mensaje pre-llenado (folio + datos del servicio)
   - Muestra pantalla de éxito con spinner

## Flujo de cancelación

- Modal de cancelación con input de folio
- `POST /` con `{ action: "cancel", folio: "WB-XXXXXX" }` — busca eventos futuros (hasta 180 días) que empiecen con el folio
- Si encuentra, elimina el evento y responde `{ success: true }`
- Muestra mensaje de éxito/error

## Panel Admin — `admin.html`

### Login
- **Usuario**: `wolfbarber` / **Contraseña**: `wolfbarber2026` (validación LOCAL, no requiere API)
- URL del API se configura después del login en la pestaña **Configuración**
- Banner amarillo si falta URL
- Sesión en memoria (no persiste en sessionStorage)

### Pestañas
1. **Servicios**: tabla con nombre, precio, duración, activo, acciones (editar/eliminar). CRUD completo con imagen drag & drop
2. **Galería**: grid de imágenes con overlay de editar/eliminar. Subida con drag & drop
3. **Horarios**: tabla con día, hora inicio, hora fin, activo. CRUD completo. Seed: 12 franjas
4. **Clientes**: tabla de solo lectura (nombre, email, teléfono, servicio, fecha, folio). Se llena con cada booking
5. **Reseñas**: tabla con nombre, texto, rating, activo, orden. CRUD completo. Se muestran en carrusel frontend
6. **FAQ**: tabla con pregunta, respuesta, activo, orden. CRUD completo. Se muestran en acordeón frontend
7. **Configuración**: URL del API + botón Confirmar, cambio de contraseña, gestión de usuarios (máx 3)

### Usuarios (en Config)
- Almacenados en sheet `Usuarios` del backend
- CRUD: username + password, username único
- Máximo 3 usuarios
- Los passwords también funcionan para login admin

## Google Apps Script — Arquitectura

### Autenticación
- **Login local**: validación en frontend (hardcoded `wolfbarber`/`wolfbarber2026`)
- **Login API**: `requireAdmin()` verifica contra `Config.admin_password` Y contra sheet `Usuarios`
- Toda acción POST admin requiere `password` en el payload

### Endpoints vía doPost(e) — 22 acciones

| action | Auth | Descripción |
|--------|------|-------------|
| `login` | No | Verifica password (seed data si vacío) |
| `booking` | No | Crea evento Calendar + email + guarda cliente |
| `cancel` | No | Cancela cita por folio (POST) |
| `getServices` | Sí | Todos los servicios |
| `saveService` | Sí | Crea/actualiza servicio |
| `deleteService` | Sí | Elimina servicio |
| `getGallery` | Sí | Toda la galería |
| `saveGalleryItem` | Sí | Crea/actualiza item galería |
| `deleteGalleryItem` | Sí | Elimina item galería |
| `uploadImage` | Sí | Sube imagen a Drive (max 10MB) |
| `changePassword` | Sí | Cambia password en Config |
| `getSchedule` | Sí | Todos los horarios |
| `saveHorario` | Sí | Crea/actualiza horario |
| `deleteHorario` | Sí | Elimina horario |
| `getClients` | Sí | Todos los clientes |
| `getReviews` | Sí | Todas las reseñas |
| `saveReview` | Sí | Crea/actualiza reseña |
| `deleteReview` | Sí | Elimina reseña |
| `getFAQ` | Sí | Todas las FAQ |
| `saveFAQ` | Sí | Crea/actualiza FAQ |
| `deleteFAQ` | Sí | Elimina FAQ |
| `getUsers` | Sí | Todos los usuarios |
| `saveUser` | Sí | Crea/actualiza usuario (máx 3) |
| `deleteUser` | Sí | Elimina usuario |
| `seedData` | Sí | Pobla datos iniciales |

### Endpoints vía doGet(e) — públicos

| Parámetros | Descripción |
|------------|-------------|
| `?action=services` | Servicios activos ordenados |
| `?action=gallery` | Galería activa |
| `?action=config` | Config pública (WhatsApp) |
| `?action=schedule` | Horarios activos por día |
| `?action=reviews` | Reseñas activas ordenadas |
| `?action=faq` | FAQ activas ordenadas |
| `?date=YYYY-MM-DD` | Slots ocupados en Calendar |

### Spreadsheet estructura (8 sheets)

| Sheet | Columnas |
|-------|----------|
| **Servicios** | id, nombre, descripcion, precio, duracion, imagen_url, activo, orden |
| **Galeria** | id, url, categoria, orden, activo |
| **Config** | clave, valor |
| **Horarios** | id, dia, hora_inicio, hora_fin, activo |
| **Clientes** | id, nombre, email, telefono, servicio, fecha, hora, folio, created_at |
| **Resenas** | id, nombre, texto, rating, fecha, activo, orden |
| **FAQ** | id, pregunta, respuesta, orden, activo |
| **Usuarios** | id, username, password, created_at |

### Drive para imágenes
- Carpeta "Wolf Barber CMS" (se crea si no existe)
- Subcarpetas: `servicios/` y `galeria/`
- URL pública: `https://lh3.googleusercontent.com/d/FILE_ID`

## Hero — Diseño text-based con animación

**Decisión clave**: el hero NO usa el logo como centro visual. En su lugar:
- Gradiente `from-black/70 via-black/10 to-black/80`
- Animación escalonada:
  - "Isaac Torres": fade-up 80px + blur 4px (0.2s delay)
  - "ᛟ WOLF BARBER ᛟ": fade-up 60px (0.7s)
  - Línea dorada: slide-in desde left, 200px width (1.3s)
  - "Est. 2020": fade-up 40px (1.8s)
- Indicador "Desliza" + expand_more animado

## Renderizado dinámico

`fetchSiteData()` se llama al cargar la página y carga:
1. Servicios → `renderServices()` + `renderBookingServices()`
2. Galería → `renderGalleryItems()` con filtros + paginación (4/page)
3. Config → actualiza números de WhatsApp
4. **Reviews** → `renderReviews()` con carrusel (auto-play 5s, touch)
5. **FAQ** → `renderFAQ()` con acordeón (solo uno abierto)

## Configuración para Isaac

### Desplegar Google Apps Script
1. Abrir https://script.google.com → Nuevo proyecto
2. Pegar `Code.gs` completo
3. Configurar Script Properties: `SPREADSHEET_ID`, `CALENDAR_ID`, `NOTIFY_EMAIL`
4. Guardar → Implementar → Nueva implementación → Aplicación web
5. Ejecutar como: **"Yo"** / Acceso: **"Cualquiera"**
6. Copiar URL → guardarla (se usará en el admin panel)
7. Ejecutar `probarNotificacion()` para verificar email
8. Ejecutar `handleSeedData()` para poblar datos iniciales

### Desplegar frontend en Vercel
```bash
git add -A
git commit -m "feat: descripción del cambio"
git push
```
Vercel deploya automáticamente desde GitHub.

### Uso del admin
1. Abrir `https://isaactorres.vercel.app/admin.html`
2. Usuario: `wolfbarber` / Contraseña: `wolfbarber2026`
3. Ir a Configuración → pegar URL del GAS → Confirmar
4. Gestionar servicios, galería, horarios, reseñas, FAQ, usuarios

## localStorage keys
- `wb_bookings`: citas agendadas localmente (fallback offline)
- `wb_api_url`: URL del GAS guardada (se lee desde script.js Y admin.js)
- `wb_admin`: (DEPRECATED) ya no se usa

## Notas importantes
- El frontend es 100% estático (Vercel), sin build step
- No hay marquee/carrusel de imágenes en la página (el carrusel es de textos/reseñas)
- Los slots de tiempo consideran la duración del servicio (ocupan múltiples slots de 30 min)
- El botón "CANCELAR CITA" está en la navbar, a la derecha del botón AGENDAR
- Todos los catch blocks de GAS usan `'Error interno del servidor'` — sin stack traces
- No hay `console.log` en producción
- Los horarios default son: Lun/Mie/Jue/Vie/Sáb 8-10 y 22-00; Mar 8-17; Dom inactivo
- Los cambios en admin no requieren redespliegue — el frontend consume datos dinámicos

## Acceso al admin
- **Footer**: Link directo `[ Admin ]` en el pie de página (abre en nueva pestaña)
- **URL directa**: `/admin.html`
- **Login**: usuario `wolfbarber`, contraseña `wolfbarber2026`

## Imágenes desde Google Drive
El backend sube imágenes a Drive y las sirve mediante:
```
https://lh3.googleusercontent.com/d/FILE_ID
```
Este formato usa el CDN de Google, no requiere autenticación. No usar `uc?export=download` ni `thumbnail`.
