---
tags: [adr, arquitectura, decisiones]
---
# Decisiones Técnicas

> Architecture Decision Records (ADR) del proyecto. Cada entrada documenta una decisión significativa, su contexto y sus consecuencias.

---

## ADR-001: Tailwind CDN runtime vs build

**Contexto**: Necesitábamos estilos utility-first sin agregar paso de build al deploy.

**Decisión**: Usar Tailwind CSS vía CDN runtime con `tailwind.config` inline en `<script>`.

**Consecuencias**:
- + Zero build step, deploy instantáneo
- + Configuración de colores y tipografía 100% controlada desde HTML
- - ~200ms extra de carga inicial (CDN + parseo del config)
- - No purge de CSS no usado

---

## ADR-002: Google Apps Script como backend

**Contexto**: Sin servidor propio ni presupuesto para backend. Necesitábamos persistencia + calendario + email.

**Decisión**: Google Apps Script como Web App con Google Sheets de BD y Google Calendar para agenda.

**Consecuencias**:
- + Costo cero (dentro del tier gratis de Google)
- + Spreadsheet como BD editable visualmente
- + Calendar API nativa
- + Notificaciones email sin configuración extra
- - Límite de 6 min de ejecución por trigger
- - ~1-2s de latencia en cada llamada (cold start)
- - No transacciones reales ni rollbacks

---

## ADR-003: Booking vía GET público

**Contexto inicial**: El booking GET era simple, rápido de implementar y Google Calendar lo soportaba.

**Decisión posterior (ADR-003b)**: Mover cancelación de GET a POST por seguridad. Ver [[Isaac Torres - Wolf Barber/Seguridad - Auditoria]].

**Razón**: GET exponía folios en logs y permitía CSRF básico. POST requiere body JSON y no es encadenable por `<img>` o `<script>`.

---

## ADR-004: Sin framework JS

**Contexto**: Sitio estático con interactividad moderada (modal, galería, fetch API).

**Decisión**: JavaScript vanilla sin React, Vue ni similares.

**Consecuencias**:
- + Zero dependencias, bundle mínimo
- + Carga instantánea (no runtime framework)
- - Organización manual del código (IIFEs + globales para onclick)
- - Menos ergonómico para estado complejo

---

## ADR-005: Sesión admin en memoria vs storage

**Contexto**: El panel admin necesita mantener autenticación durante la sesión.

**Decisión**: Password solo en variable JS (`AUTH_PASSWORD`), sin sessionStorage. URL del API se persiste en localStorage.

**Consecuencias**:
- + No hay password persistente en el navegador
- + Al cerrar pestaña, la sesión expira
- - Usuario debe re-ingresar password al recargar la página

---

## ADR-006: Login admin local + URL en Config

**Contexto**: El login requería URL del API + password, pero la URL solo se obtenía del admin → dependencia circular.

**Decisión**: Login validado **localmente** (usuario `wolfbarber` + pass `wolfbarber2026`). La URL del API se configura después del login en Config.

**Consecuencias**:
- + Rompe dependencia circular (login sin URL)
- + Banner amarillo guía al usuario si falta URL
- - Password hardcoded en JS (mitigado: solo lectura, no editable desde UI)

---

## ADR-007: Usuarios en sheet como múltiples credenciales

**Contexto**: Necesitábamos hasta 3 usuarios con diferentes credenciales para el panel admin.

**Decisión**: Sheet `Usuarios` con CRUD via API. `requireAdmin()` verifica tanto Config como sheet.

**Consecuencias**:
- + Hasta 3 usuarios gestionables desde Config
- + Login también acepta credenciales de la sheet
- + Seed automático de `wolfbarber` / `wolfbarber2026`
- - No hay roles ni permisos diferenciados (todos son admin)

---

## ADR-008: Hero animation con CSS keyframes

**Contexto**: El hero se sentía estático al cargar la página.

**Decisión**: Animación escalonada con `@keyframes` CSS: fade-up + blur + slide-line. Sin JavaScript.

**Consecuencias**:
- + Sin JS extra, cero dependencias
- + Rendimiento nativo (GPU composited)
- + Stagger natural con `animation-delay`
- - No funciona en navegadores muy antiguos (cae graceful)

---

## ADR-009: Reseñas carrusel + FAQ acordeón con fetch dinámico

**Contexto**: Se necesitaban secciones de testimonios y preguntas frecuentes gestionables desde admin.

**Decisión**: Sheets `Resenas` y `FAQ` con endpoints públicos GET. Renderizado JS en frontend. Admin CRUD completo.

**Consecuencias**:
- + Contenido 100% gestionable desde admin
- + Mismo patrón que servicios/galería (consistente)
- + Carrusel con auto-play 5s + touch support
- + Acordeón con solo un item abierto a la vez
- - Contenido no visible sin conexión a API (fallback a ocultar sección)
