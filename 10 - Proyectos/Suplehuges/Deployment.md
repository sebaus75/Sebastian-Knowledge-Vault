---
created: 2026-08-12
updated: 2026-08-12
tags: [suplehuges, deployment, vercel]
---

# Suplehuges — Deployment

## Local

- `node scripts/serve.cjs` → http://localhost:8123/demo-v2/
- Verificación: `audit.cjs`, `func_check.cjs`, `shot_check.cjs` (playwright en `C:\Users\sebas\AppData\Local\Temp\opencode\pw\`)

## Producción (Vercel)

- Repo: `../../Proyectos Open Code/SupleHuges/` · **Root Directory: `demo-v2`**
- Funciones serverless: `demo-v2/api/*.cjs` (webhooks; stubs pendientes F2)
- Sin config real, la demo funciona con catálogo embebido e imágenes apagadas (estado intermedio esperado)

## Runbook F0 (resumen — detalle en `.qa/migracion.md` del repo)

1. Crear proyecto Supabase (plan free)
2. Ejecutar `supabase/schema.sql` en el SQL Editor
3. Llenar `demo-v2/js/config.local.js` (SUPABASE_URL, SUPABASE_ANON_KEY, IMG_BASE, VIDEO_BASE)
4. Llenar `scripts/.env` (SUPABASE_URL, SUPABASE_SERVICE_KEY, IMG_SRC_BASE)
5. `node scripts/seed_catalog.cjs` → 23 productos a la DB
6. `node scripts/fetch_images.cjs` → bucket `productos`
7. Subir los 2 mp4 del hero al bucket `videos`
8. Verificar shots vs baseline → deploy a Vercel

## Rollback

- Visual: `git checkout 01dd061 -- demo-v2` (Prototipo 1)
- Infra: borrando los archivos gitignored el repo vuelve a ser 100% genérico

## Enlaces
- [[10 - Proyectos/Suplehuges/Suplehuges]] · [[10 - Proyectos/Suplehuges/Arquitectura]] · [[10 - Proyectos/Suplehuges/Seguridad - Auditoria]]
