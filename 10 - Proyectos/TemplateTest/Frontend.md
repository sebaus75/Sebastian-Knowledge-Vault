---
tags: [frontend, html, css, javascript, modulos]
---
# Frontend

## index.html (~267 líneas)

Shell mínima que carga `theme.json` + `config.json` y genera el HTML dinámicamente vía JS. Incluye CSP meta tag, JSON-LD dinámico (generado por `app.js`), preconnect a CDNs y theme FOUC prevention inline.

### Secciones

| Sección | Detalle |
|---|---|
| Announcement Bar | Barra promocional configurable desde config.json |
| Header | Navbar fijo con glassmorphism al scrollear, mobile hamburger menu |
| Hero | Fullscreen con gradiente + animación escalonada de entrada |
| Trusted | Logos de empresas confiables (data placeholder) |
| About | Grid 2 columnas con historia del negocio + stats animados |
| Services | Grid de servicios con imágenes, precio, duración, shimmer hover |
| Gallery | Grid con drag & drop reorder, lazy loading, blur placeholder, lightbox |
| Reviews | Grid de testimonios con rating en estrellas |
| FAQ | Acordeón con pregunta/respuesta (solo un item abierto) |
| Contact | Formulario + WhatsApp + horarios + mapa placeholder |
| CTA | Banner de llamado a la acción |
| Footer | Logo, redes sociales, nav links, créditos |

### Componentes globales
- **Booking Modal** — 5 pasos con indicador de progreso
- **Lightbox** — Navegación por teclado (Escape, flechas) + contador
- **WhatsApp FAB** — Botón flotante animado
- **Mobile Menu** — Overlay slide-in
- **Toast notifications** — Sistema de notificaciones stackeables
- **Skeleton screens** — Loading states con shimmer animation

## Módulos JS (8 archivos, ~1.900 líneas total)

### pubsub.js (40 líneas)
Event Bus con `on`, `off`, `emit`, `once`, `clear`. Usa `Map` + `WeakSet`.

### utils.js (111 líneas)
- DOM helpers: `$()`, `$$()`, `create()` (builder pattern)
- Async: `loadJSON()`, `saveJSON()`
- Timing: `debounce()`, `throttle()`
- Format: `formatDate()`, `formatTime()`, `parseTime()`
- Storage: `saveLS()`, `loadLS()`, `removeLS()`
- Toast system con stack de notificaciones
- HTML sanitization: `escapeHTML()` recursivo

### validator.js (90 líneas)
Schema validation engine con tipos: string, number, boolean, array, object, URL, email, phone, time, date. Soporta validación anidada, min/max, regex, enums.

### security.js (136 líneas)
- `hashPassword()` — SHA-256 encadenado × 1000 iteraciones
- `RateLimiter` — Clase con maxAttempts + lockoutMinutes en localStorage
- `CSRF` — Token de 64 caracteres hex via `crypto.getRandomValues(32)`
- `sanitize()` — XSS sanitization recursiva para objetos
- `auditLog()` — Log con timestamp + acción + userAgent

### i18n.js (50 líneas)
Bilingüe es/en con persistencia en localStorage. Función `t()` con interpolación de variables. Atributos `data-i18n`, `data-i18n-placeholder`, `data-i18n-alt`.

### gas.js (61 líneas)
Cliente GAS con `mode: 'cors'`, `AbortController` timeout de 10s, 1 reintento con 1s de delay, parseo real de respuesta JSON. Emite eventos `gas:success` / `gas:error`.

### theme.js (127 líneas)
Motor de temas: aplica CSS custom properties del tema activo, maneja dark/light/system modes con `matchMedia`, toggle visual, persistencia en localStorage, emite `theme:applied`.

### gallery.js (178 líneas)
Grid con lazy loading (`IntersectionObserver` + fallback), blur placeholder CSS, drag & drop reorder nativo (HTML5 DnD), lightbox con teclado, emite `gallery:reorder`.

### booking.js (289 líneas)
5 pasos: Servicio → Profesional → Fecha (calendario con restricciones) → Horario (slots que respetan buffer 15 min + duración) → Datos → Confirmación WhatsApp. Consciente de días cerrados, feriados, horas pasadas (hoy).

### app.js (406 líneas)
Controlador principal: carga theme.json + config.json, detecta primer uso (wizard 4 pasos: nombre, WhatsApp, email, descripción), renderiza todas las secciones, maneja scroll events, parallax, FAQ accordion, scroll reveal (`IntersectionObserver`), glow effect en mouse move, dark mode toggle, error boundary global.

### admin.js (829 líneas)
Admin SPA en un solo archivo. Ver sección [[TemplateTest/Admin Panel|Admin Panel]].

## style.css (419 líneas)

CSS custom properties para los 17 tokens de color de cada tema. Reset, botones (primary, outline, ghost, accent, sizes), header glassmorphism, hero fullscreen con gradiente + animación, galería con drag states, skeleton shimmer, scroll reveal variants, toast stack, tooltips, glow effects, pseudo-3D parallax, empty states, wizard overlay, dark mode overrides, print stylesheet, `prefers-reduced-motion`, `prefers-contrast`. Breakpoints: 1024px, 768px, 480px.
