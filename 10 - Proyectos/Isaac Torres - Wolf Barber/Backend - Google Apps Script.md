---
tags: [backend, gas, security]
---
# Backend — Google Apps Script

**Archivo**: `Code.gs` (~830 líneas)
**URL despliegue**: configurable via `localStorage` (admin panel → Config)

## Sheets

| Sheet | Headers |
|---|---|
| `Servicios` | id, nombre, descripcion, precio, duracion, imagen_url, activo, orden |
| `Galeria` | id, url, categoria, orden, activo |
| `Config` | clave, valor |
| `Horarios` | id, dia, hora_inicio, hora_fin, activo |
| `Clientes` | id, nombre, email, telefono, servicio, fecha, hora, folio, created_at |
| `Resenas` | id, nombre, texto, rating, fecha, activo, orden |
| `FAQ` | id, pregunta, respuesta, orden, activo |
| `Usuarios` | id, username, password, created_at |

## Funciones principales

### Públicas (sin auth, vía doGet)
| Función | Descripción |
|---|---|
| `getServicesPublic()` | Servicios con activo=TRUE, ordenados |
| `getGalleryPublic()` | Galería con activo=TRUE, ordenada |
| `getSiteConfig()` | Config pública (WhatsApp) |
| `getHorariosPublicos()` | Horarios activos agrupados por día |
| `getResenasPublicas()` | Reseñas activas ordenadas |
| `getFAQPublica()` | FAQ activas ordenadas |
| `getOccupiedSlots(date)` | Slots ocupados del calendario para una fecha |
| `createBooking(data)` | Crea cita en Calendar + notifica email + guarda cliente |

### Admin (requieren password, vía doPost)
| Función | Descripción |
|---|---|
| `handleGetServices()` | Todos los servicios (incl. inactivos) |
| `handleSaveService(data)` | Crear/editar servicio |
| `handleDeleteService(data)` | Eliminar servicio |
| `handleGetGallery()` | Toda la galería |
| `handleSaveGalleryItem(data)` | Crear/editar item de galería |
| `handleDeleteGalleryItem(data)` | Eliminar item |
| `handleUploadImage(data)` | Subir imagen a Drive (max 10MB) |
| `handleChangePassword(data)` | Cambiar password admin |
| `handleGetUsers()` | Listar usuarios |
| `handleSaveUser(data)` | Crear/editar usuario (máx 3) |
| `handleDeleteUser(data)` | Eliminar usuario |
| `handleGetReviews()` | Todas las reseñas |
| `handleSaveResena(data)` | Crear/editar reseña |
| `handleDeleteResena(data)` | Eliminar reseña |
| `handleGetFAQ()` | Todas las FAQ |
| `handleSaveFAQ(data)` | Crear/editar FAQ |
| `handleDeleteFAQ(data)` | Eliminar FAQ |
| `handleGetSchedule()` | Todos los horarios |
| `handleSaveHorario(data)` | Crear/editar horario |
| `handleDeleteHorario(data)` | Eliminar horario |
| `handleGetClients()` | Listar clientes registrados |
| `handleSeedData()` | Poblar datos iniciales completos |

### Seguridad incorporada
- Login local (usuario+pass hardcoded) + respaldo en sheet Usuarios
- Rate limiting: 30 req/min via PropertiesService
- Stack traces ocultos (error messages genéricos)
- Cancelación solo vía POST (no GET)
- Validación server-side imágenes 10MB
- Folio uniqueness en generateId()
- Sin console.log en frontend
- [[Isaac Torres - Wolf Barber/Seguridad - Auditoria|Ver auditoría completa]]

## Propiedades del Spreadsheet

**ID**: `1hDT2DbwYv0vh_ZLSb__KNdpA4c6X7ud6-7fgzYraw74`

## Script Properties (GAS)

Configurar en: *Editor de Apps Script → Project Settings → Script Properties*

| Propiedad | Valor | Obligatorio |
|---|---|---|
| `SPREADSHEET_ID` | ID del spreadsheet | Sí (fallback a hardcoded) |
| `CALENDAR_ID` | `primary` o ID específico | Sí |
| `NOTIFY_EMAIL` | Correo para notificaciones | Sí |

## Seed data

Al ejecutar `handleSeedData()`:
- 6 servicios de ejemplo
- Password default: `wolfbarber2026`
- WhatsApp config: `+5214423216396`
- Calendar ID: `primary`
- 12 franjas horarias default
- 4 reseñas de ejemplo
- 5 FAQ de ejemplo
- 1 usuario default: `wolfbarber` / `wolfbarber2026`
