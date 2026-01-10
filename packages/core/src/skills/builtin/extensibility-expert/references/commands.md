# Custom Commands

Custom commands (slash commands) allow you to save and reuse prompts as
shortcuts. They can be global (user-level) or project-specific.

## File Locations

- **User Commands**: `~/.gemini/commands/` (available everywhere)
- **Project Commands**: `<project-root>/.gemini/commands/` (specific to the
  project)
- **Extension Commands**: `commands/` directory within an extension folder.

## Naming and Namespacing

Command names are derived from their file paths relative to the `commands`
directory.

- `test.toml` -> `/test`
- `git/commit.toml` -> `/git:commit`

## TOML Format

Commands must be in TOML format with a `.toml` extension.

### Structure

```toml
description = "Brief description for /help"
prompt = """
Your multi-line prompt goes here.
You can use special placeholders:
- {{args}}: Injects user arguments.
- !{shell command}: Injects output of a shell command.
- @{path/to/file}: Injects content of a file or directory.
"""
```

### Placeholders

- `{{args}}`:
  - Raw injection in the prompt.
  - Shell-escaped injection inside `!{...}` blocks.
- `!{...}`: Executes a shell command. Must have balanced braces.
- `@{...}`: Injects file/directory content. Processed before `!{...}` and
  `{{args}}`.

## Default Argument Handling

If `{{args}}` is NOT in the prompt, arguments provided by the user are appended
to the end of the prompt after two newlines.

## In Extensions

Extensions provide commands by placing TOML files in a `commands/` subdirectory.

- Commands from an extension named `my-ext` might be namespaced as
  `/my-ext:command` if there is a conflict.
- Otherwise, they use their natural name (e.g., `/deploy`).
