---
created: 2026-08-12
updated: 2026-08-12
tags: [suplehuges, arquitectura, supabase]
---

# Suplehuges — Arquitectura

> Objetivo (12/ago/2026): **migración total fuera de Shopify**. Storefront sin backoffice propio; datos y autenticación en Supabase; API serverless en Vercel.

## Componentes

| Capa | Pieza | Detalle |
|---|---|---|
| Storefront | `demo-v2/` SPA vanilla (1 archivo) | Config-driven: `js/config.js` (commiteado, genérico) + `js/config.local.js` (gitignored, real) |
| Catálogo | `FALLBACK_PRODUCTS` embebido (23 productos) | Fallback offline; reemplazado por Supabase cuando hay config real |
| DB | Supabase Postgres | `supabase/schema.sql`: productos, tallas_producto, pedidos, promociones, drops, contenido, usuarios + RLS |
| Auth | Supabase Auth | Login multiusuario para panel admin (F1) |
| Storage | Supabase Storage | Bucket `productos` (imágenes) + `videos` (mp4 del hero) |
| API | `demo-v2/api/*.cjs` (Vercel functions) | Stubs: `mp-webhook.cjs`, `paypal-webhook.cjs` (F2) |

## Flujo de datos

- **Imágenes**: HTML usa centinelas `data-src="assets/img/..."`; `js/config.js` los resuelve a `IMG_BASE`/`VIDEO_BASE` solo con config real (sin config: cero peticiones).
- **Catálogo**: `loadCatalog()` hace fetch a `/rest/v1/productos` si `hasRealConfig`; si no, usa `FALLBACK_PRODUCTS`.
- **Pagos (F2)**: checkout → Mercado Pago/PayPal → webhook → Supabase.

## Documentación en el repo

- Código: `../../Proyectos Open Code/SupleHuges/demo-v2/`
- Runbook F0: `.qa/migracion.md` · Schema: `supabase/schema.sql`
- Contrato de trabajo: `AGENTS.md` del repo (regla dura: nunca commitear dominios reales)

## Enlaces
- [[10 - Proyectos/Suplehuges/Suplehuges]] · [[10 - Proyectos/Suplehuges/Decisiones Técnicas]] · [[10 - Proyectos/Suplehuges/Deployment]] · [[10 - Proyectos/Suplehuges/Seguridad - Auditoria]]
