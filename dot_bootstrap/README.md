# Fedora Bootstrap Scripts

This directory contains scripts and configuration for automated Fedora workstation setup using chezmoi.

## Files

### `executable_fedora.sh.tmpl`

Main bootstrap script. Handles:

- System configuration (fonts, GNOME, GRUB)
- Repository setup (VS Code, COPR)
- Package installation
- Optional components: GitHub SSH setup, JetBrains Toolbox, Flatpak apps

**Execution:** `chezmoi apply` or manually run `bash executable_fedora.sh.tmpl`

### `fedora.conf`

Configuration file containing:

- Git identity (from chezmoi variables)
- External URLs and API endpoints
- System paths
- COPR repository list
- System packages to install (organized by category)
- Flatpak applications list
- JetBrains dependencies

**Advantages:**

- Easy to modify package lists without touching the script
- Clear organization and comments for each section
- Single source of truth for all configurable values

### `dconf.ini`

GNOME desktop configuration (dconf settings). Applied during setup.

### `snapper_root`

Snapper configuration template for btrfs snapshots on root filesystem.

## Workflow

1. **Configuration Phase** (`fedora.conf`)
   - Lists all packages, apps, and URLs
   - User can easily customize before running

2. **Execution Phase** (`executable_fedora.sh.tmpl`)
   - Sources configuration
   - Interactively prompts user for task selection
   - Executes setup in logical order:
     - System config → Repos → Packages → Optional components

3. **Task Selection**
   - GitHub SSH & Token Setup (optional)
   - JetBrains Toolbox (optional)
   - Flatpak Applications (optional)

## Adding/Removing Packages

### Adding a Package

1. Open `fedora.conf`
2. Add to appropriate array:
   - `SYSTEM_PACKAGES` - system-wide packages
   - `FLATPAK_APPS` - Flatpak applications
   - `COPR_REPOS` - COPR repositories
3. Save and re-run bootstrap

### Adding a COPR Repository

1. Add to `COPR_REPOS` array in `fedora.conf`
2. Re-run bootstrap

## Task Selection

Task selection is controlled interactively via the whiptail menu that appears when the script runs.
All optional components (GitHub SSH, JetBrains Toolbox, and Flatpak apps) default to enabled but can be deselected during the setup prompt.

## Chezmoi Integration

These files are managed by chezmoi:

- `fedora.conf` - processed through chezmoi templates for git identity
- `executable_fedora.sh.tmpl` - template syntax for git variables
- `dconf.ini` - static configuration

Run with: `chezmoi apply`

## Troubleshooting

**Config file not found:**

```bash
ls -la dot_bootstrap/fedora.conf  # Check file exists
```

**Permission denied:**

```bash
chmod +x dot_bootstrap/executable_fedora.sh.tmpl
```

**SSH key setup fails:**

- Ensure `~/.ssh` directory exists and has 700 permissions
- Check GitHub token has `admin:public_key` permission

**COPR repo fails:**

- Some COPR repos may be temporary or architecture-specific
- Check active repos: `dnf copr list`
