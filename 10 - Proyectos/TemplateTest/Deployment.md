---
tags: [deployment, devops, vercel, gas, setup]
created: 2026-07-25
---
# Deployment

## Hosting: Vercel

**Tipo**: Static site (sin server)
**Deploy**: push a GitHub → Vercel detecta y depliega automáticamente

### vercel.json
Incluye:
- Rutas para todos los archivos estáticos
- Cache headers: 1 año inmutable para assets, no-cache para sw.js
- Security headers: X-Content-Type-Options, X-Frame-Options DENY, Referrer-Policy, Permissions-Policy

### Deploy one-click
```
git init
git add .
git commit -m "Initial deploy"
git remote add origin <tu-repo>
git push -u origin main
```
Vercel importa desde GitHub automáticamente.

## Backend: Google Apps Script

### Despliegue inicial
1. Ir a https://script.google.com
2. Crear nuevo proyecto
3. Copiar `gas/Code.gs` y `gas/config.gs` al editor
4. Ejecutar `setupConfig()` para establecer valores por defecto
5. Desplegar → *Aplicación web*
   - Ejecutar como: tu cuenta de Google
   - Acceso: *Cualquiera (público anónimo)*
6. Copiar URL generada

### Configurar Script Properties (opcional)
En *Project Settings → Script Properties*:

| Propiedad | Valor | Propósito |
|---|---|---|
| `SHEET_NAME` | `TemplateTest` | Nombre del spreadsheet a crear/usar |
| `ADMIN_HASH` | (auto) | Hash SHA-256 de la contraseña admin |
| `NOTIFY_EMAIL` | (opcional) | Email para notificaciones de booking |

### Conectar frontend con backend
1. Entrar a `https://tusitio.vercel.app/admin.html`
2. Ir a pestaña *Config*
3. Pegar URL del Web App GAS en el campo correspondiente
4. Guardar

## Desarrollo local
```
npx serve . -p 3000
# Landing: http://localhost:3000
# Admin:   http://localhost:3000/admin.html
```
Login admin por defecto: `admin123`

## Post-deploy checklist
- [ ] Landing carga sin errores en consola
- [ ] Admin login funciona
- [ ] URL de GAS configurada en admin Config
- [ ] Al menos un servicio, galería y reseña creados desde admin
- [ ] Booking modal completa el flujo
- [ ] Dark/light mode toggle funcional
- [ ] Responsive en 375px, 768px, 1440px
- [ ] 404.html personalizado se despliega
- [ ] CSV export descarga archivo válido
