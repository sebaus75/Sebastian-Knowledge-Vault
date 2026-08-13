---
created: 2026-08-12
updated: 2026-08-12
tags: [suplehuges, seguridad, auditoria]
---

# Suplehuges — Seguridad y Auditoría

> Postura de seguridad del proyecto. Última revisión: 12/ago/2026 (F0).

## Reglas vigentes

- **Nunca commitear secretos ni dominios reales**: solo viven en `demo-v2/js/config.local.js` y `scripts/.env` (gitignored). Antes de cada commit: `git status` + grep de `suplehuges`/`cdn.shopify`.
- **RLS activado desde el schema**: catálogo legible para todos (anon), escrituras solo autenticadas.
- **Webhooks (F2)**: validar firma de Mercado Pago (X-Signature) y PayPal (webhook verify) antes de mutar pedidos.
- **Panel admin (F1)**: login con Supabase Auth, roles por usuario, nunca credenciales en el frontend.

## Checklist de auditoría (pre-entrega)

- [ ] Grep de dominios reales en el árbol commit = 0 coincidencias
- [ ] `audit.cjs` 0 issues con config real cargada
- [ ] RLS verificado (anon no puede escribir; service key nunca expuesta)
- [ ] Storage: buckets públicos solo donde aplique (catálogo) y privados el resto
- [ ] Backup de `config.local.js`/`scripts/.env` fuera del repo
- [ ] Respaldo semanal de la vault (GitHub) — pendiente global

## Historial de hallazgos

- 2026-08-12: F0 terminada sin secretos en commits; 0 coincidencias de dominio real en `demo-v2/`, `scripts/`, `supabase/`, `.qa/` (salvo el texto de la regla en AGENTS.md y la tool legacy `scripts/merge_stitch.cjs`, fuera del runtime).

## Enlaces
- [[10 - Proyectos/Suplehuges/Suplehuges]] · [[10 - Proyectos/Suplehuges/Arquitectura]] · [[10 - Proyectos/Suplehuges/Deployment]]
