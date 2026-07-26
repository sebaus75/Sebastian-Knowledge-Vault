---
estado: Activo
created: 2025-07-24
tags: [proyecto/activo, frontend, barberia, gas]
---
# Isaac Torres — Wolf Barber

> Landing page premium para barbería de alta gama con temática vikinga. Catálogo dinámico, galería con filtros, booking vía Google Calendar, panel admin CMS y notificaciones por correo.

**URL**: https://isaactorres.vercel.app
**Estado**: Producción activa
**Stack**: HTML + CSS + JS vanilla | Tailwind CSS (CDN) | Google Apps Script | Google Sheets | Google Calendar | Vercel
**Código fuente**: `../Proyectos Open Code/IsaacTorres/`

---

## Map of Content

### Sistema
- [[Isaac Torres - Wolf Barber/Arquitectura|Arquitectura]] — Stack, flujo, endpoints
- [[Isaac Torres - Wolf Barber/Backend - Google Apps Script|Backend — Google Apps Script]] — Code.gs, sheets, seguridad
- [[Isaac Torres - Wolf Barber/Frontend|Frontend]] — index.html, script.js, style.css
- [[Isaac Torres - Wolf Barber/Admin Panel|Admin Panel]] — admin.html, js/admin.js

### Operaciones
- [[Isaac Torres - Wolf Barber/Deployment|Deployment]] — Vercel + GAS, configuración
- [[Isaac Torres - Wolf Barber/Guia para Isaac|Guía para Isaac]] — Manual del propietario

### Registro
- [[Isaac Torres - Wolf Barber/Seguridad - Auditoria|Seguridad — Auditoría]] — Vulnerabilidades corregidas
- [[Isaac Torres - Wolf Barber/Decisiones Técnicas|Decisiones Técnicas]] — ADR del proyecto

### Producto
- [[Isaac Torres - Wolf Barber/Brand y Producto|Brand y Producto]] — Identidad, diseño, audiencia

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
| Última auditoría | Julio 2026 — ver [[Isaac Torres - Wolf Barber/Seguridad - Auditoria]] |

## Contacto proyecto

- **Email**: isaactorreswolfbarber@gmail.com
- **WhatsApp**: +52 1 442 321 6396
- **Dirección**: Lima 35, Capital Sur, Querétaro, México
