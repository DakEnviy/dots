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
- [K9s](#k9s)
- [Python/pip](#pythonpip)

## Fish Shell

### Core
- Modular config structure (separate files in `user.{functions,conf.d,completions}/`)
- Kawasaki theme with time display
- Bright-cyan bold operators
- Hybrid Vi/Emacs key bindings, block cursor
- Terminal title with the abbreviated current directory and command name
- `~/.local/bin` added to PATH

### Plugins (fisher)
- `theme-kawasaki`, `z` (smart cd), `nvm.fish`
- `fish-eza` (ls replacement), shared grouping/icons/hyperlinks options and `llt` tree alias — if eza is installed
- `fifc` (FZF completion) — if FZF is installed
- `fzf.fish` (file/history search) — if FZF, fd, bat are installed

### FZF Integration
- Light theme, cycling, reverse layout, wrapped previews, hidden files enabled
- Bat previews, Vim editor (if installed)
- Eza directory previews, Delta diff highlighting (if installed)

### Tool Integrations
- **bat**: OneHalfLight theme, man pages via bat, `bathelp` alias
- **brew**: Shell environment setup
- **chezmoi**: `ch` alias and update reminder
- **go**: `GOPATH=~/.go`, bin in PATH
- **gpg**: `GPG_TTY`, `bw-gpg-import`/`bw-gpg-choose` functions (Bitwarden integration)
- **k9s**: `K9S_CONFIG_DIR=~/.config/k9s`
- **kubectl**: `k` alias
- **npm**: `ni`/`ns` install aliases with ad blocking, no audit and offline preference
- **nvm**: LTS default, checks `.nvmrc` on startup and directory changes
- **podman**: `docker` alias
- **python3** (macOS): USER_BASE in PATH
- **ripgrep+delta**: `rgd` function (search with delta output)
- **rust**: `CARGOPATH=~/.cargo`, bin in PATH
- **starship**: Auto-init in interactive sessions
- **tmux**: `tn` alias (PID-based session), auto-kill on exit
- **vim**: `EDITOR` variable
- **vivid**: Generates ANSI-based `LS_COLORS` matching the terminal theme
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
- **Font**: FiraCode Nerd Font Mono, size 15, thickened
- **Theme**: Zenwritten Light
- **Background**: Semi-transparent (95%) with blur effect
- **Settings**: Ligatures disabled, mouse hidden while typing, custom padding
- **Shell**: SSH environment integration enabled (`ssh-env`)
- **MacOS**: Tabs-style titlebar

See [`dot_config/ghostty/config.tmpl`](dot_config/ghostty/config.tmpl) for full configuration.

## GPG

### Configuration
- Keyserver: `hkps://keys.openpgp.org`

### Fish Integration
- **bw-gpg-import**: Imports GPG key from Bitwarden notes, sets ultimate trust
- **bw-gpg-choose**: Keeps the subkey selected via FZF and removes the other local subkeys and primary secret key

See [`private_dot_gnupg/gpg.conf.tmpl`](private_dot_gnupg/gpg.conf.tmpl) for configuration.

## Git

### Smart Integrations
- **GPG**: On desktops, derives the signing key ID from a Bitwarden note and enables commit/tag signing
- **Delta**: Pager with dark theme, line numbers, navigation (if installed)
- **Vim**: Editor integration (if installed)

### Notable Features
- **Defaults**: `main` initial branch, autosquash for interactive rebases, LF normalization on commit, `diff3` conflicts, moved-line highlighting
- **Aliases**: `st`/`ci`/`co`/`br`, `edit`/`amend`, `unstage`
- **Branch workflow**: `m` (checkout origin's default branch), `prm` (rebase on it), `new` (new branch from it)
- **WIP shortcuts**: `wip` stages all changes and commits without hooks or GPG signing; `unwip` restores them as unstaged changes
- Extension support via `~/.gitconfig-extension`

See [`dot_gitconfig.tmpl`](dot_gitconfig.tmpl) for full configuration.

## Vim

### Plugins (vim-plug)
- **Theme**: vim-one (`one` color scheme; light/dark flavor is not forced), transparent background
- **Navigation**: EasyMotion (2-char search, line jumps, word navigation)
- **Files**: yazi.vim (`-`/`_` keybindings) — if yazi is installed
- **Editing**: Easy Align (`ga` in normal/visual mode), Wayland clipboard
- **Syntax**: Polyglot (multi-language), chezmoi, Sage, KDL support

### Notable Features
- **Display**: Relative line numbers in the active window outside insert mode, no line wrapping, search highlighting, buffer-aware terminal title
- **Indentation**: 4 spaces, smart tabs and smart indent
- **Custom keybindings**: `,<space>` (clear search), `,c`/`,b` (system clipboard)
- **ripgrep**: Case-sensitive `grepprg` with vimgrep format and symlink following (if installed)

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
- `full-border`, `smart-enter`, `chmod`, `mount`
- `git` (file status icons) — if git is installed

### Notable Features
- **Theme**: OneHalfLight syntax highlighting (same as bat)
- **UI**: Full border, custom status bar with user:group and mtime
- **Settings**: Hidden files shown, size linemode
- **Git**: Status icons, `gr` to jump to git root
- **Keymaps**: `l` (smart-enter), `cm` (chmod), `M` (mount), `Ctrl+o` (macOS Quick Look)

See [`dot_config/yazi`](dot_config/yazi) for full configuration.

## K9s

### Configuration
- **Theme**: Official One Light skin

See [`dot_config/k9s`](dot_config/k9s) and [`dot_config/private_fish/user.conf.d/k9s.fish.tmpl`](dot_config/private_fish/user.conf.d/k9s.fish.tmpl) for the configuration.

## Python/pip

### Configuration
- Allow user-level pip installs outside virtual environments on externally managed Python installations
- Install to user directory by default

See [`dot_config/pip/pip.conf.tmpl`](dot_config/pip/pip.conf.tmpl) for configuration.

