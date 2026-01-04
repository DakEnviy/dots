# Configuration Documentation

This document provides detailed information about each configuration file managed by this dotfiles repository.

## Fish Shell

### Core
- Modular config structure (separate files in `user.{functions,conf.d,completions}/`)
- Kawasaki theme with time display
- Custom colors: blue commands, white comments
- Hybrid Vi/Emacs key bindings, block cursor
- `~/.local/bin` added to PATH

### Plugins (fisher)
- `theme-kawasaki`, `z` (smart cd), `nvm.fish`
- `fifc` (FZF completion) — if FZF is installed
- `fzf.fish` (file/history search) — if FZF, fd, bat are installed

### FZF Integration
- Hidden files enabled, bat previews, Vim editor
- Eza directory previews, Delta diff highlighting (if installed)

### Tool Integrations
- **bat**: TwoDark theme, man pages via bat, `bathelp` alias
- **brew**: Shell environment setup
- **chezmoi**: `ch` alias
- **eza**: `ll`, `lla`, `llt` functions (icons, octal perms, tree)
- **go**: `GOPATH=~/.go`, bin in PATH
- **gpg**: `GPG_TTY`, `bw-gpg-import`/`bw-gpg-choose` functions (Bitwarden integration)
- **kubectl**: `k` alias
- **podman**: `docker` alias
- **python3** (macOS): USER_BASE in PATH
- **ranger**: Changes to last visited directory on exit
- **ripgrep+delta**: `rgd` function (search with delta output)
- **rust**: `CARGOPATH=~/.cargo`, bin in PATH
- **starship**: Auto-init in interactive sessions
- **tmux**: `tn` alias (PID-based session), auto-kill on exit
- **vim**: `EDITOR` variable
- **yc**: `ycs3` alias (aws CLI + Yandex S3 endpoint, requires aws-cli)

## Starship

### Notable Features
- Exit status in right prompt
- Vi mode indicators (different symbols for modes)
- Long paths: 100 chars, no repo truncation
- Detailed Git status with counts
- Time and sudo indicators enabled

See [`dot_config/starship.toml.tmpl`](dot_config/starship.toml.tmpl) for full configuration.

## Hyper

### Notable Features
- **Font**: FiraCode Nerd Font, 15px
- **Theme**: Night Owl (via plugin)
- **Plugins**: hyperborder (gradient border), hyperminimal
- **Custom colors**: Pink cursor with selection, black bg
- **Settings**: Ligatures disabled, preserve CWD, alt as meta

See [`dot_hyper.js.tmpl`](dot_hyper.js.tmpl) for full configuration.

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
- **Editing**: Easy Align (visual alignment), Wayland clipboard
- **Syntax**: Polyglot (multi-language), chezmoi, Sage, KDL support

### Notable Features
- Line numbers (relative in normal mode)
- 4-space indent, smart tabs, auto-indent
- Custom keybindings: `,<space>` (clear search), `,c`/`,b` (system clipboard)

See [`dot_vimrc.tmpl`](dot_vimrc.tmpl) for full configuration.

## Tmux

### Plugins (TPM)
- **tmux-yank**: Enhanced clipboard integration

### Notable Features
- Prefix: `C-a` (instead of `C-b`), mouse enabled, 256 colors
- **Vi mode**: Vim splits (`v`/`s`), navigation (`h/j/k/l`), copy mode keybindings
- Custom status bar: uptime, time, user@host (top position, dual-line)

See [`dot_tmux.conf.tmpl`](dot_tmux.conf.tmpl) for full configuration.

## Ranger

### Configuration
- Devicons plugin (file icons, auto-installed)
- Image preview via Kitty (if installed)

See [`dot_config/ranger/rc.conf.tmpl`](dot_config/ranger/rc.conf.tmpl) for full configuration.

## Python/pip

### Configuration
- Allow pip installs outside virtual environments (for system-wide user tools)
- Install to user directory by default

See [`dot_config/pip/pip.conf.tmpl`](dot_config/pip/pip.conf.tmpl) for configuration.
