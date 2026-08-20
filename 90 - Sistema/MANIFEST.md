---
created: 2026-08-19
updated: 2026-08-19
tags: [meta, sistema, enrutamiento]
---

# MANIFEST — Enrutamiento proyecto → vault

Índice único que mapea cada proyecto de `Proyectos Open Code/` con su carpeta de documentación en la vault. **Leer siempre en inicio de sesión** (después de `CONTEXT.md`) para saber dónde documentar. Actualizar al registrar, renombrar, pausar o archivar proyectos.

## Mapa de proyectos

| Carpeta de proyecto (`Proyectos Open Code/`) | Carpeta en vault (`10 - Proyectos/`) | Fase | Estado | Modelo sugerido | Skills asociadas |
|---|---|---|---|---|---|
| `IsaacTorres/` | [[10 - Proyectos/Isaac Torres - Wolf Barber\|Isaac Torres - Wolf Barber]] | `produccion` | Activo | `estándar` | `wolf-barber-booking` |
| `SupleHuges/` | [[10 - Proyectos/Suplehuges\|Suplehuges]] | `propuesta-comercial` | Activo | `estándar` | — |
| `TemplateTest/` | [[10 - Proyectos/TemplateTest\|TemplateTest]] | `listo-empaquetar` | Activo | `estándar` | — |
| `El Legado/` | [[10 - Proyectos/El Legado\|El Legado]] | `en-desarrollo` | Activo | `barato` | `wolf-barber-booking` |
| `Mantenimiento y seguridad/` | [[10 - Proyectos/Mantenimiento y seguridad\|Mantenimiento y seguridad]] | `sistema-cerebro` | Activo | `barato` | `vault-brain` |
| `Proyectos CAD/` | [[10 - Proyectos/Proyectos CAD\|Proyectos CAD]] | `registro` | Activo | `barato` | — |
| `Sentido Creativo/` | [[10 - Proyectos/Sentido Creativo\|Sentido Creativo]] | `asesoria-ia` | Activo | `estándar` | — |

> **Modelo sugerido** (P2-01, decisión 2026-08-19): `barato` (deepseek-v4-flash-free) para fases `registro`/`sistema-cerebro`/búsquedas; `estándar` para `produccion`/diseño. No se fija `model` por proyecto: el ahorro no justifica la complejidad hoy; la columna documenta la guía si algún día aplica.

## Reglas de uso

1. **Enrutamiento**: al tocar un proyecto, leer `10 - Proyectos/<P>/STATUS.md` antes de actuar. Documentar cada cambio en la carpeta del proyecto (notas) y en su `STATUS.md` el mismo turno.
2. **Auto-provisioning**: si un proyecto de código no tiene carpeta en la vault, crearla (`MOC.md` + `STATUS.md`) y añadir su fila aquí **el mismo turno**, sin preguntar.
3. **Transición de fase**: actualizar `fase` en esta tabla + en el MOC del proyecto (ver skill `vault-brain` §4).
4. **Cierre/archivo**: mover carpeta a `40 - Archivo/` y quitar la fila de aquí (mantener nota de destino en el registro del día).

## Dónde documentar según el tipo de contenido

| Contenido | Destino |
|---|---|
| Progreso, pendientes, decisiones de un proyecto | `10 - Proyectos/<P>/STATUS.md` + notas del proyecto |
| Decisiones técnicas (ADR) | Sección "Decisiones" del MOC o nota dedicada en la carpeta |
| Sesión de trabajo (qué se hizo/falta) | `90 - Sistema/Registros/YYYY-MM-DD.md` (append-only) |
| Conocimiento reutilizable (conceptos, guías) | `30 - Recursos/` |
| Skills y su memoria | `30 - Recursos/Skills/` (fuente de verdad; sync a config global) |
| Material cerrado/obsoleto | `40 - Archivo/` (nunca borrar) |
| Entrada sin procesar | `00 - Inbox/` |