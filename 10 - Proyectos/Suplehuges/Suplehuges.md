---
estado: Activo
fase: propuesta-comercial
created: 2026-08-06
updated: 2026-08-12
tags: [proyecto/activo, ecommerce, shopify, ventas, queretaro]
---
# Suplehuges - Overview

> Tienda online de ropa deportiva premium en Querétaro. Revendedor autorizado de YoungLA, Gymshark, Darc Sport, Controlled Insanity, Breathe Divinity, DFYNE y Devant. Opera sobre Shopify con modelo mixto de stock local ("Entrega Inmediata") y preventa/importación ("Por Llegar").

**Estado vivo**: [[10 - Proyectos/Suplehuges/STATUS]] — fase, pendientes y próxima sesión.

**URL**: https://www.suplehuges.mx
**Instagram**: @suplehuges (pendiente verificar handle real — devolvió 404 en scrape)
**Estado**: Propuesta lista (06/ago/2026); F0 de migración técnica en marcha (12/ago/2026)
**Stack**: Shopify (actual) → Supabase + Vercel (objetivo, migración total)
**Documentos entregables**: `../../Proyectos Open Code/SupleHuges/` (Propuesta + Guion .docx)

---

## Map of Content

- [[10 - Proyectos/Suplehuges/Auditoria - Diagnostico|Auditoría — Diagnóstico]] — Fortalezas, dolores y oportunidades detectadas
- [[10 - Proyectos/Suplehuges/Propuesta - Fases y Costos|Propuesta — Fases y Costos]] — Plan comercial por fases y precios
- [[10 - Proyectos/Suplehuges/Guion de Venta|Guion de Venta]] — Guion de presentación para la llamada con el dueño
- [[10 - Proyectos/Suplehuges/Demo - Prototipo|Demo — Prototipo]] — Demo interactiva del estado futuro (4 vistas)
- [[10 - Proyectos/Suplehuges/Arquitectura|Arquitectura]] — Stack objetivo: demo-v2 + Supabase + Vercel
- [[10 - Proyectos/Suplehuges/Decisiones Técnicas|Decisiones Técnicas]] — Registro ADR (migración total, $0/mes, regla dura de dominios)
- [[10 - Proyectos/Suplehuges/Deployment|Deployment]] — Runbook F0, Vercel y rollback
- [[10 - Proyectos/Suplehuges/Seguridad - Auditoria|Seguridad — Auditoría]] — RLS, secretos y checklist pre-entrega

---

## Estado actual

| Aspecto | Detalle |
|---------|---------|
| Plataforma | Shopify (tienda funcional completa) |
| Modelo | Stock local (Entrega Inmediata) + preventa/importación (hasta 30 días hábiles) |
| Precios | $450–$1,900 MXN por prenda |
| Promos | Envío gratis (con inconsistencia: +$999 vs +$2,000) · Código SUPLE10 (10%) |
| Contacto | santiagomndz219@gmail.com · +52 442 615 5693 |
| Dirección | Cumbres del Ajusco, Cumbres del Cimatario, Querétaro, MX |
| Dueño | Santiago (amigo de toda la vida de Sebastián — trato preferente de precios) |

## Notas Relacionadas
- [[Home]] · [[VAULT.md]]

## Pendientes
- [x] Demo interactiva construida (04 vistas) — ver [[10 - Proyectos/Suplehuges/Demo - Prototipo]]
- [x] Demo v2 rediseñada con Google Stitch (MCP) — integrada y verificada (08/ago/2026)
- [x] Revisión visual de la demo (MiMo-V2.5: 7.5/10, lista con reservas; reservas aplicadas)
- [x] Rediseño v2 "Suplehuges Noir" (gym-poster/drop culture) + 5 rondas MiMo — ver [[10 - Proyectos/Suplehuges/Demo - Prototipo]]
- [ ] Completar F0 con credenciales reales (proyecto Supabase + runbook `.qa/migracion.md`)
- [ ] F1: panel admin noir (`demo-v2/admin/`) — login multiusuario, productos/inventario, contenido
- [ ] Revisión visual humana final de Sebastián (`demo-v2/shots/*_s*.png` — segmentos reales 390x844)
- [ ] Confirmar handle real del Instagram de Suplehuges
- [ ] Definir línea base de métricas (ventas, tráfico) antes de arrancar
- [ ] Entregar propuesta + guion al dueño y agendar llamada
- [ ] Desplegar demo-v2 a Vercel (link por WhatsApp)

## Enlaces
- https://www.suplehuges.mx
- https://www.instagram.com/suplehuges/
