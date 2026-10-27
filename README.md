# Sakupa MCP plugin

Publish and manage company websites from AI chat without a Sakupa account. Renewable 30-day free sites; hosting from JPY 200/site/month. Custom domains require a subscription; email forms have monthly quotas.
This repository contains the plugin / extension manifests and a website workflow skill for the **Sakupa MCP server**;
every entry point below launches the same npm package, `npx -y @sakupa/mcp@latest`,
so the plugin is always on the latest published version.

Product: https://sakupa.com/product/ · Full guide: https://sakupa.com/manual/ · Release timeline: https://sakupa.com/timeline/

## Install as a plugin or extension

| Tool | Commands |
| --- | --- |
| Claude Code | `claude plugin marketplace add myerwang/sakupa-plugin` then `claude plugin install sakupa@sakupa-plugin` |
| Codex (CLI, app, ChatGPT) | `codex plugin marketplace add myerwang/sakupa-plugin` then open `/plugins` and install **Sakupa** |
| Gemini CLI | `gemini extensions install https://github.com/myerwang/sakupa-plugin` |

## Company website workflow skill

The `publish-with-sakupa` skill covers creating a company or shop website, updating content,
publishing checked static files, connecting a subscribed domain and explaining site expiry.
It preserves provider choice and requires the normal deployment and payment confirmations.
Installing an MCP connection alone does not install this skill. Discovery and activation depend
on your host and version; no automatic reminder or hosting purchase is created by loading it.

The same `SKILL.md` is generated into `plugins/sakupa/skills/publish-with-sakupa/` for
Claude Code and Codex, and `skills/publish-with-sakupa/` for Gemini CLI. Existing installations
should use their host's plugin/extension update flow. Verify that the skill is visible before
relying on automatic activation.

For workspace installation, use your host's supported skill flow and place the unchanged
[skill file](skills/publish-with-sakupa/SKILL.md) in the appropriate directory:

| Host | Workspace path |
| --- | --- |
| Cursor | `.cursor/skills/publish-with-sakupa/SKILL.md` |
| VS Code | `.github/skills/publish-with-sakupa/SKILL.md` |
| Windsurf / Devin Desktop | `.devin/skills/publish-with-sakupa/SKILL.md`; older Windsurf versions use `.windsurf/skills/` |

Choose the path your installed version supports. Do not overwrite unrelated workspace rules.
The skill itself creates no project files until the user chooses and authorizes an action.

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

These files are generated from the Sakupa source repository and mirrored after local validation.
The runtime version follows published `@sakupa/mcp`; the Codex manifest also has a separate
cache revision for plugin content updates. Skill copies come from one canonical source. Issues and feedback:
https://sakupa.com/support/
