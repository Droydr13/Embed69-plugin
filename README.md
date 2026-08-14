# Nuvio Embed69

Fork personal de [Ray's Plugins](https://github.com/hihihihihiiray/nuvio-plugins) para la app **Nuvio**, con el `manifest.json` limitado únicamente al proveedor **Embed69**.

## Instalación

1. Abre la app **Nuvio**
2. Ve a **Settings → Plugins → Add new repository**
3. Pega esta URL (reemplaza `TU-USUARIO` y `TU-REPO`):
   ```
   https://raw.githubusercontent.com/Droydr13/Embed69-plugin/refs/heads/main/manifest.json
   ```
4. Activa el plugin Embed69

## Workflows incluidos

### `sync.yml` — Sincronización semanal con el repo original
- Corre automáticamente cada domingo (y también manual, desde la pestaña **Actions → Weekly Upstream Sync → Run workflow**).
- Trae los cambios que haga el mantenedor original (`hihihihihiiray/nuvio-plugins`) a los archivos de `providers/`.
- **Nunca toca `manifest.json`**, gracias a `.gitattributes` (`manifest.json merge=ours`) — así siempre se mantiene con solo Embed69 habilitado, sin importar qué providers agregue o quite el repo original.
- Si hay un conflicto de merge fuera de `manifest.json`, aborta y crea un Issue automático para revisión manual.

### `updateuseragent.yml` — Actualizar el User-Agent (heredado del repo original)
- **No corre solo** — solo se dispara manualmente desde **Actions → Update User Agent → Run workflow**.
- Te pide un nuevo string de User-Agent y lo reemplaza en todos los archivos de `providers/` que lo usen.
- Útil si algún sitio empieza a bloquear el user-agent actual.

## Cómo funciona la protección del manifest

- `.gitattributes` marca `manifest.json` con `merge=ours`.
- El workflow de sync agrega el repo original como remoto `upstream`, hace `fetch` y `merge upstream/main`.
- Todos los archivos `.js` de `providers/` se mantienen sincronizados (aunque el manifest solo exponga Embed69), para que cualquier arreglo a esos archivos también te llegue.
