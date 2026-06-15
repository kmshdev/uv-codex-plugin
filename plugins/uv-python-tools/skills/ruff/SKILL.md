---
name: ruff
description: Use when linting, formatting, or fixing Python code with ruff or migrating from Black, Flake8, or isort.
---

# ruff

Ruff is an extremely fast Python linter and code formatter. It replaces Flake8,
isort, Black, pyupgrade, autoflake, and dozens of other tools.

## When to use ruff

Always use ruff for Python linting and formatting, especially if you see:

- A `[tool.ruff]` section in `pyproject.toml`.
- A `ruff.toml` or `.ruff.toml` configuration file.

Avoid unnecessary changes:

- Do not format unformatted code. If `ruff format --diff` shows changes
  throughout an entire file, the project likely is not using ruff for formatting.
  Skip formatting to avoid obscuring actual changes.
- Scope fixes to code being edited. Use `ruff check --diff` to see fixes
  relevant to the code you are changing. Only apply fixes to files you are
  modifying unless the user explicitly asks for broader fixes.

## How to invoke ruff

- `uv run ruff ...`: use when ruff is in the project's dependencies to ensure
  you use the pinned version.
- `uvx ruff ...`: use when ruff is not a project dependency, or for quick
  one-off checks.
- `ruff ...`: use if ruff is installed globally.

## Commands

### Linting

```bash
ruff check .
ruff check path/to/file.py
ruff check --fix .
ruff check --fix --unsafe-fixes .
ruff check --watch .
ruff check --select E,F .
ruff check --ignore E501 .
ruff rule E501
ruff linter
```

### Formatting

```bash
ruff format .
ruff format path/to/file.py
ruff format --check .
ruff format --diff .
```

## Configuration

Ruff is configured in `pyproject.toml` or `ruff.toml`.

```toml
[tool.ruff.lint]
select = ["E", "F", "I", "UP"]
ignore = ["E501"]

[tool.ruff.lint.isort]
known-first-party = ["myproject"]
```

## Migrating from other tools

### Black to ruff format

```text
black .                       -> ruff format .
black --check .               -> ruff format --check .
black --diff .                -> ruff format --diff .
```

### Flake8 to ruff check

```text
flake8 .                      -> ruff check .
flake8 --select E,F .         -> ruff check --select E,F .
flake8 --ignore E501 .        -> ruff check --ignore E501 .
```

### isort to ruff check

```text
isort .                       -> ruff check --select I --fix .
isort --check .               -> ruff check --select I .
isort --diff .                -> ruff check --select I --diff .
```

## Common patterns

Apply lint fixes before formatting. Lint fixes can change code structure, such
as reordering imports, which formatting then cleans up.

```bash
ruff check --fix .
ruff format .
```

Preview unsafe fixes before applying them. Ruff marks some fixes as unsafe
because they may change behavior, not just style. For example, removing unused
imports could break code that relies on import side effects.

```bash
ruff check --fix --unsafe-fixes --diff .
ruff check --fix --unsafe-fixes .
```

Always review changes before applying `--unsafe-fixes`:

- Use `ruff rule <CODE>` to understand why the fix is considered unsafe.
- Verify the fix does not violate those assumptions in the code.

## Documentation

For detailed information, read the official ruff documentation:

- https://docs.astral.sh/ruff/
