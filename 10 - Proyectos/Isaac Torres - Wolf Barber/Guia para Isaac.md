---
tags: [manual, operacion, propietario]
created: 2026-07-24
---
# Guía para Isaac

> Manual de operación para el propietario. Cómo mantener el sitio funcionando.

**Propietario**: Isaac Torres — isaactorreswolfbarber@gmail.com

---

## Pasos para operar

### 1. Configurar el backend (GAS)

1. Ir a https://script.google.com
2. Crear proyecto "Wolf Barber Booking"
3. Copiar `Code.gs` completo al editor
4. Ir a *Project Settings → Script Properties* y agregar:
   - `SPREADSHEET_ID` = `1hDT2DbwYv0vh_ZLSb__KNdpA4c6X7ud6-7fgzYraw74`
   - `CALENDAR_ID` = `primary`
   - `NOTIFY_EMAIL` = `sebastianurbiola75@gmail.com`
5. Desplegar → *Aplicación web*
   - Ejecutar como: tu cuenta
   - Acceso: *Cualquiera (público anónimo)*
6. Copiar la URL generada

### 2. Probar notificaciones

En el editor GAS, ejecutar la función `probarNotificacion()`. Debe llegar un correo de prueba a `sebastianurbiola75@gmail.com`.

### 3. Configurar el panel admin

1. Ir a https://isaactorres.vercel.app/admin.html
2. **Usuario**: `wolfbarber` / **Contraseña**: `wolfbarber2026`
3. Aparecerá un **banner amarillo** indicando que falta la URL del API
4. Ir a la pestaña **Configuración** → pegar la URL del Web App GAS → click **"Confirmar"**
5. Ver mensaje verde de confirmación
6. **Cambiar la contraseña inmediatamente** después del primer login

### 4. Verificar funcionamiento

- Agendar una cita de prueba desde el sitio
- Confirmar: folio generado, WhatsApp se abre con datos pre-llenados
- Verificar que aparezca el evento en Google Calendar
- Verificar que llegue el correo de notificación a `sebastianurbiola75@gmail.com`
- Probar cancelación con el folio generado
- Revisar que el cliente aparezca en la pestaña **Clientes** del admin

### 5. Gestionar contenido

Usar el panel admin para:
- Agregar/editar/eliminar **servicios** (con fotos)
- Subir fotos a la **galería** (con categorías: fade, diseños, barba, coloración)
- Configurar **horarios de atención** (día, hora inicio, hora fin, activo/inactivo)
- Agregar/editar/eliminar **reseñas** (nombre, texto, rating 1-5)
- Agregar/editar/eliminar **FAQ** (pregunta + respuesta)
- Gestionar **usuarios** del panel (máximo 3)
- Cambiar **contraseña** de acceso admin

## Responsabilidades

| Isaac (propietario) | Desarrollador |
|---|---|
| Crear proyecto GAS en script.google.com | Configurar Sheet con servicios iniciales |
| Pegar Code.gs y desplegar Web App | Poner URL del API en el admin panel |
| Ejecutar `probarNotificacion()` | Agregar como miembro en Vercel |
| Enviar URL del API al desarrollador | Mantener sitio actualizado |
| Gestionar contenido desde admin panel | Auditorías de seguridad |

## Referencias

- [[10 - Proyectos/Isaac Torres - Wolf Barber/Deployment|Deployment]] — Despliegue completo
- [[10 - Proyectos/Isaac Torres - Wolf Barber/Seguridad - Auditoria|Seguridad]] — Vulnerabilidades corregidas
