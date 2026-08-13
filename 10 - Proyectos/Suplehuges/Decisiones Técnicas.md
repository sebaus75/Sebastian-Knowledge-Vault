---
created: 2026-08-12
updated: 2026-08-12
tags: [suplehuges, decisiones, arquitectura]
---

# Suplehuges — Decisiones Técnicas

> Registro de decisiones con contexto (ADR ligero). Más reciente primero.

| Fecha | Decisión | Contexto |
|---|---|---|
| 2026-08-12 | **Migración TOTAL fuera de Shopify** (no complemento) | Catálogo, pedidos, pagos y contenido propios; Shopify solo de referencia mientras viva la tienda actual |
| 2026-08-12 | **Dominios de producción nunca en commits** | Regla dura: valores reales solo en `demo-v2/js/config.local.js` y `scripts/.env` (gitignored); repo con placeholders genéricos |
| 2026-08-12 | **Infraestructura $0/mes** | Supabase (free) + Vercel (free); argumento clave de venta para el dueño |
| 2026-08-12 | **Pagos múltiples** | Mercado Pago + PayPal + Apple/Google Pay + tarjeta + SPEI + OXXO |
| 2026-08-12 | **Panel admin noir multiusuario** | Login por roles (Santiago decide accesos); estilo Suplehuges Noir (F1) |
| 2026-08-12 | **RLS desde el día 1** | Catálogo de lectura pública; escrituras solo autenticadas (panel) |
| 2026-08-08 | **Dirección visual "Suplehuges Noir"** | Gym-poster / drop culture; tokens en `DESIGN.md` del repo |
| 2026-08-06 | **4 fases por $29,000 MXN** | F0 incluida como garantía de calidad; detalle en [[10 - Proyectos/Suplehuges/Propuesta - Fases y Costos]] |

## Pendientes de decisión

- [ ] Proveedor de checkout principal: Mercado Pago vs PayPal (F2).
- [ ] Unificación del flujo "Entrega Inmediata" vs "Por Llegar" en pedidos (F2).

## Enlaces
- [[10 - Proyectos/Suplehuges/Suplehuges]] · [[10 - Proyectos/Suplehuges/Arquitectura]] · [[10 - Proyectos/Suplehuges/Deployment]]
