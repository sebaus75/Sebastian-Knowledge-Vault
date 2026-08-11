---
proyecto: "Isaac Torres - Wolf Barber"
fase: "produccion"
actualizado: 2026-08-10
estado: Activo
tags: [proyecto, status, barberia]
---

# STATUS — Isaac Torres · Wolf Barber

## Fase actual

`produccion` — Landing premium + booking + admin CMS vivos en https://isaactorres.vercel.app. Mantenimiento y entrega al propietario.

## Hecho (más reciente primero)

- [2026-07-24] Sitio completo en producción: catálogo dinámico, galería con filtros, booking vía Google Calendar, panel admin CMS, notificaciones email (Guia para Isaac operativa).
- [2026-07-24] Auditoría de seguridad julio 2026 — vulnerabilidades corregidas (ver [[10 - Proyectos/Isaac Torres - Wolf Barber/Seguridad - Auditoria]]).
- [2026-07-24] 9 ADR documentados — incluye ADR-003b (cancelación GET → POST), ADR-005/006/007 (auth admin) (ver [[10 - Proyectos/Isaac Torres - Wolf Barber/Decisiones Técnicas]]).
- [2026-07-24] Backend GAS desplegado: 8 sheets + Google Calendar + MailApp.

## En progreso

- [ ] Cambiar contraseña default `wolfbarber2026` después del primer login (Guia para Isaac, paso 3).
- [ ] Agregar a Isaac como miembro del proyecto en Vercel (tabla de responsabilidades).

## Bloqueado / Pendiente

- [ ] Prueba end-to-end pendiente de validar con Isaac: booking → folio → WhatsApp → Calendar → correo → cancelación (Guia para Isaac, paso 4).
- [ ] Dominio propio (hoy `isaactorres.vercel.app`).
- [ ] NOTIFY_EMAIL apunta a `sebastianurbiola75@gmail.com` — confirmar destino definitivo de notificaciones.

## Decisiones recientes

- [2026-07-24] Auth: login local (usuario+pass) + respaldo en sheet Usuarios; password nunca persistida en el navegador (ADR-005/006/007).
- [2026-07-24] Backend: Google Apps Script + Sheets + Calendar, costo cero (ADR-002).

## Próxima sesión

- Entregar manual a Isaac y ejecutar la prueba end-to-end (Guia para Isaac, pasos 2-4); acordar cambio de contraseña y dominio.

---
_Actualizar al final de cada sesión. Ver `AGENTS.md` (protocolo) y `90 - Sistema/Registros/`._
