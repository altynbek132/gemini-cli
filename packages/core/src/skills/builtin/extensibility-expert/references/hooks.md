# Hooks System

Hooks allow you to intercept and customize Gemini CLI behavior at specific
lifecycle events.

## Configuration

Hooks are configured in `settings.json` under the `hooks` key.

```json
"hooks": {
  "enabled": true,
  "BeforeTool": [
    {
      "type": "command",
      "command": "node my-hook.js",
      "name": "My Custom Hook"
    }
  ]
}
```

## Supported Events

- `BeforeTool` / `AfterTool`: Intercept or process tool calls/results.
- `BeforeAgent` / `AfterAgent`: Setup context or summarize agent loops.
- `BeforeModel` / `AfterModel`: Modify prompts or responses.
- `SessionStart` / `SessionEnd`: Initialize or cleanup session resources.
- `Notification`: Respond to CLI notifications.
- `PreCompress`: Handle context compression events.

## Communication Protocol

- **Input (stdin)**: Hook receives a JSON object with event details
  (`session_id`, `hook_event_name`, `tool_name`, etc.).
- **Output (stdout)**: Hook should emit a JSON object with a `decision` or other
  instructions.
- **Exit Codes**:
  - `0`: Success. `stdout` is parsed as JSON.
  - `2`: Blocking Error. Interrupts operation, shows `stderr` to user.

## Common Output Fields

- `decision`: `allow`, `deny`, `block`, `ask`, `approve`.
- `reason`: Explanation shown to the **agent** (if denied/blocked).
- `systemMessage`: Message shown to the **user**.
- `continue`: `boolean`. If `false`, terminates the agent loop.
- `hookSpecificOutput`:
  - `additionalContext`: Appends text to the agent's context.
  - `llm_request` / `llm_response`: Overrides for model interactions.

## In Extensions

Extensions provide hooks in `hooks/hooks.json` (not `gemini-extension.json`).

```json
{
  "hooks": {
    "before_agent": [
      {
        "type": "command",
        "command": "node ${extensionPath}/scripts/setup.js",
        "name": "Extension Setup"
      }
    ]
  }
}
```
