# Configuration Documentation

This document provides detailed information about each configuration file managed by this dotfiles repository.

**Table of Contents**
- [Fish Shell](#fish-shell)
- [Starship](#starship)
- [Ghostty](#ghostty)
- [GPG](#gpg)
- [Git](#git)
- [Vim](#vim)
- [Tmux](#tmux)
- [Yazi](#yazi)
- [Python/pip](#pythonpip)

## Fish Shell

### Core
- Modular config structure (separate files in `user.{functions,conf.d,completions}/`)
- Kawasaki theme with time display
- Custom colors: blue commands, white comments
- Hybrid Vi/Emacs key bindings, block cursor
- `~/.local/bin` added to PATH

### Plugins (fisher)
- `theme-kawasaki`, `z` (smart cd), `nvm.fish`
- `eza` (ls replacement) — if eza is installed
- `fifc` (FZF completion) — if FZF is installed
- `fzf.fish` (file/history search) — if FZF, fd, bat are installed

### FZF Integration
- Hidden files enabled, bat previews, Vim editor
- Eza directory previews, Delta diff highlighting (if installed)

### Tool Integrations
- **bat**: TwoDark theme, man pages via bat, `bathelp` alias
- **brew**: Shell environment setup
- **chezmoi**: `ch` alias and update reminder
- **go**: `GOPATH=~/.go`, bin in PATH
- **gpg**: `GPG_TTY`, `bw-gpg-import`/`bw-gpg-choose` functions (Bitwarden integration)
- **kubectl**: `k` alias
- **podman**: `docker` alias
- **python3** (macOS): USER_BASE in PATH
- **ripgrep+delta**: `rgd` function (search with delta output)
- **rust**: `CARGOPATH=~/.cargo`, bin in PATH
- **starship**: Auto-init in interactive sessions
- **tmux**: `tn` alias (PID-based session), auto-kill on exit
- **vim**: `EDITOR` variable
- **yazi**: `y` alias, changes to last visited directory on exit
- **yc**: `ycs3` alias (aws CLI + Yandex S3 endpoint, requires aws-cli)

## Starship

### Notable Features
- Exit status in right prompt
- Vi mode indicators (different symbols for modes)
- Long paths: 100 chars, no repo truncation
- Detailed Git status with counts
- Time and sudo indicators enabled

See [`dot_config/starship.toml.tmpl`](dot_config/starship.toml.tmpl) for full configuration.

## Ghostty

### Notable Features
- **Font**: FiraCode Nerd Font Mono, 15px, thickened
- **Theme**: Night Owl
- **Background**: Semi-transparent (95%) with blur effect
- **Settings**: Ligatures disabled, mouse hidden while typing, custom padding
- **Shell**: SSH integrations enabled
- **MacOS**: Tabs-style titlebar

See [`dot_config/ghostty/config.tmpl`](dot_config/ghostty/config.tmpl) for full configuration.

## GPG

### Configuration
- Keyserver: `hkps://keys.openpgp.org`

### Fish Integration (Desktop only)
- **bw-gpg-import**: Imports GPG key from Bitwarden notes, sets ultimate trust
- **bw-gpg-choose**: Interactive subkey selection via FZF, cleanup unused keys

See [`private_dot_gnupg/gpg.conf.tmpl`](private_dot_gnupg/gpg.conf.tmpl) for configuration.

## Git

### Smart Integrations
- **GPG**: Auto-detects key from Bitwarden, enables commit/tag signing
- **Delta**: Pager with dark theme, line numbers, navigation (if installed)
- **Vim**: Editor integration (if installed)

### Notable Features
- **Branch workflow**: `m` (checkout main/master), `prm` (pull rebase), `new` (branch from main)
- **WIP shortcuts**: `wip` (fast commit bypassing hooks), `unwip` (undo)
- Extension support via `~/.gitconfig-extension`

See [`dot_gitconfig.tmpl`](dot_gitconfig.tmpl) for full configuration.

## Vim

### Plugins (vim-plug)
- **Theme**: OneDark, transparent background
- **Navigation**: EasyMotion (2-char search, line jumps, word navigation)
- **Files**: yazi.vim (`-`/`_` keybindings) — if yazi is installed
- **Editing**: Easy Align (visual alignment), Wayland clipboard
- **Syntax**: Polyglot (multi-language), chezmoi, Sage, KDL support

### Notable Features
- Line numbers (relative in normal mode)
- 4-space indent, smart tabs, auto-indent
- Custom keybindings: `,<space>` (clear search), `,c`/`,b` (system clipboard)
- **ripgrep**: `grepprg` set to rg with vimgrep format (if installed)

See [`dot_vimrc.tmpl`](dot_vimrc.tmpl) for full configuration.

## Tmux

### Plugins (TPM)
- **tmux-yank**: Enhanced clipboard integration

### Notable Features
- Prefix: `C-a` (instead of `C-b`), mouse enabled, 256 colors
- **Vi mode**: Vim splits (`v`/`s`), navigation (`h/j/k/l`), copy mode keybindings
- Custom status bar: uptime, time, user@host (top position, dual-line)

See [`dot_tmux.conf.tmpl`](dot_tmux.conf.tmpl) for full configuration.

## Yazi

### Plugins (ya pkg)
- `full-border`, `smart-enter`, `chmod`
- `git` (file status icons) — if git is installed

### Notable Features
- **Theme**: TwoDark syntax highlighting (same as bat)
- **UI**: Full border, custom status bar with user:group and mtime
- **Settings**: Hidden files shown, size linemode
- **Git**: Status icons, `gr` to jump to git root
- **Keymaps**: `l` (smart-enter), `cm` (chmod), `Ctrl+o` (macOS Quick Look)

See [`dot_config/yazi`](dot_config/yazi) for full configuration.

## Python/pip

### Configuration
- Allow pip installs outside virtual environments (for system-wide user tools)
- Install to user directory by default

See [`dot_config/pip/pip.conf.tmpl`](dot_config/pip/pip.conf.tmpl) for configuration.

