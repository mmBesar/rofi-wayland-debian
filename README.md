# Rofi with Wayland Support - Debian Packages

[![Build Status](https://github.com/mmBesar/rofi-wayland-debian/actions/workflows/build-multi-deb.yml/badge.svg)](https://github.com/mmBesar/rofi-wayland-debian/actions)
[![Latest Release](https://img.shields.io/github/v/release/mmBesar/rofi-wayland-debian)](https://github.com/mmBesar/rofi-wayland-debian/releases/latest)

**Unofficial Debian packages** for [Rofi](https://github.com/davatorium/rofi) with official Wayland support.

> **⚠️ Important:** This repository only provides Debian packaging. All credit for Rofi itself goes to the original developers at [davatorium/rofi](https://github.com/davatorium/rofi).

## About

This repository automatically builds Debian packages from the official [davatorium/rofi](https://github.com/davatorium/rofi) repository, which now includes merged Wayland support. The packages are built weekly and on every commit to ensure you get the latest features and bug fixes.

### Features

- ✅ **Official Wayland support** via layer shell protocol
- ✅ **X11/XCB support** (dual backend)
- ✅ **Automatic backend detection** based on your session
- ✅ **All standard rofi features** (run, drun, window, ssh, keys, filebrowser modes)
- ✅ **Multi-Debian support** (Bookworm, Trixie, Sid)
- ✅ **Weekly automated builds** to stay current with upstream

## Quick Installation

### Prerequisites
```bash
sudo apt update
sudo apt install curl
```

### Debian 12 (Bookworm)
```bash
wget $(curl -s https://api.github.com/repos/mmBesar/rofi-wayland-debian/releases/latest | grep "browser_download_url.*bookworm.*\.deb" | grep -v "dbgsym" | cut -d '"' -f 4)
sudo apt install ./rofi-wayland_*bookworm*.deb
```

### Debian 13 (Trixie)
```bash
wget $(curl -s https://api.github.com/repos/mmBesar/rofi-wayland-debian/releases/latest | grep "browser_download_url.*trixie.*\.deb" | grep -v "dbgsym" | cut -d '"' -f 4)
sudo apt install ./rofi-wayland_*trixie*.deb
```

### Debian Sid (Unstable)
```bash
wget $(curl -s https://api.github.com/repos/mmBesar/rofi-wayland-debian/releases/latest | grep "browser_download_url.*sid.*\.deb" | grep -v "dbgsym" | cut -d '"' -f 4)
sudo apt install ./rofi-wayland_*sid*.deb
```

## Manual Installation

1. Go to the [Releases page](https://github.com/mmBesar/rofi-wayland-debian/releases/latest)
2. Download the appropriate `.deb` file for your Debian version:
   - `rofi-wayland_*~bookworm*.deb` for Debian 12
   - `rofi-wayland_*~trixie*.deb` for Debian 13
   - `rofi-wayland_*~sid*.deb` for Debian Sid
3. Install: `sudo apt install ./rofi-wayland_*.deb`

## Usage

Rofi automatically detects whether you're running Wayland or X11:

```bash
# Application launcher
rofi -show drun

# Window switcher  
rofi -show window

# Run command
rofi -show run

# Force X11 backend (if needed)
rofi -show drun -x11
```

## Configuration

Rofi configuration works exactly as documented in the [official documentation](https://davatorium.github.io/rofi/). Your existing rofi configs should work without changes.

Default config location: `~/.config/rofi/config.rasi`

## Troubleshooting

### Package Conflicts
If you have the official `rofi` package installed:
```bash
sudo apt remove rofi
sudo apt install ./rofi-wayland_*.deb
```

### Missing Dependencies
If you get dependency errors during installation:
```bash
sudo apt install -f
```

### Wayland Issues
- Ensure you're running a Wayland compositor that supports layer-shell protocol
- Popular compositors with layer-shell support: Sway, Hyprland, River, Wayfire
- GNOME Wayland has limited support - X11 backend might work better

### Theme Issues
If themes don't work properly:
```bash
rofi-theme-selector
```

## Building from Source

If you want to build the packages yourself:

```bash
git clone https://github.com/mmBesar/rofi-wayland-debian.git
cd rofi-wayland-debian
# GitHub Actions will automatically build on push
```

## License and Attribution

### This Repository (Packaging)
- **License:** MIT License
- **Copyright:** 2025 mmBesar
- **Purpose:** Debian packaging only

### Original Rofi Project
- **Repository:** [davatorium/rofi](https://github.com/davatorium/rofi)
- **License:** MIT License  
- **Copyright:** 2012-2024 Dave Davenport and contributors
- **All credit for Rofi functionality goes to the original developers**

### Important Legal Notes

- This repository **only provides packaging** - no modifications to Rofi source code
- All Rofi functionality, features, and code belong to the original [davatorium/rofi](https://github.com/davatorium/rofi) project
- We build directly from the official upstream repository
- This is an **unofficial** packaging effort, not affiliated with the Rofi developers
- If you encounter bugs with Rofi functionality (not packaging), please report them to the [upstream repository](https://github.com/davatorium/rofi/issues)

## Support

### For Rofi Issues (Functionality, Features, Bugs)
- **Official Documentation:** https://davatorium.github.io/rofi/
- **Official Repository:** https://github.com/davatorium/rofi
- **Official Issues:** https://github.com/davatorium/rofi/issues

### For Packaging Issues (Installation, Dependencies, Debian-specific)
- **This Repository Issues:** https://github.com/mmBesar/rofi-wayland-debian/issues
- **Discussions:** Use GitHub Discussions for questions

## Contributing

Contributions to the **packaging** are welcome:
- Improve Debian packaging scripts
- Fix dependency issues
- Enhance documentation
- Test on different Debian versions

**Do not** report Rofi functionality issues here - those belong in the upstream repository.

## Acknowledgments

- **Dave Davenport** and all contributors to the original [Rofi project](https://github.com/davatorium/rofi)
- **lbonn** for the original Wayland implementation that was later merged upstream
- The **Debian** community for packaging standards and tools

## Disclaimer

This is an **unofficial** packaging project. Use at your own risk. The maintainer is not responsible for any issues arising from the use of these packages. Always backup your system before installing unofficial packages.

For production environments, consider using the official Debian repositories or building from source following the [official installation guide](https://davatorium.github.io/rofi/INSTALL/).
