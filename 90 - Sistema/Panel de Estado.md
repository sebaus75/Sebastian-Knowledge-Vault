---
created: 2026-08-10
updated: 2026-08-10
tags: [meta, dashboard, sistema]
---

# Panel de Estado

Dashboard generado por Dataview. Requiere el plugin **Dataview** activo. Es la entrada rápida para agentes y humanos.

## Proyectos activos

```dataview
TABLE fase, estado, created, updated AS "Actualizado"
FROM "10 - Proyectos" AND #proyecto/activo
SORT created DESC
```

## STATUS por proyecto

```dataview
TABLE fase, actualizado
FROM "10 - Proyectos" AND "STATUS"
SORT actualizado DESC
```

## Inbox pendiente

```dataview
LIST
FROM "00 - Inbox"
SORT file.ctime DESC
```

## Registros de sesión (últimos 5)

```dataview
LIST
FROM "90 - Sistema/Registros"
SORT file.name DESC
LIMIT 5
```

## Archivo (cerrados)

```dataview
LIST
FROM "40 - Archivo"
SORT file.name ASC
```

## Enlaces rotos

> Ejecutar manualmente: plugin **Checklist/Broken Links** de Obsidian, o el script `link_audit.mjs` del proyecto Mantenimiento y seguridad.
