# Conectar este repositorio a un servidor MCP (guía rápida)

Pasos mínimos para conectar tu repo a un MCP local:

1. Preparar un túnel (si el MCP corre en tu máquina y GitHub debe alcanzarlo):

   - Instala y ejecuta `ngrok` (o similar) para exponer un puerto local:

   ```powershell
   ngrok http 3000
   ```

   - Copia la URL pública que te da ngrok (ej. `https://abcd1234.ngrok.io`).

2. Configurar webhook en GitHub:

   - Ve a la página del repo en GitHub → Settings → Webhooks → Add webhook.
   - Payload URL: `https://<TU_NGROK_URL>/events/github` (o la URL esperada por tu MCP).
   - Content type: `application/json`.
   - Secret: usa el mismo valor que pongas en `mcp.json` → `hooks.onPush.secret`.
   - Selecciona 'Let me select individual events' y marca `Push`.

3. Ejecutar tu servidor MCP localmente:

   - El comando exacto depende de la implementación del MCP que uses. En general, inicia el servidor y configúralo para escuchar en el puerto que estás exponiendo con ngrok (ej. 3000).

4. Verificar:

   - Haz un `git push` al repo y observa que el MCP reciba el evento.
   - Revisa logs del MCP para confirmar procesamiento.

5. Opcional — automatizar con scripts:

   - Añade un script de PowerShell/Bash que inicie ngrok y el MCP y muestre la URL para copiarla al webhook.

Archivos en este repo:

- `mcp.json`: manifiesto con entrada y configuración de webhook (edítalo con tu host/secret).
- `index.html`: entrada del sitio/juego.

Notas:

- Si tu MCP es una plataforma cloud, en vez de ngrok configura el webhook directamente con la URL que te proporcione la plataforma.
- Si quieres, puedo crear un script `start-mcp.ps1` que arranque ngrok y muestre la URL pública.
