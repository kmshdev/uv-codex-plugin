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

Scripts: use `uv run script.py`, `uv run --with <package> script.py`, and
inline metadata via `uv add --script`.

Projects: start with `uv init`, `uv add`, `uv lock`, `uv sync`, and
`uv run <command>`. Use `uv run`, not direct `python`. Reach for `--group`,
`--dev`, `--optional`, `--bounds`, and `--upgrade-package` when dependency
intent requires them.

Python versions: use `uv python install`, `uv python install --upgrade`,
`uv python upgrade`, `uv python pin`, and `uv python pin --global`. Python
upgrades are stable in uv 0.10+.

Workspaces: use them for monorepos sharing one `uv.lock`. Use
`uv workspace list`, `uv workspace dir`, and `uv run --package <name>`. Prefer
path dependencies for separate environments or incompatible `requires-python`.

Tools: use `uvx` / `uv tool run` for isolated tools and `uv run` for
project-bound tools such as pytest or mypy. Use `uv tool install` only when
persistent installation is requested. Use `uv tool upgrade`,
`uv tool update-shell`, `--with`, and `--with-executables-from` as needed.

Build and publish: use `uv build`, `uv build --no-sources`, `uv version`, and
`uv publish`. Publishing supports trusted publishers, token env vars, custom
index `publish-url`, and PEP 740 attestations.

Private indexes: use `[[tool.uv.index]]`, named explicit indexes, and
`tool.uv.sources` pins. uv defaults to first-index resolution. Use
`UV_INDEX_<NAME>_USERNAME/PASSWORD`, `uv auth`, or credential providers.

## Legacy pip interface

Use `uv venv`, `uv pip install`, `uv pip compile`, and `uv pip sync` only for
legacy `requirements.txt` workflows or manual environments. Do not introduce new
`requirements.txt` files unless required. In uv 0.10+, `uv venv` requires
`--clear` to remove an existing environment.

## Preview features

Do not recommend preview features by default. They require `--preview`,
`UV_PREVIEW=1`, or `--preview-features`. Preview areas include `uv upgrade`,
`uv workspace metadata`, `uv format`, `uv audit`, `pylock.toml`, malware
checks, native auth, and JSON output. Formatting guidance belongs in the ruff
skill.

## Reference

For detailed changes, changed behavior, and source URLs, read
`references/uv-changes-since-2025-10.md`.

Open that reference before changing this skill, when a user asks what changed
in uv since the source plugin, or when a task depends on newer uv behavior.

Official uv docs: https://docs.astral.sh/uv/llms.txt
