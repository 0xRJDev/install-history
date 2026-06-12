# install-history

A small Fish shell script for viewing recent package install history on Arch-based systems.

Designed mainly for **CachyOS / Arch Linux**, it reads your pacman log and shows what packages were installed, upgraded, removed, or reinstalled within the last few days.

It also tries to identify where each package came from:

* `CACHY` — CachyOS repositories
* `ARCH` — Arch official repositories
* `AUR/LOC` — AUR or locally installed packages
* `FLATPAK` — Flatpak history, if available

## Features

* Shows install history from the last `N` days
* Defaults to the last 3 days
* Groups entries by date
* Shows install time
* Shows package name and version
* Detects CachyOS, Arch, AUR/local, and Flatpak entries
* Highlights important system/gaming-related packages
* Supports filtering modes
* Written for Fish shell

## Installation

Clone the repository:

```f
git clone https://github.com/YOUR_USERNAME/install-history.git
cd install-history
```

Copy the script into your local bin folder:

```fish
mkdir -p ~/.local/bin
cp install-history ~/.local/bin/install-history
chmod +x ~/.local/bin/install-history
```

Make sure `~/.local/bin` is in your `PATH`.

For Fish shell, you can check with:

```fish
echo $PATH
```

If needed, add it:

```fish
fish_add_path ~/.local/bin
```

## Usage

Show installs from the last 3 days:

```fish
install-history
```

Show installs from the last 4 days:

```fish
install-history 4
```

Show installs, upgrades, removals, and reinstalls:

```fish
install-history 7 --all
```

Show only important system/gaming-related packages:

```fish
install-history 7 --important
```

Show only AUR/local packages:

```fish
install-history 14 --aur
```

Show only Flatpak history:

```fish
install-history 7 --flatpak
```

Show help:

```fish
install-history --help
```

## Options

| Option        | Description                                                                               |
| ------------- | ----------------------------------------------------------------------------------------- |
| `--installed` | Show installed packages only. This is the default.                                        |
| `--all`       | Show installed, upgraded, removed, and reinstalled packages.                              |
| `--important` | Show packages likely to affect the system, desktop, graphics stack, gaming, audio, or VR. |
| `--aur`       | Show only AUR/local packages.                                                             |
| `--flatpak`   | Show only Flatpak history.                                                                |
| `--help`      | Show usage information.                                                                   |

## Important package tags

The script adds tags to packages that may be relevant when troubleshooting.

Examples:

| Tag        | Meaning                                    |
| ---------- | ------------------------------------------ |
| `graphics` | NVIDIA, Mesa, Vulkan, DXVK, VKD3D          |
| `kernel`   | Linux kernel packages                      |
| `gaming`   | Steam, Wine, Proton, Gamescope, MangoHud   |
| `desktop`  | KDE, Plasma, KWin, Wayland, XWayland, SDDM |
| `audio`    | PipeWire, WirePlumber, ALSA, PulseAudio    |
| `core`     | systemd, glibc, gcc, LLVM, Python, Qt      |
| `portal`   | Flatpak and xdg-desktop-portal             |
| `VR`       | OpenXR, Monado, VR-related packages        |

## Notes

AUR detection is best-effort.

Pacman does not store “AUR” as a package source in `/var/log/pacman.log`, so the script checks whether a package exists in your currently enabled pacman repositories. If it does not, it is marked as `AUR/LOC`.

That means a package may show as `AUR/LOC` if:

* it came from the AUR
* it was installed locally
* it came from a repository you no longer have enabled
* it was removed from your current repositories

## Requirements

* Fish shell
* pacman
* awk
* sort
* Flatpak optional

## Tested on

* CachyOS
* Arch Linux
* Fish shell

## Why?

When something breaks after an update or package install, checking recent changes should be quick.

Instead of digging through `/var/log/pacman.log`, run:

```fish
install-history 7 --important
```

That gives a quick view of recent changes that are most likely to affect graphics, gaming, KDE, Wayland, audio, or core system behaviour.

## License

MIT
