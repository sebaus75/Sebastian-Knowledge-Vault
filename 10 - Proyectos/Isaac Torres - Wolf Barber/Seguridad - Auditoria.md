---
tags: [seguridad, auditoria, backend, frontend]
---
# Seguridad — Auditoría

**Fecha**: Julio 2026
**Scope**: Código fuente completo (frontend + backend GAS)

## Resumen

Auditoría de seguridad integral. Se corrigieron 7 vulnerabilidades, se agregaron 4 controles de seguridad y 2 correcciones adicionales en iteración posterior. Sin impacto visual en la página.

---

## Vulnerabilidades corregidas

### 🔴 Crítica: Login bypass en primera ejecución
**Archivo**: `Code.gs:adminLogin()`
**Problema**: `if (!stored) return true` — si no había password configurado, aceptaba *cualquier* contraseña.
**Fix**: `if (!stored) return false` — sin password configurado, nadie accede.
**Comportamiento afectado**: Seed data debe ejecutarse manualmente `handleSeedData()` desde el editor GAS.

### 🔴 Crítica: Stack traces expuestos
**Archivo**: `Code.gs` — catch blocks con `e.toString()`
**Problema**: Los errores internos se devolvían al cliente.
**Fix**: Reemplazado por `'Error interno del servidor'` — mensaje genérico. **(Auditado Jul 2026: 0 instancias restantes)**

### 🟡 Alta: Cancelación de citas vía GET
**Archivo**: `doGet()` + `cancelBooking()`
**Problema**: `?action=cancel&folio=X` en GET. Folio en logs, historial y CSRF.
**Fix**: Movido a POST con JSON body.

### 🟡 Alta: Password admin en sessionStorage
**Archivo**: `js/admin.js`
**Problema**: `sessionStorage.setItem('wb_admin', ...)` — password persistía en texto plano.
**Fix**: Password solo en memoria (variable `AUTH_PASSWORD`).

### 🟡 Alta: Auto-login desde storage
**Archivo**: `js/admin.js` — init block
**Problema**: Login automático si password estaba en storage.
**Fix**: Eliminado auto-login.

### 🟡 Media: URL del API hardcodeada
**Archivo**: `js/script.js` — `CALENDAR_WEBAPP_URL`
**Problema**: URL hardcodeada sin fallback.
**Fix**: `getApiUrl()` busca `localStorage` primero, luego fallback hardcoded.

### 🟢 Baja: API key expuesta
**Archivo**: `opencode.json`
**Problema**: API key de Stitch en texto plano.
**Fix**: Eliminado bloque `headers` con API key.

---

## Controles agregados

### Rate limiting (30 req/min)
`Code.gs` — `isRateLimited()` con PropertiesService. Previene abuso del Web App público.

### PropertiesService para configuración
`Code.gs` — `SPREADSHEET_ID`, `CALENDAR_ID`, `NOTIFY_EMAIL` leen de Script Properties primero, con fallback.

### Validación server-side de imágenes
`Code.gs` — `handleUploadImage()` verifica base64 ≤ 10MB antes de crear blob en Drive.

### Folio uniqueness
`Code.gs` — `generateId()` + `isFolioUsed()` verifica contra sheets existentes, reintenta hasta 10 veces.

---

## Correcciones posteriores (Iteración 2 — Jul 2026)

### 🟡 Media: RequireAdmin solo verificaba Config sheet
**Archivo**: `Code.gs:requireAdmin()`
**Problema**: Solo validaba contra `admin_password` de Config, ignorando usuarios en sheet Usuarios.
**Fix**: `requireAdmin()` ahora intenta `adminLogin()` y luego `userLogin()` contra sheet Usuarios.

### 🟢 Baja: error.toString() remanentes
**Archivo**: `Code.gs` — `getOccupiedSlots()` y `cancelBooking()`
**Problema**: 2 catch blocks aún exponían `error.toString()`.
**Fix**: Reemplazados por `'Error interno del servidor'`.

### 🟢 Baja: escapeHtml() faltante en script.js
**Archivo**: `js/script.js` — `renderReviews()` y `renderFAQ()`
**Problema**: Usaban `escapeHtml()` sin tenerla definida → XSS potencial en reseñas y FAQ.
**Fix**: Agregada función `escapeHtml()` en script.js.

---

## Estado actual

| Control | Estado |
|---|---|
| Stack traces ocultos | ✅ 0 instancias de error.toString() |
| Auth por password | ✅ Local + sheet Usuarios |
| Rate limiting | ✅ 30 req/min |
| Validación imágenes | ✅ 10MB server-side |
| Folio uniqueness | ✅ Con reintentos |
| Cancelación solo POST | ✅ |
| Sin console.log en frontend | ✅ |
| Sin API keys en código | ✅ |
| Sesión admin en memoria | ✅ Sin sessionStorage |
| escapeHtml en renders | ✅ Ambos archivos |
