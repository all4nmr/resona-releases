# Resona NMR Studio — Downloads

Release binaries for **Resona NMR Studio**, an NMR processing and assignment
platform.

**This repository contains release binaries only.** The source code is in a
private repository and is not published here.

## Downloads

Get everything from the [Releases](https://github.com/all4nmr/resona-releases/releases)
page — files download directly, no intermediate page.

### macOS (Apple Silicon)

| File | Size | What it is |
|---|---|---|
| `Resona-mac-arm64.dmg` | 77 MB | The application |
| `ResonaMCP-mac-arm64.tar.gz` | 29 MB | MCP server for AI agents (separate download) |

### Windows

| File | Size | What it is |
|---|---|---|
| `ResonaSetup-0.1.0.exe` | — | Installer — installs the app **and** the MCP server |

Windows ships as a single installer. There is nothing else to download.

Latest version, direct links:

- macOS app: <https://github.com/all4nmr/resona-releases/releases/latest/download/Resona-mac-arm64.dmg>
- macOS MCP server: <https://github.com/all4nmr/resona-releases/releases/latest/download/ResonaMCP-mac-arm64.tar.gz>
- Windows installer: <https://github.com/all4nmr/resona-releases/releases/latest/download/ResonaSetup-0.1.0.exe>

## macOS: install the app

1. Download `Resona-mac-arm64.dmg`.
2. Open it and drag **Resona** into your **Applications** folder.
3. Launch it from Applications.

Requires Apple Silicon (M1/M2/M3/M4). Intel Macs are not supported.

The app is not notarized, so Gatekeeper warns on first launch:

> "Resona is from an unidentified developer and may be damaged."

**This warning is expected and the app is safe.** Either:

- Right-click **Resona** in Applications → **Open** → **Open** on the dialog
  (recommended), or
- Run `xattr -cr /Applications/Resona.app` once from Terminal

## Windows: install the app

1. Download `ResonaSetup-0.1.0.exe`.
2. Run it. The installer places the app and, if you keep the default options,
   the MCP server alongside it.
3. Launch **Resona** from the Start menu or the desktop shortcut.

The installer is **not code-signed**, so Windows SmartScreen may warn:

> "Windows protected your PC"

Choose **More info** → **Run anyway**. This warning is expected — the software
is unsigned, not malicious.

No administrator rights are required: the installer installs per-user under
`%LOCALAPPDATA%\Resona`, so you can decline the UAC prompt.

## The MCP server (for AI agents)

The MCP server lets AI agents (Claude, Cursor, ChatGPT, and similar) call
Resona's 55 tools directly: spectrum processing, peak picking, protein
auto-assignment, J-coupling search, relaxation, DNMR fitting.

**Windows users: nothing to do.** The installer already places the MCP server
at:

```
%LOCALAPPDATA%\Resona\mcp\ResonaMCP.exe
```

**macOS users:** download `ResonaMCP-mac-arm64.tar.gz` separately. It is not
inside the .app.

```bash
mkdir -p ~/ResonaMCP && cd ~/ResonaMCP
tar -xzf ~/Downloads/ResonaMCP-mac-arm64.tar.gz
chmod +x ResonaMCP/ResonaMCP
```

Do not move or rename the `_internal/` folder — the server will not start
without it.

### Connecting an AI client

Point the client at the server. The path must be **absolute**.

**Windows** (Claude Desktop,
`%APPDATA%\Claude\claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "resona": {
      "command": "C:\\Users\\YOUR_NAME\\AppData\\Local\\Resona\\mcp\\ResonaMCP.exe"
    }
  }
}
```

**macOS** — config file location depends on the client:

| Client | Config path |
|---|---|
| Claude Desktop | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Cursor | `~/.cursor/mcp.json` |
| VS Code (Copilot / Cline / Roo) | `~/.vscode/mcp.json` |

```json
{
  "mcpServers": {
    "resona": {
      "command": "/Users/YOUR_NAME/ResonaMCP/ResonaMCP/ResonaMCP"
    }
  }
}
```

Restart the client fully after editing — closing the window leaves a
background process running and the change will not take effect.

Success looks like these tools appearing: `project_status`, `process_1d`,
`run_batch`, `assign_protein`, `j_couplings_1d`, `dnmr_vt_fit`.

### Human approval is required

The server cannot bypass your sign-off. `apply_labels` — the tool that writes
labels onto real peaks — refuses to run unless the caller passes both
`human_confirmed: true` and a `human_statement`. Read-only inspection,
review, candidate approval, and dry-run previews are unrestricted.

Agents propose; you approve.

## Requirements

- macOS 12 or newer, Apple Silicon
- Windows 10 or newer

## Troubleshooting

**Nothing appears in my AI client.** Check the path is absolute, restart the
client fully, and confirm the file exists. On Windows, verify
`%LOCALAPPDATA%\Resona\mcp\ResonaMCP.exe` is present.

**"ResonaMCP" tools missing but the server connects.** Your client may be
speaking an older MCP protocol version. Update it.

**macOS: `Cannot open ... because it is from an unidentified developer`.**
Right-click → Open, or `xattr -cr` the binary as shown above.

## License

Non-commercial use only: students, private individuals, government agencies,
public educational institutions, and non-profit organizations. Commercial use
by a for-profit entity requires a separate paid license.

Copyright © 2026 Jeahoo Kwon. All rights reserved.

Questions: all4nmr@gmail.com
