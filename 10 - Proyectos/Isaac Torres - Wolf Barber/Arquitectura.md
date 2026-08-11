---
tags: [arquitectura, backend, frontend]
created: 2026-07-24
---
# Arquitectura

## Stack Tecnológico

| Componente | Tecnología |
|---|---|
| Frontend | HTML5, CSS3, JavaScript vanilla |
| Estilos | Tailwind CSS (CDN runtime) + `css/style.css` |
| Backend | Google Apps Script (GAS) |
| Base de datos | Google Sheets (8 sheets) |
| Calendario | Google Calendar API |
| Hosting | Vercel (static) |
| Fuentes | Google Fonts (Cinzel, DM Sans, Material Symbols) |

## Flujo de datos

```
[Usuario] → [Vercel CDN] → [index.html + CSS + JS]
                              ↓ (fetch GET/POST)
                    [Google Apps Script Web App]
              ↓
    ┌─────────────────┼─────────────────┐
     [Sheets: 8 total]  [Google Calendar]  [Drive: Imágenes]
     (Servicios, Galeria, Config, Horarios,
      Clientes, Resenas, FAQ, Usuarios)
```

## Endpoints del API

| Ruta | Método | Uso |
|---|---|---|
| `?action=services` | GET | Servicios públicos activos (público) |
| `?action=gallery` | GET | Galería pública activa (público) |
| `?action=config` | GET | Configuración pública (WhatsApp) |
| `?action=schedule` | GET | Horarios activos por día (público) |
| `?action=reviews` | GET | Reseñas activas ordenadas (público) |
| `?action=faq` | GET | FAQ activas ordenadas (público) |
| `?date=YYYY-MM-DD` | GET | Slots ocupados del calendario (público) |
| `POST /` | POST | Booking + acciones admin (autenticado vía password) |

## Acciones admin (POST)

| `action` | Función |
|---|---|
| `login` | Verifica password contra Config o sheet Usuarios |
| `booking` | Crea evento Calendar + email + guarda cliente |
| `getServices` / `saveService` / `deleteService` | CRUD servicios |
| `getGallery` / `saveGalleryItem` / `deleteGalleryItem` | CRUD galería |
| `uploadImage` | Sube imagen a Drive |
| `changePassword` | Cambia password admin (Config sheet) |
| `getSchedule` / `saveHorario` / `deleteHorario` | CRUD horarios |
| `getClients` | Lista clientes |
| `getReviews` / `saveReview` / `deleteReview` | CRUD reseñas |
| `getFAQ` / `saveFAQ` / `deleteFAQ` | CRUD FAQ |
| `getUsers` / `saveUser` / `deleteUser` | CRUD usuarios (máx 3) |
| `cancel` | Cancela cita por folio (POST) |
| `seedData` | Pobla datos iniciales |

## Estructura de archivos

```
Proyectos Open Code/IsaacTorres/
├── index.html          # Landing page
├── admin.html          # Panel CMS
├── css/
│   ├── style.css       # Estilos personalizados
│   └── admin.css       # Estilos del panel admin
├── js/
│   ├── script.js       # Lógica frontend
│   └── admin.js        # Lógica del admin
├── Code.gs             # Backend GAS
├── vercel.json         # Config Vercel
├── _serve.js           # Servidor local (puerto 8080)
├── opencode.json       # Config OpenCode CLI
└── robots.txt          # SEO
```

## Diagrama de booking

```
1. Usuario abre modal → selecciona servicio
2. Elige fecha → fetch GET /?action=schedule para slots disponibles
3. Slots ocupados se consultan vía GET /?date= para Calendar
4. Ingresa datos personales (nombre, teléfono, email)
5. Resumen → confirmación → POST / con action=booking
6. GAS: crea evento Calendar + envía email notificación + guarda en Clientes
7. Cliente: redirige a WhatsApp con mensaje pre-llenado
```
