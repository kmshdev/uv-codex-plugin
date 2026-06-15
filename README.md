# Astral Codex Plugin

Community Codex port of the Astral Claude Code plugin skills for Python projects.

This repository is a Codex marketplace root. It exposes one local plugin, `astral`,
with skills for:

- `uv`: Python package and environment management.
- `ruff`: Python linting and formatting.
- `ty`: Python type checking.

## Install

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add kmshdev/astral-codex-plugin
```

Then install the plugin:

```bash
codex plugin add astral@astral-codex-plugin
```

Start a new Codex thread after installation so Codex loads the bundled skills.

## Layout

```text
.agents/plugins/marketplace.json
plugins/astral/
  .codex-plugin/plugin.json
  skills/
    uv/SKILL.md
    ruff/SKILL.md
    ty/SKILL.md
```

## Attribution

The skill content was migrated from
`https://github.com/astral-sh/claude-code-plugins`. This is a community Codex
port, not an official Astral-published plugin.

The source plugin is dual licensed under MIT or Apache-2.0. Copies of both
licenses are included in this repository.
