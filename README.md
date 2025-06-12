# Shell Setup

My personal shell environment automation. The script I use to quickly set up a consistent development environment on new machines.

## Overview

This project automates the setup of a modern Zsh shell with Oh My Zsh, Powerlevel10k theme, useful plugins, and essential development tools. Born out of the need to repeatedly configure new development environments, it ensures consistency across macOS, Linux, and WSL systems.

## Features

- **Modular Package Manager Support**: Currently supports Homebrew (macOS), designed for easy extension to APT (Linux/WSL)
- **Oh My Zsh Setup**: Automatic installation and configuration with sensible defaults
- **Powerlevel10k Theme**: Modern, informative terminal prompt
- **Smart Backups**: Never overwrites existing configurations without backup
- **Dry-Run Mode**: See what would be changed before making any modifications
- **Installation Modes**: Choose between minimal essentials or full feature set
- **Clean Configuration Management**: Uses markers for easy reversal and updates

## Quick Start

```bash
git clone https://github.com/marcelwenner/shell-setup.git
cd shell-setup
./install.sh
```

## Installation Options

```bash
./install.sh --dry-run     # Preview changes without applying
./install.sh --minimal     # Essential tools only
./install.sh --full        # Complete setup (default)
./install.sh --update      # Update existing installations
./install.sh -y            # Skip confirmation prompts
```

## What Gets Installed

### Core Tools (always)
- git, zsh, zsh-completions
- fzf (fuzzy finder)
- gum (better CLI prompts)

### Optional Tools (full mode)
Configurable via `config/brew_optionals.txt`

## Architecture

```
shell-setup/
├── install.sh              # Main entry point
├── lib/
│   ├── utils.sh           # Core utilities and logging
│   └── package_managers/  # Pluggable package manager drivers
│       └── pm_brew.sh     # Homebrew implementation
├── config/                # Package and plugin definitions
└── scripts/               # Modular installation steps
```

The modular design makes it straightforward to:
- Add support for new package managers
- Customize tool selections
- Extend functionality without touching core logic

## Customization

Edit configuration files in `config/`:
- `brew_essentials.txt` - Always installed packages
- `brew_optionals.txt` - Full installation packages  
- `omz_plugins.txt` - Oh My Zsh plugins to enable

## Safety Features

- Automatic backup of existing `.zshrc` 
- All changes use marked blocks for clean removal
- Dry-run mode for safe testing
- Complete uninstallation with `./uninstall.sh`

## Extending for Other Systems

Adding APT support example:
1. Create `lib/package_managers/pm_apt.sh` 
2. Implement required functions following the Homebrew driver pattern
3. Detection happens automatically in `lib/utils.sh`

## License

Unlicense - See [LICENSE](LICENSE)
