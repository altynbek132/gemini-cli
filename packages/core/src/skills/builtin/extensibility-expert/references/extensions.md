# Extensions

Extensions package custom commands, MCP servers, prompts, hooks, and skills into
a shareable format.

## Directory Structure

```
my-extension/
├── gemini-extension.json
├── GEMINI.md (optional, extension-specific context)
├── commands/ (TOML commands)
├── hooks/
│   └── hooks.json
├── skills/ (Agent Skills)
└── mcp-servers/ (if any)
```

## `gemini-extension.json`

```json
{
  "name": "my-extension",
  "version": "1.0.0",
  "mcpServers": {
    "server1": { "command": "node ${extensionPath}/server.js" }
  },
  "contextFileName": "GEMINI.md",
  "excludeTools": ["run_shell_command(rm -rf)"],
  "settings": [
    {
      "name": "API Key",
      "envVar": "MY_API_KEY",
      "sensitive": true
    }
  ]
}
```

## Management Commands

- `gemini extensions install <source>`: Install from GitHub URL or local path.
- `gemini extensions new <path> [template]`: Create a boilerplate extension.
  - Templates: `context`, `custom-commands`, `exclude-tools`, `mcp-server`.
- `gemini extensions link <path>`: Symlink a local extension for development.
- `gemini extensions update <name>`: Update an installed extension.
- `gemini extensions list`: Show all installed extensions.

## Variables

- `${extensionPath}`: Path to the extension folder.
- `${workspacePath}`: Path to the current workspace.
- `${/}` or `${pathSeparator}`: OS-specific path separator.
