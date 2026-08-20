---
proyecto: "El Legado"
fase: "en-desarrollo"
actualizado: 2026-08-19
estado: Activo
tags: [proyecto, status, barberia]
---

# STATUS — El Legado

## Fase actual

`en-desarrollo` — Landing + producto completo construidos, verificados y **en producción** (2026-08-19). Alcance C aprobado: pulido + deploy y booking + admin. Modo portafolio (sin cliente real). URL: `https://el-legado-barberia.vercel.app`.

## Hecho (más reciente primero)

- [2026-08-19] **Deploy en producción**: `https://el-legado-barberia.vercel.app` (vercel --prod, alias activo). E2E en producción 31/31 PASS; Lighthouse producción Perf 98 · SEO 100 · A11y 95 · BP 100 (LCP 1.9s).
- [2026-08-19] Producto construido en `Proyectos Open Code/El Legado/`: landing (`index.html`), data layer (`assets/js/store.js`, mock + puente GAS), backend (`backend/Code.gs` + `backend/API.md`), panel admin (`admin.html` + `assets/js/admin.js`), imágenes extraídas/optimizadas y SEO (robots/sitemap/OG/JSON-LD).
- [2026-08-19] Verificación E2E Playwright **31/31 PASS** y Lighthouse Perf 94 · SEO 100 · A11y 95 · BP 100.
- [2026-08-19] Investigación del negocio: 4 sucursales reales con WhatsApp, precios y horarios (IG @barberiaellegado, 4.4K).
- [2026-08-19] Documentación completada: objetivo, stack, estética, sucursales (ver [[10 - Proyectos/El Legado/El Legado]]).
- [2026-08-19] Registro del proyecto en la vault (MOC + STATUS + MANIFEST).

## En progreso

- [ ] Conectar backend GAS real (desplegar `backend/Code.gs` + crear sheet + setear `localStorage.el_legado_api`), si se decide pasar de modo portafolio a producción real.

## Bloqueado / Pendiente

- [ ] Cambiar password del admin (`legado2026`) antes de cualquier uso real.
- [ ] Respaldo de imágenes/videos originales (el HTML base64 original se eliminó; quedan los `.webp` extraídos).

## Decisiones recientes

- [2026-08-19] Alcance C híbrido por fases: pulido + deploy y producto (booking + admin). Portafolio, sin contactar al dueño.
- [2026-08-19] Stack: HTML/CSS/JS vanilla + GAS + Sheets; capa store con mock local (modo portafolio) y puente a GAS.
- [2026-08-19] Admin local: usuario `admin` / password `legado2026` (cambiar en producción).

## Próxima sesión

- Revisar el sitio en producción y decidir si se conecta el backend GAS real (requiere cuenta de Google Apps Script del usuario).
- Respadar imágenes/videos originales (los `.webp` extraídos están en `assets/img/`; los base64 del HTML original se eliminaron).

---
_Actualizar al final de cada sesión. Ver `AGENTS.md` (protocolo) y `90 - Sistema/Registros/`._