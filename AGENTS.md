# Repository Guidelines

## Architecture and Layout

This is the chezmoi source state for macOS and Ubuntu. Edit files here, never rendered files in `$HOME`.

- On `chezmoi init` (or a command using `--init`), `.chezmoi.yaml.tmpl` generates the chezmoi config before the target state is computed. It explicitly loads `.chezmoidata/apps.yaml` and `.chezmoidata/package_managers.yaml` through `include | fromYaml`, then computes `.configure`, `.binaries`, and `.packages`.
- Bootstrap is iterative: the first `chezmoi init --apply` can render `run_after_install_packages.sh.tmpl`, which installs missing packages and writes `.reinit`; `bootstrap.sh` repeats `chezmoi init --apply` while that marker exists so newly installed binaries are detected. Preserve this contract.
- `.chezmoidata/apps.yaml` is the app registry. App configs live under `dot_config/`; Fish integrations are in `dot_config/private_fish/user.conf.d/`.
- `dot_*`, `private_*`, and `.tmpl` are behavioral attributes; prefix order matters. `.chezmoiexternal.yaml` is implicitly templated, and its keys plus `.chezmoiignore` use target paths.
- `run_after_*` runs after target updates. `run_onchange_*` reruns when its rendered content differs from the content of its last successful execution.

## Change Rules

- Register apps with a unique lowercase `exec`, clear `name`/`desc`, accurate `conf`, and supported install methods. `conf: true` enables `.configure.<exec>`.
- Preserve install priority: platform manager, Cargo, script, external. `apt!`/`brew!` are pre-install dependencies; `script!` is post-install. Plain `brew` values are formulas; values beginning with `brew`/`cask` or spanning lines are raw Brewfile entries.
- Every app config must be `.tmpl` and guarded by `{{ if .configure.<exec> -}}`. Cross-tool integrations check both `.configure.<dependency>` (when that dependency has `conf: true`) and `.binaries.<dependency>`. Check an app's own binary only when absence would break a runtime command, not merely to render its config.
- When an executable might not yet be on `PATH`, use its `.binaries.<exec>` path in `run_*` scripts, non-primary shells, and early initialization. Guard platform behavior with `.chezmoi.os`, `.chezmoi.osRelease`, or `.hostType`.
- In `.chezmoi.yaml.tmpl`, expose reusable values under `data`, use `prompt*Once`, use `unsafe` when empty values must prompt again, and clear app-specific values when disabled.

## Code Style

- **Templates:** Keep outer guards at column zero. Use `{{-`/`-}}` only after inspecting rendered whitespace. Follow nearby `get`, `dig`, `joinPath`, `quote`, and `toYaml | trim | nindent` patterns; align wrapped pipelines and conditions.
- **End of file:** End every text source file, including `.tmpl` files, with a newline. When changing template guards or whitespace trimming, verify that every non-empty rendered file also ends with a newline.
- **YAML:** Use two spaces and no tabs. In `apps.yaml`, order fields `name`, `desc`, `exec`, `conf`, `install`, then list install methods by priority.
- **Shell:** `bootstrap.sh` stays POSIX `sh` with `set -e`; lifecycle scripts use `#!/usr/bin/env bash` and `set -euo pipefail`. Indent four spaces, quote expansions and paths, keep heredoc delimiters unindented, and make scripts idempotent.
- **Fish:** Keep one integration per `<feature>.fish.tmpl` and indent four spaces. Use `set -l` for locals, `-g` for session globals, `-gx` for exports, and `-U` only for intentional universal state. Use snake_case variables and `__`-prefixed private helpers. Prefer aliases for literal shortcuts and functions for arguments or state. Guard interactive setup with `status is-interactive`; run `fish_indent` only after rendering.
- **TOML/configs:** Group related settings with blank lines and preserve local quote style. Align `=` only in compact adjacent groups. Ghostty keys remain kebab-case `key = value`.
- **Lua:** Use four spaces, snake_case locals, early returns, spaced operators, and trailing commas in multiline tables.
- **Vim/tmux/Git:** Group behavior under short comments, use four-space nested indentation, and preserve native syntax. Keep TPM initialization at the bottom of `dot_tmux.conf.tmpl`.
- **Imported assets:** Do not reformat `OneHalfLight.tmTheme` or other vendored themes; preserve upstream tabs, metadata, and structure.

## Chezmoi Safety Boundary

- Normal add, edit, configure, fix, or test requests authorize source-repository changes only—not destination files, generated chezmoi config, packages, plugins, login shell, or other host state.
- Never run `bootstrap.sh`, `chezmoi apply`, `chezmoi update`, `chezmoi init`, or equivalent host-mutating commands unless the user requests that exact action in the current turn.
- Prefer non-destination-mutating checks: `git diff --check`, parsers, linters, targeted `chezmoi execute-template`/`cat`, `chezmoi status`, `chezmoi diff`, and `chezmoi apply --dry-run --verbose`. Render templates before language-specific linting.
- First inspect templates for hooks, `output`, password-manager access, prompts, externals, or other side effects. Dry-run skips chezmoi scripts but not configured hooks.
- Report checks run and the exact manual apply command. After an authorized apply, run `chezmoi verify`; a second dry run should show no unexpected work. Never infer host-mutation permission from earlier turns.

## Security and Review

Never commit rendered configs, Bitwarden output, credentials, private keys, `BW_SESSION`, or host-specific state. Prefer pinned external releases and checksums; justify mutable URLs and set `refreshPeriod`.

Use Conventional Commits, e.g. `feat(yazi): add plugin` or `fix(fish): resolve binary path`. PRs should state behavior, affected platforms, prompt/package changes, validation, and screenshots for visual changes.
