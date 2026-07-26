---
estado: Activo
created: 2026-07-25
tags: [proyecto/activo, frontend, template, comercial, gas]
---
# TemplateTest

> Template landing page + admin panel de nivel comercial ($30k+). 4 temas visuales, booking multi-paso, galería drag & drop, i18n, seguridad, backend GAS. Producto genérico adaptable a cualquier nicho de negocio.

**URL**: https://templatetest.vercel.app (pendiente deploy)
**Estado**: Desarrollo completado — listo para empaquetar
**Stack**: HTML5 + Tailwind CDN + Vanilla JS ES6 modules | Google Apps Script | Google Sheets | Vercel
**Código fuente**: `../Proyectos Open Code/TemplateTest/`
**Precio objetivo**: $30k+

---

## Map of Content

### Sistema
- [[TemplateTest/Arquitectura|Arquitectura]] — Stack, flujo, estructura de archivos
- [[TemplateTest/Backend - Google Apps Script|Backend — Google Apps Script]] — Code.gs, endpoints, seguridad server-side
- [[TemplateTest/Frontend|Frontend]] — index.html, 8 módulos JS, style.css
- [[TemplateTest/Admin Panel|Admin Panel]] — admin.html, admin.js, 12 pestañas CRUD

### Operaciones
- [[TemplateTest/Deployment|Deployment]] — Vercel + GAS, configuración one-click
- [[TemplateTest/Guía para Usuario|Guía para Usuario]] — Manual del comprador

### Registro
- [[TemplateTest/Seguridad - Auditoria|Seguridad — Auditoría]] — Controles implementados
- [[TemplateTest/Decisiones Técnicas|Decisiones Técnicas]] — ADR del proyecto

### Producto
- [[TemplateTest/Brand y Producto|Brand y Producto]] — Propuesta de valor, mercado, pricing

---

## Estado actual

| Aspecto | Detalle |
|---------|---------|
| Hosting | Vercel (estático) |
| Backend | Google Apps Script desplegado como Web App |
| BD | Google Sheets |
| Temas visuales | 4 (dark, light, minimal, bold) + dark/light mode toggle |
| i18n | es/en desde admin |
| Booking | 5 pasos, buffer 15 min, múltiples profesionales |
| Seguridad | SHA-256 × 1000 iteraciones, rate limiting, CSRF, CSP, audit log |
| Galería | Drag & drop reorder, lazy loading, lightbox |
| Admin CRUD | Servicios, galería, reseñas, FAQ, profesionales, horarios, clientes, bookings |
| Última auditoría | Julio 2026 — ver [[TemplateTest/Seguridad - Auditoria]] |

## Historial de desarrollo

| Ronda | Alcance | Archivos |
|-------|---------|----------|
| R1 — Base inicial | Landing + admin + booking + GAS | 15 archivos, ~130 KB |
| R2 — Nivel comercial | 4 temas, seguridad, i18n, galería, wizard, SEO | 27 archivos, ~31 KB de código |
| R3 — Bugfixes + data | Corregir 6 bugs críticos, poblar datos barbería | Ediciones quirúrgicas en 17 archivos |
| R4 — Security hardening | SHA-256 iterado, CSRF fuerte, rate limiting server-side, CSP | Ediciones en 8 archivos + .gitignore |

## Contacto proyecto

- **WhatsApp**: +52 1 555 000 0000
- **Email**: hola@minegocio.com
- **Dirección**: Av. Principal 123, Ciudad de México
