# uv Codex Plugin

Community Codex plugin for uv-centered Python project workflows.

This repository is a Codex marketplace root. It exposes one local plugin,
`uv-python-tools`, with skills for:

- `uv`: Python package and environment management.
- `ruff`: Python linting and formatting.
- `ty`: Python type checking.

## Install

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add kmshdev/uv-codex-plugin
```

Then install the plugin:

```bash
codex plugin add uv-python-tools@uv-codex-plugin
```

Start a new Codex thread after installation so Codex loads the bundled skills.

## Layout

```text
.agents/plugins/marketplace.json
plugins/uv-python-tools/
  .codex-plugin/plugin.json
  skills/
    uv/SKILL.md
    ruff/SKILL.md
    ty/SKILL.md
```

## Attribution

The skill content was migrated from
`https://github.com/astral-sh/claude-code-plugins`. This is a community Codex
plugin, not an official Astral-published or uv-published plugin.

The source plugin is dual licensed under MIT or Apache-2.0. Copies of both
licenses are included in this repository.
