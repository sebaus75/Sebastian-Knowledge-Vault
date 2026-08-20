---
estado: Activo
fase: registro
created: 2026-08-19
updated: 2026-08-19
tags: [proyecto/activo, cad, python, planos, dxf]
---
# Proyectos CAD

> Pipeline Python para generación, verificación y render de planos arquitectónicos/eléctricos (DXF → PDF/previews) con `ezdxf`. Trabajo actual: vivienda de 2 niveles `VIVIENDA_2_NIVELES`. Carpeta: `Proyectos Open Code/Proyectos CAD/`.

**Estado vivo**: [[10 - Proyectos/Proyectos CAD/STATUS]] — fase, pendientes y próxima sesión.
**Código fuente**: `../Proyectos Open Code/Proyectos CAD/`

---

## Map of Content

- [[10 - Proyectos/Proyectos CAD/STATUS|STATUS]] — estado operativo

---

## Estado actual (documentado 2026-08-19)

**Pipeline verificado en repo:**

| Script | Rol |
|---|---|
| `generar_plano.py` (~29 KB) | Genera DXF R2010 (metros, escala 1:1 Model Space): vivienda 6.00 × 15.00 m, PB (X 0-6, Y 0-15), PA (offset +9 m), tablas/cuadro/unifilar/leyenda |
| `verificar_plano.py` (~10 KB) | Chequeos de integridad/geometría del DXF |
| `render_previews.py` | Previews PNG por hoja (`previews/`: HOJA_1..3, PA, PB_arquitectura, PB_electrica, Tablas) |
| `exportar_pdf.py` | Exportación a PDF |

**Salidas generadas:** `VIVIENDA_2_NIVELES.dxf` (170 KB) + `.pdf` (2.6 MB) + 7 previews PNG.
**Flujo AutoCAD (plot.log, 12/ago/2026):** fuente `Documents/Autocad Proyectos/DSE/VIVIENDA_2_NIVELES.dwg` → PDF con `DWG To PDF.pc3`, ISO A2 (594×420), escala 1:50; 3 hojas (PB arquitectónica, PB eléctrica, PA arquitectónica + eléctrica).

## Pendientes del proyecto

- [ ] Documentar el flujo completo como runbook (entradas → pasos → salidas) para reproducibilidad.
- [ ] Evaluar: ¿pipeline reutilizable para otros proyectos (DSE) o trabajo puntual de `VIVIENDA_2_NIVELES`?