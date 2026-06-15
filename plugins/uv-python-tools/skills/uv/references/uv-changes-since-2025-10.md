# uv changes since the original Claude plugin

The original `astral-sh/claude-code-plugins` uv skill first landed on
2025-10-23 in commit `f9d25e0`. A later 2026-02-27 commit only added the skill
`name` frontmatter. This reference summarizes uv changes that matter for this
Codex plugin as of uv `0.11.21`, published 2026-06-11.

## How to use this reference

Use this file as deferred context for the uv skill. Keep `SKILL.md` concise and
operational; move detailed release history, source URLs, and edge-case notes
here. Open this reference before:

- updating uv workflow guidance in `SKILL.md`;
- answering what changed in uv since the source plugin;
- deciding whether a workflow is stable or preview-only;
- adding guidance for workspaces, Python upgrades, publishing, indexes, auth,
  or preview features.

Do not copy the entire reference into `SKILL.md`. Promote only short,
frequently needed operational rules into the active skill.

## Sources inspected

- Original plugin source: `astral-sh/claude-code-plugins`, uv skill in the
  Astral plugin skill directory.
- Current uv documentation index:
  https://docs.astral.sh/uv/llms.txt
- uv feature overview:
  https://docs.astral.sh/uv/getting-started/features/index.md
- Projects guide:
  https://docs.astral.sh/uv/guides/projects/index.md
- Scripts guide:
  https://docs.astral.sh/uv/guides/scripts/index.md
- Tools guide:
  https://docs.astral.sh/uv/guides/tools/index.md
- Workspaces:
  https://docs.astral.sh/uv/concepts/projects/workspaces/index.md
- Project dependencies:
  https://docs.astral.sh/uv/concepts/projects/dependencies/index.md
- Locking and syncing:
  https://docs.astral.sh/uv/concepts/projects/sync/index.md
- Running commands:
  https://docs.astral.sh/uv/concepts/projects/run/index.md
- Creating projects:
  https://docs.astral.sh/uv/concepts/projects/init/index.md
- Building and publishing packages:
  https://docs.astral.sh/uv/guides/package/index.md
- Package indexes:
  https://docs.astral.sh/uv/concepts/indexes/index.md
- Authentication:
  https://docs.astral.sh/uv/concepts/authentication/index.md
- Preview features:
  https://docs.astral.sh/uv/concepts/preview/index.md
- uv GitHub releases:
  https://github.com/astral-sh/uv/releases

## Release window

The original skill was authored just before uv `0.9.6`. Relevant releases since
then include:

- `0.9.6` on 2025-10-29
- `0.10.0` on 2026-02-05
- `0.11.0` on 2026-03-23
- `0.11.21` on 2026-06-11

There were 59 uv releases from `0.9.6` through `0.11.21` in the researched
window.

## Stable workflow updates to reflect in the skill

### Python versions

uv `0.10.0` stabilized Python upgrades:

- `uv python upgrade`
- `uv python install --upgrade`
- transparent Python patch upgrades for virtual environments

Tools now respect a global Python pin from `uv python pin --global` unless the
tool invocation specifies `--python`.

### Projects and dependencies

Current project guidance should include:

- `uv lock` for lockfile creation and refresh.
- `uv tree` for dependency-tree inspection.
- `uv add --dev`, `uv add --group`, and `uv add --optional`.
- `dependency-groups` as local development dependency groups.
- `project.optional-dependencies` as published extras.
- `tool.uv.sources` for alternate development sources.
- `uv add --bounds` and the `add-bounds` setting, stable since `0.10.0`.
- `uv add <requirement> --upgrade-package <name>` for upgrading a locked
  package while changing constraints.

### Workspaces

Workspaces should be documented as a monorepo workflow with:

- One shared `uv.lock`.
- `tool.uv.workspace.members`.
- `tool.uv.sources.<package> = { workspace = true }`.
- `uv run --package <member>` and `uv sync --package <member>`.
- `uv workspace list` and `uv workspace dir`, stable since `0.10.0`.

Path dependencies remain preferable when packages need independent virtual
environments or incompatible Python-version ranges.

### Tools

Current tool guidance should include:

- `uv tool upgrade`.
- `uv tool update-shell`.
- `uv tool install --with`.
- `uv tool install --with-executables-from`.
- The distinction between isolated tools (`uvx` / `uv tool run`) and
  project-bound commands (`uv run pytest`, `uv run mypy`).

### Build and publish

uv now directly covers workflows that older guidance associated with build or
twine:

- `uv build`.
- `uv build --no-sources` before publishing, to check builds without local
  `tool.uv.sources`.
- `uv version` and `uv version --bump <part>`.
- `uv publish`.
- Trusted publishing from GitHub Actions.
- `UV_PUBLISH_TOKEN`, `UV_PUBLISH_USERNAME`, and `UV_PUBLISH_PASSWORD`.
- `publish-url` on `[[tool.uv.index]]`, then `uv publish --index <name>`.
- Attestation upload when matching PEP 740 attestation files are present.
- `uv publish --no-attestations` when a registry rejects attestations.

### Private indexes and authentication

Current index guidance should include:

- `[[tool.uv.index]]` with a `name` and `url`.
- `explicit = true` for indexes that should only serve pinned packages.
- `tool.uv.sources.<package> = { index = "<name>" }`.
- uv's default first-index strategy, which reduces dependency-confusion risk.
- Avoiding unsafe index strategies unless explicitly requested.
- `UV_INDEX_<NAME>_USERNAME` and `UV_INDEX_<NAME>_PASSWORD`.
- `uv auth` and credential providers such as netrc, keyring, and system-native
  stores.

`0.10.0` changed multi-credential behavior: if multiple stored credentials
match a URL, uv now errors instead of picking the first one. Include a username
explicitly, for example `uv auth token --username user example.com`.

## Changed or breaking behavior

- `uv venv` now requires `--clear` before removing an existing virtual
  environment.
- `--native-tls` is deprecated; use `--system-certs`.
- `uv init --project` is deprecated.
- Multiple indexes with `default = true` now error.
- Explicit indexes must be named.
- Alternative Python implementation executables use implementation names such
  as `pypy3.10` instead of CPython-like names.
- Older Docker image tags such as `bookworm`, `alpine3.21`, and Python 3.8
  variants were removed.

## Preview features

Do not use these as default recommendations. They require `--preview`,
`UV_PREVIEW=1`, or `--preview-features` unless the command itself opts into a
preview behavior:

- `uv upgrade`
- `uv workspace metadata`
- `uv format`
- `uv audit`
- `pylock.toml`
- malware checks
- native auth
- `uv auth helper`
- selected JSON output support

`uv format` uses Ruff formatting behavior and remains preview; the default
plugin guidance should continue sending ordinary formatting work to the ruff
skill.
