# Nuvio Embed69

Fork personal de [Ray's Plugins](https://github.com/hihihihihiiray/nuvio-plugins) para la app **Nuvio**, con el `manifest.json` limitado únicamente al proveedor **Embed69**.

Este repo se sincroniza automáticamente cada semana (y manualmente vía `workflow_dispatch`) con el repositorio original, para recibir arreglos y mejoras en los archivos de `providers/`. El `manifest.json` está protegido (`merge=ours`) para que la sincronización nunca lo sobreescriba: siempre se mantiene solo con Embed69 habilitado.

## Instalación

1. Abre la app **Nuvio**
2. Ve a **Settings → Plugins → Add new repository**
3. Pega esta URL (reemplaza `TU-USUARIO` por tu usuario/repo de GitHub):
   ```
   https://raw.githubusercontent.com/TU-USUARIO/TU-REPO/refs/heads/main/manifest.json
   ```
4. Activa el plugin Embed69

## Cómo funciona la sincronización

- `.gitattributes` marca `manifest.json` con `merge=ours`, así los merges automáticos nunca tocan ese archivo.
- El workflow `sync.yml` agrega el repo original como remoto `upstream`, hace `fetch` y `merge upstream/main`.
- Si hay un conflicto fuera de `manifest.json`, el workflow aborta el merge y crea un Issue automáticamente para revisión manual.
