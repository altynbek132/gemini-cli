# Model-Context Protocol (MCP) Servers

MCP servers allow you to extend Gemini CLI with custom tools. The CLI connects
to these servers to discover and execute tools.

## Configuration

MCP servers are configured in `settings.json` (user, project, or extension)
under the `mcpServers` key.

### Stdio Server (Standard I/O)

Used for local servers executed as subprocesses.

```json
"mcpServers": {
  "my-server": {
    "command": "node",
    "args": ["path/to/server.js"],
    "env": { "API_KEY": "..." },
    "cwd": "path/to/working-dir"
  }
}
```

### SSE Server (Server-Sent Events)

Used for remote servers communicating over HTTP.

```json
"mcpServers": {
  "remote-server": {
    "url": "http://localhost:3001/sse",
    "headers": { "Authorization": "Bearer ..." }
  }
}
```

### HTTP Server

```json
"mcpServers": {
  "http-server": {
    "httpUrl": "http://localhost:3002/mcp"
  }
}
```

## Options

- `trust` (boolean): If `true`, bypasses tool call confirmations for this
  server.
- `includeTools` (string[]): Allowlist of tools to enable.
- `excludeTools` (string[]): Blocklist of tools to disable.
- `timeout` (number): Request timeout in milliseconds.

## In Extensions

Extensions define MCP servers in `gemini-extension.json`.

```json
{
  "name": "my-extension",
  "mcpServers": {
    "ext-server": {
      "command": "node",
      "args": ["${extensionPath}/server.js"]
    }
  }
}
```

Use `${extensionPath}` to reference files within the extension directory.
