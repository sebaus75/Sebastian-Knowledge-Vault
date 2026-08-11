---
tags: [backend, gas, google-apps-script, api]
created: 2026-07-25
---
# Backend — Google Apps Script

**Archivo**: `gas/Code.gs` (~150 líneas) + `gas/config.gs` (~60 líneas)

Backend serverless gratuito dentro del ecosistema Google. Se despliega como Web App y se comunica vía HTTP POST/GET con el frontend.

## Endpoints públicos (GET)

| Ruta | Devuelve |
|---|---|
| `?action=getServices` | Servicios activos con precio, duración, imagen |
| `?action=getGallery` | Items de galería activos ordenados |
| `?action=getReviews` | Reseñas activas con rating |
| `?action=getFAQ` | FAQ activas ordenadas |
| `?action=getConfig` | Config pública (WhatsApp, horarios, profesionales, feriados) |
| `?action=getCsrf` | Token CSRF de 64 chars hex |

## Endpoints autenticados (POST)

Requieren `admin` + `password` + `csrf` válidos en el body:

| `action` | Función |
|---|---|
| `login` | Verifica hash SHA-256 contra ScriptProperties |
| `saveService` / `deleteService` | CRUD servicios |
| `saveGalleryItem` / `deleteGalleryItem` / `reorderGallery` | CRUD galería |
| `saveReview` / `deleteReview` | CRUD reseñas |
| `saveFAQ` / `deleteFAQ` | CRUD FAQ |
| `saveProfessional` / `deleteProfessional` | CRUD profesionales |
| `saveSchedule` / `deleteSchedule` | CRUD horarios |
| `getClients` / `getBookings` | Consulta clientes y citas |
| `saveConfig` | Guarda configuración general |
| `exportCSV` | Exporta datos a CSV |
| `getAuditLogs` / `clearAuditLogs` | Gestión de auditoría |

## Seguridad server-side

| Control | Implementación |
|---|---|
| **Rate limiting** | 5 intentos de login por IP en 15 min (CacheService), 30 requests/min para demás endpoints |
| **CSRF validation** | Token almacenado en ScriptProperties, validado contra el enviado en cada POST |
| **Autenticación** | SHA-256 hash contra hash almacenado en ScriptProperties |
| **Sanitización** | Escape de `'` para Sheets injection, validación de tipos en todos los campos |
| **Audit logging** | Cada acción admin se registra con timestamp + IP + acción |
| **Error handling** | Errores genéricos al cliente (sin stack traces) |
| **Sheet auto-creation** | Sheets se crean automáticamente con headers si no existen |

## Sheets creadas automáticamente

| Sheet | Headers |
|---|---|
| `Servicios` | id, nombre, descripcion, precio, duracion, imagen, activo, orden |
| `Galeria` | id, titulo, src, orden |
| `Resenas` | id, nombre, texto, rating, activo, orden |
| `FAQ` | id, pregunta, respuesta, activo, orden |
| `Profesionales` | id, nombre, especialidad, bio, avatar, activo, orden |
| `Horarios` | id, dia, apertura, cierre, activo |
| `Clientes` | id, nombre, email, telefono, servicio, profesional, fecha, hora, estado |
| `AuditLog` | timestamp, accion, detalle, ip |

## Config.gs

Configuración inicial del proyecto GAS. Incluye:
- `setupConfig()` — establece valores por defecto en ScriptProperties
- `generateHash()` — SHA-256 via `Utilities.computeDigest`
- `getConfig()` / `setConfig()` — acceso a ScriptProperties
