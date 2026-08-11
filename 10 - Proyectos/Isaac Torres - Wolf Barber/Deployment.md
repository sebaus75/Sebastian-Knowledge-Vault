---
tags: [deployment, devops, vercel, gas]
created: 2026-07-24
---
# Deployment

## Hosting: Vercel

**URL**: https://isaactorres.vercel.app
**Proyecto**: `isaactorres`
**Tipo**: Static site (sin server)

| Archivo | Propósito |
|---|---|
| `vercel.json` | Config de deploy |
| `.vercel/project.json` | Config del proyecto Vercel |
| `.vercel/.env.production.local` | Variables de producción |
| `robots.txt` | Crawling SEO |

### Deploy
```
git add .
git commit -m "mensaje"
git push
```
Vercel detecta el push y despliega automáticamente.

## Backend: Google Apps Script

### Despliegue inicial
1. Ir a https://script.google.com
2. Crear proyecto → pegar `Code.gs`
3. Desplegar → *Aplicación web*
   - Ejecutar como: `isaactorreswolfbarber@gmail.com`
   - Acceso: *Cualquiera (público anónimo)*
4. Copiar URL generada

### Configurar Script Properties
En *Project Settings → Script Properties*:
| Propiedad | Valor |
|---|---|
| `SPREADSHEET_ID` | `1hDT2DbwYv0vh_ZLSb__KNdpA4c6X7ud6-7fgzYraw74` |
| `CALENDAR_ID` | `primary` |
| `NOTIFY_EMAIL` | `sebastianurbiola75@gmail.com` |

### Probar
Ejecutar `probarNotificacion()` en el editor GAS. Debe llegar un correo de prueba.

## Desarrollo local
```
node _serve.js    # Puerto 8080
```

## Configuración post-deploy
1. Entrar a `https://isaactorres.vercel.app/admin.html`
2. Ingresar URL del Web App GAS
3. Login con password default `wolfbarber2026`
4. Verificar que servicios y galería carguen
