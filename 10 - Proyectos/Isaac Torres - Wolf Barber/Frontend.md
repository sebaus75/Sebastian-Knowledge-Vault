---
tags: [frontend, html, css, javascript]
created: 2026-07-24
---
# Frontend

## index.html (~560 líneas)

Landing page oscuro/dorada con temática vikinga. Carga vía Tailwind CDN runtime con configuración `tailwind.config` inline.

### Secciones
| Sección | Detalle |
|---|---|
| Navbar | Fijo, glassmorphism al scrollear, logo + smooth scroll |
| Hero | Fullscreen con imagen de fondo, gradiente, **animación escalonada de entrada** |
| About | Grid 2 columnas, gold brackets, runas decorativas, stats |
| Servicios | Render JS dinámico desde API, shimmer hover |
| Galería | Filtros por categoría, lightbox, paginación (4 items) |
| CTA | "Únete a la Manada" con botón booking |
| Contacto | Dirección, WhatsApp, horarios, iframe Google Maps |
| **Reviews** | **Carrusel de testimonios con auto-play 5s, dots, navegación, touch** |
| **FAQ** | **Acordeón de preguntas frecuentes (solo una abierta a la vez)** |
| Footer | Logo, nav links, redes sociales, link admin (nueva pestaña) |

### Componentes
- **Booking Modal** — 4 pasos (servicio → fecha/hora → datos → confirmación)
- **Cancel Modal** — Ingresa folio para cancelar vía API POST
- **Lightbox** — Vista completa de imagen con tecla Escape
- **Mobile Menu** — Overlay fullscreen con transición
- **WhatsApp FAB** — Flotante en mobile

## script.js (~864 líneas)

Organizado en IIFEs y funciones globales (necesarias para `onclick` en HTML):

| Bloque | Responsabilidad |
|---|---|
| `getApiUrl()` | Obtiene URL del API (localStorage → fallback hardcoded) |
| Navbar scroll | `scroll` event → clase `.scrolled` |
| Scroll reveal | `IntersectionObserver` con rootMargin |
| Mobile menu | Toggle `translate-x-full` |
| Smooth scroll | `scrollTo` con offset del navbar |
| Lightbox | Open/close con overlay click y Escape |
| Cancel booking | POST a API con folio |
| Booking modal | 4 steps: service select, date/time **dinámico desde API schedule**, personal info, confirm |
| Gallery | Filter + pagination (4/page) |
| Fetch data | services, gallery, config, **reviews, faq** desde API |
| Render | services, booking services, gallery items, **reviews carousel, FAQ accordion** |

### Reviews Carousel
- `window.renderReviews(reviews)` — lanza track-slider con auto-play 5s
- Navegación por dots, botones prev/next, soporte touch
- Rating en estrellas ★, texto en itálica, nombre del cliente
- Si no hay reseñas, no se renderiza nada

### FAQ Accordion
- `window.renderFAQ(faq)` — acordeón con toggle click
- Solo un item abierto a la vez (los demás se cierran automáticamente)
- Animación suave con max-height y rotate del ícono expand_more

## Hero Animation

Animación escalonada con `@keyframes`:
| Elemento | Efecto | Delay |
|---|---|---|
| "Isaac Torres" | Fade up 80px + blur 4px | 0.2s |
| "ᛟ WOLF BARBER ᛟ" | Fade up 60px | 0.7s |
| Línea dorada | Slide-in desde left, ancho 200px | 1.3s |
| "Est. 2020" | Fade up 40px | 1.8s |

Usa `cubic-bezier(0.16, 1, 0.3, 1)` para sensación elástica.

## style.css (~415 líneas)

Variables CSS personalizadas, glass-nav, shimmer, scroll-reveal, time-slots, country-selector, gallery filters, modal overlay, focus-visible, animaciones hero, carrusel reviews, accordion FAQ.
