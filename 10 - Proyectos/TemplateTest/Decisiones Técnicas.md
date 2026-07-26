---
tags: [adr, arquitectura, decisiones]
---
# Decisiones Técnicas

> Architecture Decision Records (ADR) del proyecto. Cada entrada documenta una decisión significativa, su contexto y sus consecuencias.

---

## ADR-001: Tailwind CDN runtime vs build

**Contexto**: Necesitábamos estilos utility-first sin agregar paso de build al deploy.

**Decisión**: Usar Tailwind CSS vía CDN runtime con configuración inline.

**Consecuencias**:
- + Zero build step, deploy instantáneo
- + Configuración 100% controlable desde HTML/JS
- - ~200ms extra de carga inicial (CDN + parseo)
- - No purge de CSS no usado
- - Dependencia de CDN externa

---

## ADR-002: HTML generado por JS vs HTML estático

**Contexto**: El template debe ser genérico para cualquier nicho, con contenido 100% configurable.

**Decisión**: El `index.html` es un shell mínimo; `app.js` lee `theme.json` + `config.json` y renderiza el HTML dinámicamente.

**Consecuencias**:
- + Un solo `index.html` sirve para cualquier negocio
- + Cambios en config.json se reflejan sin tocar HTML
- + FOUC prevention con CSS inline inicial
- - Sin JS, la landing no muestra nada (JS requerido)
- - Más complejidad en el render que HTML estático

---

## ADR-003: Sin framework JS

**Contexto**: Template estático con interactividad moderada (modal, galería, booking, admin).

**Decisión**: JavaScript vanilla con módulos IIFE, sin React, Vue, Svelte ni similares.

**Consecuencias**:
- + Zero dependencias, bundle mínimo (~31 KB total)
- + Carga instantánea, sin runtime framework
- + Control total sobre performance y bundle
- - Organización manual del código (IIFEs + globales para onclick)
- - Event Bus pub/sub necesario para comunicación entre módulos

---

## ADR-004: Datos locales + GAS opcional

**Contexto**: El template debe funcionar incluso sin configurar el backend GAS.

**Decisión**: `theme.json` y `config.json` se cargan desde el sistema de archivos (estático). GAS es un backend opcional para persistencia real. El admin trabaja sobre localStorage por defecto.

**Consecuencias**:
- + Funciona completamente offline/sin backend
- + Demo inmediato al abrir index.html
- + El usuario puede evaluar sin configurar GAS
- - Sin GAS, los cambios en admin se pierden al limpiar localStorage
- - Arquitectura híbrida (local vs remoto) añade complejidad

---

## ADR-005: 4 temas fijos + editor visual

**Contexto**: El producto necesita diferenciarse visualmente sin requerir diseño personalizado.

**Decisión**: 4 temas predefinidos (dark, light, minimal, bold) + editor visual en admin para personalizar colores, fuentes y estilos.

**Consecuencias**:
- + El usuario puede cambiar toda la apariencia sin tocar código
- + Temas predefinidos garantizan calidad visual
- + Editor en vivo con preview instantánea
- + Dark/light mode toggle nativo con preferencia del sistema
- - 4 temas fijos limitan la diferenciación (mitigado por editor)

---

## ADR-006: Reserva sin recargar página

**Contexto**: El booking modal debe ser rápido y no interrumpir la navegación.

**Decisión**: Booking modal en 5 pasos con generación dinámica de calendario y slots. Confirmación vía WhatsApp sin recargar la página.

**Consecuencias**:
- + Experiencia fluida, sin recarga
- + Slots en tiempo real que respetan buffer, feriados y horas pasadas
- + WhatsApp como canal de confirmación universal (sin necesidad de cuenta)
- - No hay confirmación en tiempo real del lado del negocio (solo email GAS)
- - El booking sin backend real no persiste (solo WhatsApp)

---

## ADR-007: SHA-256 encadenado para passwords

**Contexto**: GAS no tiene bcrypt/Argon2. Necesitábamos algo mejor que SHA-256 directo.

**Decisión**: SHA-256 encadenado 1000 iteraciones en cliente y servidor. Documentado que para producción real se recomienda bcrypt vía backend dedicado.

**Consecuencias**:
- + Mejor que SHA-256 directo (1000× más costoso de brute-force)
- + Implementación idéntica en cliente y servidor (consistente)
- + Sin dependencias externas
- - No es tan seguro como bcrypt/scrypt/Argon2
- - Aún vulnerable a ASIC/GPU brute-force con suficientes recursos

---

## ADR-008: Sesión admin en memoria

**Contexto**: El panel admin necesita autenticación segura sin backend de sesiones.

**Decisión**: Password solo en variable JS en memoria. Sin sessionStorage, sin localStorage. Al cerrar pestaña, la sesión expira.

**Consecuencias**:
- + No hay credenciales persistidas en el navegador
- + Al cerrar pestaña, sesión termina automáticamente
- + Rate limiting del lado del cliente previene fuerza bruta local
- - Usuario debe re-ingresar password al recargar la página
- - La validación es local, no contra servidor (hasta que se configure GAS)

---

## ADR-009: Galería con drag & drop nativo

**Contexto**: La galería necesita reordenamiento visual sin librerías externas.

**Decisión**: Usar HTML5 Drag & Drop API nativa en lugar de librerías como SortableJS.

**Consecuencias**:
- + Zero dependencias externas
- + Funcionalidad completa (drag, drop, reorder)
- + Compatibilidad con navegadores modernos
- - Sin soporte táctil nativo (drag & drop HTML5 es pobre en móvil)
- - Implementación manual de todas las interacciones

---

## ADR-010: CSP con nonce para scripts inline

**Contexto**: Seguridad requiere CSP, pero el proyecto usa scripts inline.

**Decisión**: CSP configurado con nonce generado por JS. Documentado que para máxima seguridad se requiere build tooling que genere nonces server-side.

**Consecuencias**:
- + CSP funcional sin `'unsafe-inline'`
- + Nonce único por carga de página
- + Previene inyección de scripts no autorizados
- - Nonce generado por JS es menos seguro que server-side
- - Sin build tooling, el nonce debe manejarse manualmente
