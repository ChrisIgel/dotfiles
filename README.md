# dotfiles

## Setup

```bash
sudo dnf install -y chezmoi
chezmoi init --apply <your-github-username>
~/.bootstrap/fedora.sh
```

## Bootstrap skip flags

The bootstrap script supports env vars to skip slow or interactive sections during testing:

| Variable           | Skips                                                                                                                                         |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `SKIP_GITHUB=1`    | SSH key passphrase prompt, GitHub token prompt/validation, SSH key generation, GitHub API upload, `known_hosts` update, chezmoi remote switch |
| `SKIP_JETBRAINS=1` | JetBrains Toolbox download and launch                                                                                                         |
| `SKIP_FLATPAK=1`   | Flathub remote setup and all Flatpak app installs                                                                                             |

Example:

```bash
SKIP_GITHUB=1 SKIP_JETBRAINS=1 SKIP_FLATPAK=1 ~/.bootstrap/fedora.sh
```
