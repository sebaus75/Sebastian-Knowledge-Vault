---
estado: Activo
fase: produccion
created: 2026-07-24
updated: 2026-08-10
tags: [proyecto/activo, frontend, barberia, gas]
---
# Isaac Torres — Wolf Barber

> Landing page premium para barbería de alta gama con temática vikinga. Catálogo dinámico, galería con filtros, booking vía Google Calendar, panel admin CMS y notificaciones por correo.

**Estado vivo**: [[10 - Proyectos/Isaac Torres - Wolf Barber/STATUS]] — fase, pendientes y próxima sesión.

**URL**: https://isaactorres.vercel.app
**Estado**: Producción activa
**Stack**: HTML + CSS + JS vanilla | Tailwind CSS (CDN) | Google Apps Script | Google Sheets | Google Calendar | Vercel
**Código fuente**: `../Proyectos Open Code/IsaacTorres/`

---

## Map of Content

### Sistema
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Arquitectura|Arquitectura]] — Stack, flujo, endpoints
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Backend - Google Apps Script|Backend — Google Apps Script]] — Code.gs, sheets, seguridad
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Frontend|Frontend]] — index.html, script.js, style.css
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Admin Panel|Admin Panel]] — admin.html, js/admin.js

### Operaciones
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Deployment|Deployment]] — Vercel + GAS, configuración
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Guia para Isaac|Guía para Isaac]] — Manual del propietario

### Registro
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Seguridad - Auditoria|Seguridad — Auditoría]] — Vulnerabilidades corregidas
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Decisiones Técnicas|Decisiones Técnicas]] — ADR del proyecto

### Producto
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Brand y Producto|Brand y Producto]] — Identidad, diseño, audiencia

---

## Estado actual

| Aspecto | Detalle |
|---------|---------|
| Hosting | Vercel (estático) |
| Backend | Google Apps Script desplegado como Web App |
| BD | Google Sheets (8 sheets) |
| Calendario | Google Calendar (primary) |
| Notificaciones | Email vía MailApp |
| Auth admin | Login local (usuario+pass) + respaldo en sheet Usuarios |
| Dominio | isaactorres.vercel.app |
| Última auditoría | Julio 2026 — ver [[10 - Proyectos/Isaac Torres - Wolf Barber/Seguridad - Auditoria]] |

## Contacto proyecto

- **Email**: isaactorreswolfbarber@gmail.com
- **WhatsApp**: +52 1 442 321 6396
- **Dirección**: Lima 35, Capital Sur, Querétaro, México
