---
tags: [arquitectura, frontend, backend, estructura]
created: 2026-07-25
---
# Arquitectura

## Stack Tecnológico

| Componente | Tecnología |
|---|---|
| Frontend | HTML5, CSS3, JavaScript vanilla (ES6 modules vía IIFE) |
| Estilos | Tailwind CSS (CDN runtime) + `assets/css/style.css` |
| Iconos | Tabler Icons (CDN) |
| Backend | Google Apps Script (GAS) como Web App |
| Base de datos | Google Sheets |
| Hosting | Vercel (static) |
| Fuentes | Fontshare (Cabinet Grotesk, Satoshi, Inter) |
| PWA | Service Worker + manifest.json |

## Flujo de datos

```
[Usuario] → [Vercel CDN] → [index.html + CSS + JS]
                              ↓ (fetch)
                    [Google Apps Script Web App]
                     ↓
              [Google Sheets]
```

## Endpoints del API (GAS)

| Ruta | Método | Uso |
|---|---|---|
| `?action=getServices` | GET | Servicios públicos (público) |
| `?action=getGallery` | GET | Galería pública (público) |
| `?action=getReviews` | GET | Reseñas activas (público) |
| `?action=getFAQ` | GET | FAQ activas (público) |
| `?action=getConfig` | GET | Config pública (WhatsApp, horarios) |
| `?action=getCsrf` | GET | Token CSRF (público) |
| `POST /` | POST | Contacto, booking, newsletter (público) |
| `POST /` + auth | POST | CRUD admin (autenticado) |

## Estructura de archivos

```
Proyectos Open Code/TemplateTest/
├── index.html              # Landing page (267 líneas, shell + 10 secciones)
├── admin.html              # Panel admin (337 líneas, 12 pestañas)
├── 404.html                # Página 404 con themed visual
├── config.json             # Contenido del negocio (servicios, galería, reseñas, FAQ, horarios, i18n)
├── theme.json              # Branding (4 temas, colores, fuentes, contacto, SEO)
├── manifest.json           # PWA manifest
├── robots.txt              # SEO crawlers
├── sitemap.xml             # SEO sitemap
├── sw.js                   # Service Worker (caché de estáticos)
├── vercel.json             # Config deploy + security headers
├── .gitignore
│
├── assets/
│   ├── css/
│   │   └── style.css       # 419 líneas — todos los estilos (landing + admin + responsive)
│   └── js/
│       ├── pubsub.js        # Event Bus pub/sub (40 líneas)
│       ├── utils.js         # Utilidades: DOM, fetch, toast, format, crypto (111 líneas)
│       ├── validator.js     # Schema validation engine (90 líneas)
│       ├── security.js      # SHA-256 × 1000, RateLimiter, CSRF, XSS sanitize (136 líneas)
│       ├── i18n.js          # Internacionalización es/en (50 líneas)
│       ├── gas.js           # Cliente GAS API con timeout + retry (61 líneas)
│       ├── theme.js         # Motor de 4 temas + dark/light toggle (127 líneas)
│       ├── gallery.js       # Galería con drag & drop + lazy loading + lightbox (178 líneas)
│       ├── booking.js       # Booking 5 pasos con buffer + profesionales (289 líneas)
│       ├── app.js           # Controlador landing + wizard de primer uso (406 líneas)
│       └── admin.js         # Admin: 12 pestañas, CRUD, editor tema, CSV (829 líneas)
│
└── gas/
    ├── Code.gs              # Backend GAS: CRUD, auth, rate limit, emails (150 líneas)
    └── config.gs            # Config de despliegue GAS (60 líneas)
```

## Arquitectura de módulos JS

Los módulos se comunican mediante un Event Bus centralizado (`pubsub.js`):

```
Bus.emit / Bus.on
  ↑
  ├── theme.js    → theme:applied, theme:changed
  ├── i18n.js     → locale:change
  ├── gallery.js  → gallery:reorder
  ├── booking.js  → booking:confirmed, booking:error
  ├── gas.js      → gas:success, gas:error
  └── admin.js    → admin:login, admin:logout, admin:saved
```

## Principios de diseño

1. **Zero dependencias externas** (solo Tailwind CDN + Tabler Icons)
2. **Sin build step** — deploy directo a Vercel
3. **Datos locales primero** (`localStorage`), GAS como backend opcional
4. **Render dinámico** — el HTML de la landing se genera desde `theme.json` + `config.json`
5. **Temas en tiempo real** — cambio de tema en admin → landing sin recargar
