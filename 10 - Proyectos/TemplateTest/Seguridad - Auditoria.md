---
tags: [seguridad, auditoria, backend, frontend, hardening]
created: 2026-07-25
---
# Seguridad — Auditoría

**Fecha**: Julio 2026
**Scope**: Código fuente completo (frontend + backend GAS)

## Resumen

Auditoría de seguridad integral realizada en 2 rondas (R3 + R4). Se corrigieron 6 bugs críticos, se implementaron 8 controles de seguridad y se hizo hardening de 3 vectores de ataque. Sin impacto visual en la página.

---

## Bugs corregidos

### 🔴 Crítico: removeLS no importado en admin.js
**Archivo**: `assets/js/admin.js:10`
**Problema**: `removeLS('admin_logged_in')` en logout lanzaba `ReferenceError` porque `removeLS` no estaba en el destructuring de `Utils`.
**Fix**: Agregado al destructuring: `const { $, $$, create, loadJSON, toast, saveLS, loadLS, removeLS, escapeHTML } = Utils;`

### 🔴 Crítico: renderAudit inaccesible desde onclick
**Archivo**: `admin.html:305` + `admin.js:339`
**Problema**: Botón "Limpiar" en audit logs llamaba `renderAudit()` que era función privada del IIFE, no accesible desde inline onclick.
**Fix**: Exportada como `Admin.renderAudit()` y actualizado el onclick.

### 🔴 Crítico: Wizard pierde datos al recargar
**Archivo**: `assets/js/app.js:19-20`
**Problema**: El wizard de primer uso guardaba en localStorage key `wizard_data` pero nunca lo leía al cargar la página.
**Fix**: En la carga de `config.json`, hacer merge con `wizard_data` de localStorage si existe.

### 🔴 Crítico: JSON-LD hardcodeado
**Archivo**: `index.html` (antes) → `assets/js/app.js:105-131` (después)
**Problema**: JSON-LD LocalBusiness tenía "Mi Negocio", "+1-555-000-0000" y "hola@minegocio.com" fijos, sin importar la configuración del admin.
**Fix**: JSON-LD movido a `app.js` como función `renderJSONLD()` que usa datos de `theme.json` + `config.json` en tiempo real.

### 🟡 Alto: Brand name mismatch
**Archivo**: `index.html` (6 lugares)
**Problema**: El title, meta description, og:title y og:site_name decían "Mi Negocio", mientras que `config.json` y `theme.json` usaban "Corte & Estilo".
**Fix**: Unificado a "Corte & Estilo" en todos los meta tags estáticos. Los dinámicos toman del theme.

### 🟡 Alto: SW cacheaba index.html como fallback 404
**Archivo**: `sw.js:34`
**Problema**: En navegación offline, el Service Worker servía `index.html` en lugar de `404.html` para páginas no encontradas.
**Fix**: Cambiado `caches.match('/index.html')` → `caches.match('/404.html')`.

---

## Controles de seguridad implementados

### SHA-256 encadenado × 1000 iteraciones
`security.js:5-8` — En lugar de SHA-256 directo, se encadena 1000 veces para hacer brute-force más costoso. Idéntico en cliente y servidor.

### CSRF con crypto.getRandomValues(32)
`security.js:30-48` — Token de 64 caracteres hex generado con criptografía verdaderamente aleatoria. Server-side valida contra ScriptProperties.

### Rate limiting server-side (GAS)
`Code.gs:12-18,53-56` — 5 intentos de login por IP en 15 minutos (CacheService). 30 requests/minuto para demás endpoints. Sin posibilidad de spoofeo vía `_ip` parameter (eliminado).

### CSP con nonce
`index.html:19` — Content Security Policy configurada. Nonce generado por JS para scripts inline. Documentada la recomendación de nonce server-side para producción crítica.

### Sanitización server-side
`Code.gs` — Escape de comillas simples (`'` → `''`) para Sheets injection prevention. Validación de tipos en todos los campos.

### Audit logging
`Code.gs` + `security.js` — Cada acción admin (login, CRUD, cambios de configuración) se registra con timestamp, acción, detalle y userAgent tanto en frontend como en backend.

### OG Image fallback
`app.js:150-158` — Si `og:image` está vacío, se genera un canvas inline con el nombre del negocio como fallback para preview en redes sociales.

### Hardening de errores
`app.js:13` — Error toast visible si falla la carga de config.json. Sin stacks expuestos al usuario.

---

## Limitaciones conocidas (por stack)

| Limitación | Motivo | Mitigación |
|---|---|---|
| CSP sin `'unsafe-inline'` total | Requiere build tooling con server-side nonces | Nonce generado por JS; documentado upgrade path |
| bcrypt/Argon2 no disponibles | GAS no tiene这些算法 | SHA-256 × 1000 iteraciones |
| CSRF no es infalible | Single-page app sin server-rendered tokens | Token 64 hex chars + validación server-side |
| Rate limit client-side bypasseable | localStorage es borrable | Rate limit server-side real en GAS |

## Estado actual

| Control | Estado |
|---|---|
| removeLS importado | ✅ |
| renderAudit exportado | ✅ |
| Wizard data persistente | ✅ |
| JSON-LD dinámico | ✅ |
| Brand name unificado | ✅ |
| SW fallback 404 | ✅ |
| SHA-256 × 1000 iteraciones | ✅ |
| CSRF 64 chars crypto | ✅ |
| Rate limit server-side | ✅ (5 login/15min, 30 general/min) |
| CSP con nonce | ✅ |
| Sanitización server-side | ✅ |
| Audit log | ✅ |
| OG Image fallback | ✅ |
| Manejo de errores | ✅ |
