---
proyecto: "Mantenimiento y seguridad"
tipo: guia
created: 2026-08-19
updated: 2026-08-19
tags: [proyecto, sistema, setup, portabilidad]
---

# Setup — Multi-Máquina (P3-02)

Cómo levantar el sistema cerebro completo en otra máquina.

## 1. Clonar la vault (git)

```powershell
git clone https://github.com/sebaus75/Sebastian-Knowledge-Vault.git "C:\Users\<usuario>\Desktop\Sebastian_Knowledge_Vault\Sebastian Knowledge Vault"
```

## 2. Copiar la config de OpenCode

Copiar la carpeta completa `~/.config/opencode/` (scripts, plugins, skills, certs, commands, `opencode.jsonc`). Ojo: `node_modules/` se regenera manteniendo `package.json`.

## 3. Variable de entorno

Los scripts y el plugin leen `VAULT_PATH` (fallback: ruta local por defecto):

```powershell
[Environment]::SetEnvironmentVariable("VAULT_PATH", "C:\Users\<usuario>\...\Sebastian Knowledge Vault", "User")
```

`NODE_EXTRA_CA_CERTS` apunta al cert (`~/.config/opencode/certs/obsidian-local-rest-api.crt`) — necesario para el MCP con cert autofirmado.

## 4. Verificación tras clonar

```powershell
powershell -ExecutionPolicy Bypass -File ~/.config/opencode/scripts/mcp-health.ps1   # OK con Obsidian abierto
powershell -ExecutionPolicy Bypass -File ~/.config/opencode/scripts/sync-skills.ps1  # DONE n skills
```

Si el MCP degrada (cert/API key regenerados al reiniciar Obsidian): re-descargar cert y key desde Ajustes del plugin, actualizar `opencode.jsonc` (y el `opencode.json` del proyecto) y reiniciar opencode. `mcp-health.ps1` detecta el fallo y da la instrucción.

## 5. Tareas programadas a recrear

- `Vault Backup Semanal` (dom 09:00, `backup-vault.ps1 -Push`)
- `Vault Health Semanal` (lun 08:00, `health-weekly.ps1`)