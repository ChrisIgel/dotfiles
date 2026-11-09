# dotfiles

## Setup

```bash
sudo dnf install -y chezmoi whiptail
chezmoi init --apply <your-github-username>
~/.bootstrap/fedora.sh
```

The bootstrap script will prompt you to select which tasks to perform:

- **GitHub SSH & Token Setup** — SSH key generation, GitHub token validation, and remote configuration
- **JetBrains Toolbox** — Download and launch JetBrains Toolbox
- **Flatpak Applications** — Flathub setup and application installations

All tasks are enabled by default. Use the interactive menu to select which tasks to skip.
