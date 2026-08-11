---
tags: [manual, usuario, cliente, onboarding]
created: 2026-07-25
---
# Guía para Usuario

> Manual del propietario para administrar su landing page.

---

## Primeros pasos

1. **Abrir la página**: Ve a `https://tudominio.vercel.app`
2. **Wizard de configuración**: La primera vez aparecerá un asistente de 4 pasos para configurar nombre del negocio, WhatsApp, email y descripción.
3. **Admin panel**: Ve a `https://tudominio.vercel.app/admin.html`
4. **Login**: Usuario: `admin` | Contraseña: `admin123`
5. **Cambiar contraseña**: Ve a la pestaña *Config* → cambia la contraseña por una segura.

---

## Landing page

La página principal se genera automáticamente desde los datos que configures en el admin. Las secciones aparecen/desaparecen según las actives en *Config → Secciones*.

### Secciones disponibles

| Sección | Qué muestra |
|---|---|
| Announcement Bar | Promociones o avisos importantes |
| Hero | Título, subtítulo, botón CTA |
| Trusted | Logos de empresas aliadas |
| About | Historia del negocio + estadísticas |
| Services | Servicios con precio, duración, imagen |
| Gallery | Galería de trabajos (arrastra para reordenar) |
| Reviews | Opiniones de clientes |
| FAQ | Preguntas frecuentes |
| Contact | Formulario + WhatsApp + horario + mapa |
| CTA | Banner promocional final |
| Footer | Redes sociales, nav, créditos |

---

## Admin panel

### Pestañas principales

| Pestaña | Qué puedes hacer |
|---|---|
| **Dashboard** | Resumen visual del negocio |
| **Servicios** | Agregar, editar, eliminar servicios. Cada servicio tiene: nombre, descripción, precio, duración, imagen |
| **Galería** | Agregar imágenes, reordenar arrastrando, eliminar |
| **Reseñas** | Gestionar opiniones de clientes |
| **FAQ** | Preguntas y respuestas frecuentes |
| **Horarios** | Configurar días y horas de atención |
| **Profesionales** | Agregar empleados con foto y especialidad |
| **Clientes** | Ver clientes que han agendado (solo lectura) |
| **Bookings** | Ver citas agendadas |
| **Theme** | Cambiar colores, fuentes, logo, SEO |
| **Config** | URL del backend, secciones on/off, contraseña |
| **Audit** | Historial de cambios en el admin |

### Keyboard shortcuts
- `Ctrl+S` — Guardar cambios en cualquier pestaña
- `/` — Focus en el campo de búsqueda

### Tips
- Los cambios en el admin se reflejan al recargar la landing page
- Siempre confirma antes de eliminar (hay confirmación)
- Si algo no se ve bien, revisa que la sección esté activa en *Config*
- El modo oscuro/claro se puede cambiar desde el landing o desde el admin

---

## Booking (agendar cita)

Los clientes pueden agendar citas desde la landing page sin necesidad de registrarse:

1. Hacen clic en "Agendar cita" o en el botón flotante de WhatsApp
2. Eligen servicio
3. Eligen profesional
4. Eligen fecha (ven días disponibles)
5. Eligen horario (slots disponibles automáticos)
6. Ingresan sus datos
7. Confirman → se redirigen a WhatsApp con el mensaje pre-llenado

> **Nota**: Para que las citas se guarden en tu Google Sheets, necesitas configurar la URL del backend GAS en *Config*. Sin backend, las citas solo se confirman vía WhatsApp.

---

## Temas visuales

El template incluye 4 temas predefinidos:

| Tema | Estilo |
|---|---|
| **Dark** | Azul índigo/morado oscuro — moderno y sofisticado |
| **Light** | Azul/blanco — limpio y profesional |
| **Minimal** | Blanco y negro — elegante y atemporal |
| **Bold** | Rojo/negro — audaz y llamativo |

Puedes cambiar el tema activo desde el admin en *Theme*. También puedes personalizar colores individuales, fuentes y agregar CSS personalizado.

El toggle de modo oscuro/claro en la landing respeta la preferencia del sistema.

---

## Exportar datos

En el admin, puedes exportar tus datos a CSV:
- **Clientes**: Lista completa con email, teléfono, servicios contratados
- **Bookings**: Citas con fecha, hora, servicio, profesional

El CSV se descarga automáticamente y es compatible con Excel (incluye BOM para caracteres especiales).

---

## Soporte técnico

Si encuentras algún problema:
1. Verifica que todos los archivos están desplegados correctamente en Vercel
2. Revisa que la URL del backend GAS esté correcta en *Config*
3. Si el booking no funciona, confirma que GAS está desplegado como Web App público
4. Para temas visuales, usa el editor en *Theme* — cualquier cambio se ve en vivo

**Contacto**: hola@minegocio.com | WhatsApp: +52 1 555 000 0000
