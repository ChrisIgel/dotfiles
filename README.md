# dotfiles

## Setup

```bash
sudo dnf install -y chezmoi whiptail
chezmoi init --apply <your-github-username>
~/.bootstrap/fedora.sh
```

The bootstrap script will prompt you to select which tasks to perform.
All tasks are enabled by default. Use the interactive menu to select which tasks to skip.
