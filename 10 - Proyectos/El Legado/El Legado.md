---
estado: Activo
fase: en-desarrollo
created: 2026-08-19
updated: 2026-08-19
tags: [proyecto/activo, barberia, landing, html, booking, admin]
---
# El Legado

> Landing premium de barbería "El Legado Barbería" (Querétaro) con 4 sucursales: Jardines, Mirador, Sonterra y Arcos. Taller completo en `Proyectos Open Code/El Legado/`: landing + booking + panel admin + backend GAS. Modo portafolio.

**Estado vivo**: [[10 - Proyectos/El Legado/STATUS]] — fase, pendientes y próxima sesión.
**URL**: https://el-legado-barberia.vercel.app
**Estado**: En producción (portafolio)
**Código fuente**: `../Proyectos Open Code/El Legado/` (`index.html`, `admin.html`, `assets/`, `backend/`)

---

## Map of Content

- [[10 - Proyectos/El Legado/STATUS|STATUS]] — estado operativo

---

## Estado actual (documentado 2026-08-19)

| Aspecto | Detalle |
|---------|---------|
| Tipo | Landing estática + JS (booking 4 pasos + cancelación por folio) |
| Estética | Barbershop clásica-premium: carbón (#1A1208), cobre (#C47A45), dorado (#B8892A), crema |
| Tipografías | Playfair Display, Inter, Bebas Neue (Google Fonts) |
| Sucursales | 4: Jardines, Mirador, Sonterra, Arcos (WhatsApp reales) |
| Tagline | "La moda pasa, el legado permanece" |
| Backend/hosting | Vercel (estático) — en producción; backend opcional Google Apps Script (`backend/Code.gs`) |
| Datos | Derechos de sucursales en stock; precios: cortes $245–$325, barba $280–$325, packs $495–$795 |
| Administración | Panel `admin.html` (login `admin`/`legado2026`, 7 tabs) |
| Verificación | E2E 31/31 PASS · Lighthouse Perf 94 / SEO 100 / A11y 95 / BP 100 |

## Pendientes del proyecto

- [ ] Conectar backend GAS real (desplegar `Code.gs` + crear sheet + `el_legado_api`).
- [ ] Cambiar password del admin (`legado2026`) antes de cualquier uso real.
- [ ] Validar con el dueño (si algún día deja de ser portafolio): fotografías reales de las 4 sucursales.