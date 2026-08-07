# Repository Guidelines

## Architecture

This is the chezmoi source state for macOS and Ubuntu. Edit it, never rendered files in `$HOME`.

- `.chezmoi.yaml.tmpl` loads `.chezmoidata/apps.yaml` and `.chezmoidata/package_managers.yaml`, then computes `.configure`, `.binaries`, and `.packages` before the target state is built.
- Fresh bootstrap is iterative: package installation may write `.reinit`, and `bootstrap.sh` repeats `chezmoi init --apply` until it is absent. Preserve this contract.
- On an already configured machine, reconfigure with `chezmoi init`, complete new prompts, inspect `chezmoi diff`, then run `chezmoi apply`. Do not use `bootstrap.sh` or `.reinit` for this flow.
- `.chezmoidata/apps.yaml` is the app registry. App configs live under `dot_config/`; Fish integrations live under `dot_config/private_fish/user.conf.d/`.
- Use `$osid` (`<os>-<arch>` on macOS, `<os>-<release>-<arch>` on Linux) for platform-specific lookups.
- `dot_*`, `private_*`, and `.tmpl` are behavioral attributes whose order matters. `.chezmoiexternal.yaml` is implicitly templated; its keys and `.chezmoiignore` use target paths.

## Change Rules

- Give each app a unique lowercase `exec`, clear `name`/`desc`, accurate `conf`, and supported install methods. `conf: true` enables `.configure.<exec>`.
- Use an app's optional scalar-valued `path` map only for directories it provides. Keys are `all`, an OS, or `$osid` (most specific wins); resolve relative values from `.chezmoi.homeDir` and keep shared paths such as `.local/bin` in the base search path.
- Preserve install priority: platform manager, Cargo, script, external. `apt!`/`brew!` are pre-install dependencies; `script!` is post-install. Plain `brew` values are formulas; values starting with `brew`/`cask` or spanning lines are raw Brewfile entries.
- Make every app config a `.tmpl` guarded by `{{ if .configure.<exec> -}}`. Cross-tool integrations check `.configure.<dependency>` when applicable and `.binaries.<dependency>`. Check an app's own binary only when its absence would break a runtime command.
- Use `.binaries.<exec>` in lifecycle scripts, non-primary shells, and early initialization when `PATH` may be incomplete. Guard platform behavior with `.chezmoi.os`, `.chezmoi.osRelease`, or `.hostType`.
- In `.chezmoi.yaml.tmpl`, expose reusable values under `data`, use `prompt*Once`, use `unsafe` when an empty value must prompt again, and clear app-specific values when disabled.

## Style

- Keep template outer guards at column zero. Inspect rendered whitespace before using `{{-`/`-}}`; follow nearby template-function and pipeline patterns. End every text source and every non-empty rendered branch with a newline.
- Preserve each file's existing EOF layout: never add or remove a final blank line as incidental cleanup. In particular, do not replace an existing trailing blank line (`\n\n`) with only a final newline (`\n`); verify EOF whitespace after every edit.
- Use two-space YAML without tabs. In `apps.yaml`, order fields `name`, `desc`, `exec`, `conf`, `path`, `install`, then installation methods by priority.
- Keep `bootstrap.sh` POSIX `sh` with `set -e`. Lifecycle scripts use Bash with `set -euo pipefail`; indent four spaces, quote expansions, keep heredoc delimiters unindented, and remain idempotent.
- In Fish, keep one integration per file, indent four spaces, use scoped variables deliberately, and prefer functions when arguments or state are involved. Guard interactive setup and run `fish_indent` only on rendered files.
- Preserve nearby native style in TOML, Lua, Vim, tmux, Git, and other configs. Keep TPM initialization last. Do not reformat vendored themes or imported assets.

## Safety

- Normal change and test requests authorize source-repository edits only—not destination files, generated config, packages, plugins, login shells, or other host state.
- Never run `bootstrap.sh`, `chezmoi init`, `chezmoi apply`, `chezmoi update`, or equivalent host-mutating commands unless the user requests that exact action in the current turn.
- Before reading source state through chezmoi, inspect templates for hooks, `output`, password-manager access, prompts, externals, and other side effects. Dry-run skips chezmoi scripts, not configured hooks.
- Prefer `git diff --check`, parsers, linters, targeted rendering, `chezmoi status`, `chezmoi diff`, and `chezmoi apply --dry-run --verbose`. Lint rendered output rather than mixed template source.
- Report checks run and the exact manual apply sequence. After an authorized apply, run `chezmoi verify`; a second dry run should show no unexpected work.

Never expose or include rendered configs, decrypted output, credentials, private keys, `BW_SESSION`, or host-specific state. Prefer pinned externals and checksums; justify mutable URLs and set `refreshPeriod`.

Do not create commits unless explicitly requested; the user normally commits changes personally.
