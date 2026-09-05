# Sakupa MCP plugin

Publish and manage AI-made static websites from the AI tool you already use.
This repository is the plugin / extension manifest for the **Sakupa MCP server**;
every entry point below launches the same npm package, `npx -y @sakupa/mcp@latest`,
so the plugin is always on the latest published version.

Full guide: https://sakupa.com/manual/ · Release timeline: https://sakupa.com/timeline/

## Install as a plugin or extension

| Tool | Commands |
| --- | --- |
| Claude Code | `claude plugin marketplace add myerwang/sakupa-plugin` then `claude plugin install sakupa@sakupa-plugin` |
| Codex (CLI, app, ChatGPT) | `codex plugin marketplace add myerwang/sakupa-plugin` then open `/plugins` and install **Sakupa** |
| Gemini CLI | `gemini extensions install https://github.com/myerwang/sakupa-plugin` |

## Or add the MCP server directly

| Tool | Command |
| --- | --- |
| Claude Code | `claude mcp add --transport stdio --scope user sakupa -- npx -y @sakupa/mcp@latest` |
| Codex | `codex mcp add sakupa -- npx -y @sakupa/mcp@latest` |
| Gemini CLI | `gemini mcp add sakupa npx -y @sakupa/mcp@latest` |
| VS Code | `code --add-mcp '{"name":"sakupa","command":"npx","args":["-y","@sakupa/mcp@latest"]}'` |
| Any MCP host | add the JSON below to its MCP configuration |

```json
{
  "mcpServers": {
    "sakupa": {
      "command": "npx",
      "args": ["-y", "@sakupa/mcp@latest"]
    }
  }
}
```

Or just tell your AI tool: *"Install the official Sakupa plugin from myerwang/sakupa-plugin
and verify it."* Tools with a plugin system install the plugin; the others can use the JSON above.

## Layout

- `gemini-extension.json` — the repository root is the Gemini CLI extension.
- `.claude-plugin/marketplace.json` — Claude Code marketplace listing `plugins/sakupa`.
- `.agents/plugins/marketplace.json` — Codex marketplace listing `plugins/sakupa`.
- `plugins/sakupa/` — the plugin itself: `.claude-plugin/plugin.json`, `.codex-plugin/plugin.json`,
  and the MCP server declarations (`.mcp.json`, `codex-mcp.json`).

These files are generated from the Sakupa source repository and mirrored here on every
update; the version in each manifest equals the published `@sakupa/mcp` version. Issues and feedback:
https://sakupa.com/support/
