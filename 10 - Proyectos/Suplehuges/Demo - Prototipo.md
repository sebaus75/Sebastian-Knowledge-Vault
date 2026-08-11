---
estado: Activo
created: 2026-08-06
updated: 2026-08-09
tags: [suplehuges, demo, prototipo, ventas, stitch]
---
# Suplehuges — Demo Interactiva (Prototipo)

> Prototipo navegable del "estado futuro" de la tienda para la presentación de venta con Santiago. Muestra las Fases 0–2 aplicadas: barra de ofertas unificada, WhatsApp flotante, guía de tallas, reseñas con foto, insignias Entrega Inmediata/Por Llegar, tracking de preventa y drops con wishlist + alertas.

## Versión actual: demo-v2 v2 — "Suplehuges Noir" (08/ago/2026)

**Ubicación**: `../../Proyectos Open Code/SupleHuges/demo-v2/`
**Archivos**: `index.html` (69 KB, 4 vistas) + `js/app.js` (7 KB) — HTML generado por **Google Stitch** (MCP) con Tailwind CDN, integrado por `scripts/merge_stitch.cjs` (reproducible: `node scripts/merge_stitch.cjs`).
**Servidor**: `node scripts/serve.cjs` (root = proyecto) → `http://localhost:8123/demo-v2/` (la v1 vanilla sigue en `/demo/` para comparar)

### Dirección aprobada (register: brand)
- **Evolucionar "Performance Noir"** (proyecto Stitch `13819334863633442428` = "Suplehuges Redesigned Homepage", la referencia desktop) hacia un lane propio **gym-poster / cultura drop**, aplicado a las 4 vistas móviles, con WCAG 2.1 AA.
- `PRODUCT.md` y `DESIGN.md` en la raíz del repo — spec completa **"Suplehuges Noir"**: Anton (display) / Barlow Condensed 600-700 (headings/labels/CTAs) / Sora (body); Power Red `#E11D2E` (evoluciona de `#C8102E`), success `#3ED660`, amber `#EE9441`; negro puro `#000`, surfaces `#0E0E0E/#161616/#1C1C1C/#242424`, muted `#A6A6AC`; esquinas sharp 0px; sección gap 96px; marquee ticker; countdown; stock bars; grain.
- Design system en Stitch: `assets/1037769942626643743` (proyecto demo "Suplehuges - Demo v2 (Stitch)" `17470664732876903681`).
- Impeccable skill actualizado a v4.0.4.

### Las 4 vistas (regeneradas con GEMINI_3_1_PRO + designSystem Noir)

| Ruta | Contenido | Fase que vende |
|---|---|---|
| `#/home` | Marquee, header, **hero video real + headline ENTRENA./VISTE./DOMINA.**, trust strip, HOMBRE (4 productos reales CDN), drop banner con **countdown en vivo (30 AGO · 8:00 PM)** + fecha visible, newsletter, footer | F0 |
| `#/producto` | Devant Seamless T-Shirt Black: galería + 4 thumbs reales, **pills de talla interactivas** (click→selección), CTA h-16 "AGREGAR AL CARRITO" + "COMPRAR AHORA", specs, reseñas con foto, WhatsApp | F0/F1 |
| `#/pedido` | Pedido #SH-1042: timeline 4 pasos (Pagado → En aduana → **En tránsito ACTUAL** → Listo) + rastreo ESTAFETA `1Z8A2A94-QRO` + toggle WhatsApp funcional + mockup de chat | F1 |
| `#/drops` | Countdown card grande (blanco+glow, 64px), 4 drop cards con stock "SÓLO QUEDAN", sin pagos adelantados | F2 |

### Integración (`scripts/merge_stitch.cjs`)
- Imágenes placeholder de Stitch → **CDN real de suplehuges.mx** (0 aida restantes, verificado).
- Hero: video oficial del sitio + poster modelo + overlay `from-black via-black/50 to-black/10` + text-shadow doble en headline (legibilidad AA sobre video).
- Nav inferior **unificada 4 tabs** (INICIO/DROPS/PEDIDOS/PERFIL) en todas las vistas, tab activo por ruta.
- `data-cd-unit` (countdown en vivo vía app.js, deadline 30 ago 2026 20:00), `data-size-pill`/`data-size-group`, `data-wa-toggle` (persistencia localStorage), chip "Prototipo" dismissible (click).
- `fixWhatsAppIcons` con path canónico; WA número corregido `5244266155693`; links `#/...` mapeados.
- CSS scoped por vista: drops countdown 64px blanco, pills 56px (target táctil), línea timeline `#3A3A3A`, badge ACTUAL 12px.

## Versión anterior: demo-v1 (vanilla, respaldada en git)

**Ubicación**: `../../Proyectos Open Code/SupleHuges/demo/` — `index.html` + `css/style.css` + `js/app.js`, cero dependencias. Se conserva para comparación A/B y como fallback.

## Verificación realizada (08/ago/2026)

- `node scripts/merge_stitch.cjs` → OK (0 aida restantes, HTML balanceado 155/155 divs)
- `scripts/verify_routes.cjs`: las 4 rutas muestran SOLO su vista (hidden correcto) — verificado en Chrome headless
- **Metodología de screenshots corregida**: captura por segmentos con viewport real 390x844 vía CDP (`Page.captureScreenshot`, DPR 2) en `demo-v2/shots/{view}_s{0..2}.png` — los full-page de 9000px rompían las unidades `vh` (hero de 7650px de negro, artefactos)
- **5 rondas de revisión visual MiMo-V2.5** sobre segmentos reales. Correcciones aplicadas: overlay hero + text-shadow, countdown drops blanco/glow 64px, pills talla 56px interactivas, timeline pedido aireado, nav unificada, chip prototipo reubicado+dismissible, fecha del drop visible en móvil, título producto 28px móvil, ENTREGA HOY con fondo, countdown en vivo real
- **Veredicto final MiMo**: "Listo para mostrar — el demo transmite calidad, urgencia y confianza sin necesidad de explicaciones"

## Notas de uso en la venta

- Abrir en móvil (lo que verá Santiago) — mobile-first. Recorrido ideal: `#/home` → card → `#/producto` (tallas + reseñas) → `#/pedido` (timeline + rastreo) → `#/drops` (countdown + stock).
- Banner "PROTOTIPO — Vista propuesta" dismissible (click).
- Demo-v2 está en local; si se quiere link para WhatsApp, desplegar demo-v2 a Vercel (pendiente, descartado por ahora).
- Nota: la vista producto llega vía cards de home/`#/producto` (no está en la nav).

## Pendientes
- [ ] Revisión visual humana final del usuario sobre `demo-v2/shots/*_s*.png`
- [ ] Decidir despliegue a Vercel (link por WhatsApp)
- [x] Revisión visual → hecho con MiMo 08/ago/2026 (5 rondas, veredicto final OK)

## Enlaces
- [[10 - Proyectos/Suplehuges/Suplehuges]] · [[10 - Proyectos/Suplehuges/Propuesta - Fases y Costos]] · [[10 - Proyectos/Suplehuges/Guion de Venta]] · [[10 - Proyectos/Suplehuges/Auditoria - Diagnostico]]
