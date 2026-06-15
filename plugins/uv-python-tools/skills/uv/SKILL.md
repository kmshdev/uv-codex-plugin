---
name: uv
description: Use when working with Python projects, scripts, packages, tools, or publishing workflows that should use uv for package and environment management.
---

# uv

uv is an extremely fast Python package and project manager. It replaces pip,
pip-tools, pipx, pyenv, virtualenv, poetry, twine, and related tools.

Use uv when a project has `uv.lock`, uv-generated `requirements*` files, or a
task involving Python dependencies, environments, scripts, tools, builds, or
publishing. Do not force uv into Poetry or PDM projects identified by
`poetry.lock` or `pdm.lock`.

## Core workflows

### Scripts

Use for standalone Python files. Prefer `uv run script.py`,
`uv run --with <package> script.py`, and inline metadata via `uv add --script`.

### Projects

Use when there is a `pyproject.toml`, `uv.lock`, or a new project:

```bash
uv init
uv add requests
uv add --dev pytest
uv lock
uv sync
uv run <command>
```

Use `uv run`, not direct `python`. Use `--group`, `--dev`, `--optional`,
`--bounds`, and `--upgrade-package` when the dependency target requires them.

### Python versions

Use uv instead of pyenv: `uv python install`, `uv python upgrade`,
`uv python pin`, and `uv python pin --global`. Python upgrades are stable in
uv 0.10+. Tools respect global pins unless `--python` is supplied.

### Workspaces

Use workspaces for monorepos that should share one `uv.lock`. Use
`uv workspace list`, `uv workspace dir`, and `uv run --package <name>`. Prefer
path dependencies when members need separate environments or incompatible
`requires-python`.

### Tools

Use `uvx` / `uv tool run` for isolated tools and `uv run` for project tools:

```bash
uvx ruff check .
uv tool install ruff
uv tool upgrade ruff
```

Use `uv tool install` only when persistent installation is requested. Use
`--with` / `--with-executables-from` for related packages and executables.

### Build, version, and publish

Use `uv build`, `uv build --no-sources`, `uv version`, and `uv publish` for
release workflows. `uv publish` supports trusted publishing, credential env
vars, custom index `publish-url`, and PEP 740 attestations.

### Private indexes and authentication

Use `[[tool.uv.index]]` for private indexes. Prefer named explicit indexes and
`tool.uv.sources` pins. uv uses first-index resolution by default; avoid unsafe
strategies unless explicitly accepted. Use `UV_INDEX_<NAME>_USERNAME/PASSWORD`
or `uv auth` for credentials.

## Legacy pip interface

Use `uv venv`, `uv pip install`, `uv pip compile`, and `uv pip sync` only for
legacy `requirements.txt` workflows or manual environments. Do not introduce new
`requirements.txt` files unless required. In uv 0.10+, `uv venv` requires
`--clear` to remove an existing environment.

## Preview features

Do not recommend preview features by default. They require `--preview`,
`UV_PREVIEW=1`, or `--preview-features`.

Preview areas include `uv upgrade`, `uv workspace metadata`, `uv format`,
`uv audit`, `pylock.toml`, malware checks, native auth, and JSON output.
Formatting guidance belongs in the ruff skill.

## Reference

For detailed changes, changed behavior, and source URLs, read the reference file.
Official uv docs: https://docs.astral.sh/uv/llms.txt
