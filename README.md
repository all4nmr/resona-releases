# Resona NMR Studio — Downloads

Release binaries for **Resona NMR Studio**, an NMR processing and
assignment platform.

| Platform | File | Size |
|---|---|---|
| macOS (Apple Silicon) | `Resona-mac-arm64.dmg` | 77 MB |
| macOS MCP server | `ResonaMCP-mac-arm64.tar.gz` | 29 MB |
| Windows | see below | — |

**This repository contains release binaries only.** The source code lives in a
private repository and is not published here.

## Download

Go to the [Releases](https://github.com/all4nmr/resona-nmr-studio-releases/releases)
page and pick the version you want. Files download directly — no intermediate
page.

Direct links for the latest version:

- macOS app: <https://github.com/all4nmr/resona-nmr-studio-releases/releases/latest/download/Resona-mac-arm64.dmg>
- macOS MCP server: <https://github.com/all4nmr/resona-nmr-studio-releases/releases/latest/download/ResonaMCP-mac-arm64.tar.gz>

## macOS: install the app

1. Download `Resona-mac-arm64.dmg`.
2. Open it and drag **Resona** into your **Applications** folder.
3. Launch it from Applications.

The app is not notarized, so macOS Gatekeeper warns on first launch:

> "Resona is from an unidentified developer and may be damaged."

**This warning is expected and the app is safe.** Either:

- Right-click **Resona** in Applications → **Open** → **Open** on the dialog
  (recommended), or
- Run `xattr -cr /Applications/Resona.app` once from Terminal

Requires Apple Silicon (M1/M2/M3/M4). Intel Macs are not supported.

## macOS: install the MCP server (for AI agents)

This is a **separate** download — the MCP server is not inside the .app.

```bash
mkdir -p ~/ResonaMCP && cd ~/ResonaMCP
tar -xzf ~/Downloads/ResonaMCP-mac-arm64.tar.gz
chmod +x ResonaMCP/ResonaMCP
```

Do not move or rename the `_internal/` folder; the server will not start
without it.

Then point your AI client at it (absolute path required):

```json
{
  "mcpServers": {
    "resona": {
      "command": "/Users/YOUR_NAME/ResonaMCP/ResonaMCP/ResonaMCP"
    }
  }
}
```

Config file locations:

| Client | Path |
|---|---|
| Claude Desktop | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Cursor | `~/.cursor/mcp.json` |
| VS Code (Copilot / Cline / Roo) | `~/.vscode/mcp.json` |

Restart the client fully after editing — closing the window is not enough.

Success looks like these tools appearing: `project_status`, `process_1d`,
`run_batch`, `assign_protein`, `j_couplings_1d`, `dnmr_vt_fit`.

## Windows

Windows installers are attached to the same releases page. The installer puts
both the GUI app and the MCP server in place for you.

## Requirements

- macOS 12 or newer, Apple Silicon
- Windows 10 or newer

## License

Non-commercial use only — students, private individuals, government agencies,
public educational institutions, and non-profit organizations. Commercial use
requires a separate paid license. See the LICENSE file in the releases page
or contact all4nmr@gmail.com.