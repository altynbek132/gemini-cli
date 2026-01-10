# Agent Skills

Agent Skills are modular packages that provide specialized knowledge, workflows,
and tools to the agent.

## Structure

A skill is a directory containing a `SKILL.md` file and optional resource
directories.

```
my-skill/
├── SKILL.md (required)
│   ├── YAML frontmatter (name, description)
│   └── Markdown instructions
├── scripts/    - Executable code
├── references/ - Documentation to be loaded as needed
└── assets/     - Templates, boilerplate, etc.
```

## SKILL.md

### Frontmatter

```yaml
---
name: my-skill
description:
  'Briefly explain WHAT the skill does and WHEN to use it. This is the primary
  triggering mechanism.'
---
```

### Body

Contains detailed instructions for the agent on how to use the skill and its
resources.

## Locations

- **Built-in Skills**: `packages/core/src/skills/builtin/` (pre-installed).
- **User Skills**: `~/.gemini/skills/` (manually added).
- **Extension Skills**: `skills/` directory within an extension folder.

## Best Practices

- **Concise**: Only include context the agent doesn't already have.
- **Progressive Disclosure**: Use the `references/` directory for detailed
  documentation and link to it from `SKILL.md`.
- **Scripts**: Use scripts for deterministic tasks or to avoid repetitive code
  generation.
- **Imperative Tone**: Use commands (e.g., "Analyze the logs", "Generate a
  test").
