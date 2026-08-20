---
proyecto: "Suplehuges"
fase: "propuesta-comercial"
actualizado: 2026-08-19
estado: Activo
tags: [proyecto, status, ecommerce]
---

# STATUS — Suplehuges

## Fase actual

`propuesta-comercial` — Propuesta lista, demo en nivel de venta; F0 de migración (fuera de Shopify) commiteada. Falta: entregar propuesta a Santiago, agendar llamada y cerrar la venta.

## Hecho (más reciente primero)

- [2026-08-12] **S5 — F0 migración fuera de Shopify** (`2641d32`): Supabase + Vercel, repo sin dominios reales (config-driven + gitignored), `schema.sql` 7 tablas + RLS, seed/fetch imágenes, stubs webhooks, runbook `.qa/migracion.md`. Verificado + visual aprobado por dueño (marquee NO es prueba). Detalle: [[10 - Proyectos/Suplehuges/Arquitectura]] y [[10 - Proyectos/Suplehuges/Deployment]].
- [2026-08-12] S4 (pulido pedido/drops/producto, `e9c3ff4`) + S2/S3 prototipo 1/1.1 (tienda, hero, POR QUÉ SUPLEHUGES) — audit 0 issues. Ver [[10 - Proyectos/Suplehuges/Demo - Prototipo]].
- [2026-08-06] Propuesta formal aprobada: 4 fases por $29,000 — [[10 - Proyectos/Suplehuges/Propuesta - Fases y Costos]] · Auditoría + guion: [[10 - Proyectos/Suplehuges/Auditoria - Diagnostico]] · [[10 - Proyectos/Suplehuges/Guion de Venta]].

## En progreso

- [ ] Completar F0 con credenciales reales (runbook `.qa/migracion.md`).
- [ ] F1: panel admin noir (`demo-v2/admin/`) — login, productos/inventario, contenido.
- [ ] Revisión visual humana final (`demo-v2/shots/`).

## Bloqueado / Pendiente

- [ ] Proyecto Supabase del cliente (sin credenciales no cargan imágenes ni se verifican shots).
- [ ] Entregar propuesta + guion al dueño y agendar llamada (objetivo de la fase).
- [ ] Confirmar handle real de Instagram + línea base de métricas.

## Decisiones recientes

- [2026-08-12] **Migración TOTAL fuera de Shopify**: Supabase + Vercel, infra $0/mes, pagos múltiples (Mercado Pago, PayPal, wallets, SPEI, OXXO).
- [2026-08-12] Regla dura: nunca commitear dominios reales (solo `config.local.js`/`scripts/.env`, gitignored).
- [2026-08-08] Dirección visual: Suplehuges Noir (gym-poster / drop culture).
- [2026-08-06] Precio cerrado 4 fases: $29,000, F0 incluida.

## Próxima sesión

1. Crear proyecto Supabase y ejecutar runbook F0 (`.qa/migracion.md`).
2. Verificar shots vs baseline + deploy demo-v2 a Vercel.
3. F1 panel admin; mostrar demo a Santiago y agendar llamada.

---
_Actualizar al final de cada sesión. Ver `AGENTS.md` (protocolo) y `90 - Sistema/Registros/`._