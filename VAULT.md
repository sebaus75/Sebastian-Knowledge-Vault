---
created: 2026-07-25
tags: [meta, configuracion, guia]
---

# Configuración del Vault

Este vault sigue el método **PARA** adaptado (Proyectos, Áreas, Recursos, Archivo) + Zettelkasten para notas de pensamiento.

## Reglas

- **Links sobre carpetas**: Preferir `wikilinks` sobre jerarquías profundas
- **Notas atómicas**: Una idea por nota
- **Formato descriptivo** para nombres de archivo: `Nombre - Descripcion.md` (espacios + guiones)
- **MOCs**: Mapas de contenido como índices navegables
- **Sin archivos sueltos en raíz**: Solo `Home.md`, `CONTEXT.md`, `VAULT.md`, `AGENTS.md` y `.gitignore`

## Sistema cerebro (agentes IA)

Esta vault es la memoria de trabajo de los agentes de IA (OpenCode). Contrato, protocolos y reglas de tokens en [[AGENTS.md]]. Puntos de entrada:

1. [[CONTEXT]] — estado global (proyectos, fases, última sesión)
2. [[90 - Sistema/Panel de Estado]] — dashboard Dataview
3. `STATUS.md` en cada proyecto — estado operativo vivo
4. [[90 - Sistema/Registros]] — historial de sesiones (append-only)

Todo cambio en un proyecto debe actualizar su `STATUS.md` el mismo turno.

## Plugins recomendados

- **Dataview**: Consultas dinámicas sobre metadatos
- **Graph Analysis**: Salud del grafo de enlaces
- **Tag Wrangler**: Gestión de tags en lote
- **Vault Inspector**: Detección de enlaces rotos y archivos huérfanos
- **Local Images Plus**: Descarga y organización de imágenes

## Mantenimiento

- Respaldar semanalmente (GitHub + copia local)
- Revisar `00 - Inbox/` cada semana
- Archivar proyectos completados cada mes
- Correr Vault Inspector mensualmente