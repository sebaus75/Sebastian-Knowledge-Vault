---
proyecto: "Suplehuges"
fase: "propuesta-comercial"
actualizado: 2026-08-12
estado: Activo
tags: [proyecto, status, ecommerce]
---

# STATUS — Suplehuges

## Fase actual

`propuesta-comercial` — Propuesta lista y demo en nivel de venta; F0 de migración técnica (fuera de Shopify) ya commiteada. Falta: entregar propuesta a Santiago, agendar llamada y cerrar la venta.

## Hecho (más reciente primero)

- [2026-08-12] **S5 — F0 migración fuera de Shopify** (commit `2641d32`): repo sin dominios reales (config-driven + gitignored), `supabase/schema.sql` (7 tablas + RLS), seed/fetch de imágenes, stubs webhooks, runbook `.qa/migracion.md`. Verificado: funcional OK; imágenes esperan credenciales (estado intermedio).
- [2026-08-12] **S5 visual**: botones 3D hard-shadow, footer/bottom-nav/FAB globales; **marquee de anuncio APROBADO por el dueño** (ya no es PRUEBA). Audit 0 issues, shots OK, 4 revisiones MiMo OK.
- [2026-08-12] S4: pulido pedido/drops/producto (timeline fijo, self-link carrito, video hero pausado) — commit `e9c3ff4`.
- [2026-08-09] S2+S3: Prototipo 1 (`01dd061`) y 1.1 (`9639da9`): tienda chips/favoritos/producto, hero nuevo, POR QUÉ SUPLEHUGES, audit 0 issues.
- [2026-08-06] Propuesta formal aprobada: 4 fases por $29,000 — ver [[10 - Proyectos/Suplehuges/Propuesta - Fases y Costos]].
- [2026-08-06] Auditoría diagnóstica + guion de venta listos — ver [[10 - Proyectos/Suplehuges/Auditoria - Diagnostico]] y [[10 - Proyectos/Suplehuges/Guion de Venta]].

## En progreso

- [ ] Completar F0 con credenciales reales (runbook `.qa/migracion.md` del repo).
- [ ] F1: panel admin noir (`demo-v2/admin/`) — login multiusuario, productos/inventario, contenido.
- [ ] Revisión visual humana final de Sebastián (`demo-v2/shots/`).

## Bloqueado / Pendiente

- [ ] Proyecto Supabase del cliente (sin credenciales no cargan imágenes ni se verifican shots visuales).
- [ ] Entregar propuesta + guion al dueño y agendar llamada (objetivo de la fase).
- [ ] Confirmar handle real de Instagram (@suplehuges devolvió 404).
- [ ] Línea base de métricas (ventas, tráfico) antes de arrancar F0.

## Decisiones recientes

- [2026-08-12] **Migración TOTAL fuera de Shopify** (no complemento): Supabase + Vercel, infra $0/mes, pagos múltiples (Mercado Pago, PayPal, Apple/Google Pay, SPEI, OXXO).
- [2026-08-12] Regla dura: **nunca commitear dominios reales** (solo en `config.local.js`/`scripts/.env`, gitignored).
- [2026-08-08] Dirección visual demo: Suplehuges Noir (gym-poster / drop culture).
- [2026-08-06] Precio cerrado por 4 fases juntas: $29,000, con F0 incluida como garantía de calidad.

## Próxima sesión

1. Crear proyecto Supabase y ejecutar runbook F0 (`.qa/migracion.md`).
2. Verificar shots vs baseline + deploy demo-v2 a Vercel.
3. F1 panel admin; mostrar demo a Santiago y agendar llamada.

---
_Actualizar al final de cada sesión. Ver `AGENTS.md` (protocolo) y `90 - Sistema/Registros/`._
