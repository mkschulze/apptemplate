# ConPort MCP Setup (Projekt-agnostisch)

Diese Anleitung zeigt, wie ConPort MCP in Copilot (VS Code), Claude und Codex aktiviert wird.
Alle Pfade sind Platzhalter und muessen ersetzt werden.

## Platzhalter
- /ABS/PATH/TO/PROJECT: absoluter Pfad zum Projekt-Root
- /ABS/PATH/TO/LOGFILE: optionaler absoluter Logfile-Pfad

## Voraussetzungen
- Im Projekt existiert context_portal/context.db
- uvx ist installiert (uv) und context-portal-mcp ist verfuegbar
- Optional: logs/ Ordner im Projekt (wenn ./logs/conport.log genutzt wird)

## Copilot (VS Code)
Lege im Projekt eine Datei .vscode/mcp.json an:

```json
{
  "servers": {
    "conport": {
      "command": "uvx",
      "args": [
        "--from",
        "context-portal-mcp",
        "conport-mcp",
        "--mode",
        "stdio",
        "--workspace_id",
        "/ABS/PATH/TO/PROJECT",
        "--log-file",
        "./logs/conport.log",
        "--log-level",
        "INFO"
      ]
    }
  },
  "inputs": []
}
```

## Claude (Desktop)
Konfigurationsdatei (Standardpfade):
- macOS: ~/Library/Application Support/Claude/claude_desktop_config.json
- Windows: %APPDATA%/Claude/claude_desktop_config.json
- Linux: ~/.config/Claude/claude_desktop_config.json

Beispiel:

```json
{
  "mcpServers": {
    "conport": {
      "command": "uvx",
      "args": [
        "--from",
        "context-portal-mcp",
        "conport-mcp",
        "--mode",
        "stdio",
        "--workspace_id",
        "/ABS/PATH/TO/PROJECT",
        "--log-file",
        "/ABS/PATH/TO/LOGFILE",
        "--log-level",
        "INFO"
      ]
    }
  }
}
```

Hinweis: Wenn dein Client kein cwd unterstuetzt, nutze absolute Pfade fuer --log-file.

## Codex (Codex CLI)
In ~/.codex/config.toml:

```toml
[mcp_servers.conport]
command = "uvx"
args = [
  "--from",
  "context-portal-mcp",
  "conport-mcp",
  "--mode",
  "stdio",
  "--workspace_id",
  "/ABS/PATH/TO/PROJECT",
  "--log-file",
  "./logs/conport.log",
  "--log-level",
  "INFO",
]
cwd = "/ABS/PATH/TO/PROJECT"
```

## Validierung
- Client neu starten oder neu laden.
- Einen einfachen Call testen, z. B. get_product_context.

## Troubleshooting
- "Server not found": Config-Pfad/JSON pruefen, Client neu laden.
- "context.db not found": workspace_id stimmt nicht oder DB fehlt.
- "uvx not found": uv installieren oder Pfad anpassen.
