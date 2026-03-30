# Rofi with Wayland Support — Debian Packages

[![Stable Release](https://img.shields.io/github/v/release/mmBesar/rofi-wayland-debian?label=stable&color=brightgreen)](https://github.com/mmBesar/rofi-wayland-debian/releases/latest)
[![Dev Release](https://img.shields.io/github/v/release/mmBesar/rofi-wayland-debian?include_prereleases&label=dev&color=orange)](https://github.com/mmBesar/rofi-wayland-debian/releases)
[![Stable Build](https://github.com/mmBesar/rofi-wayland-debian/actions/workflows/build-stable.yml/badge.svg)](https://github.com/mmBesar/rofi-wayland-debian/actions/workflows/build-stable.yml)
[![Dev Build](https://github.com/mmBesar/rofi-wayland-debian/actions/workflows/build-dev.yml/badge.svg)](https://github.com/mmBesar/rofi-wayland-debian/actions/workflows/build-dev.yml)

**Unofficial Debian packages** for [Rofi](https://github.com/davatorium/rofi) with official Wayland support, plus the [rofi-emoji](https://github.com/Mange/rofi-emoji) plugin — ready to install.

> **⚠️ Important:** This repository only provides Debian packaging. All credit for Rofi goes to [davatorium/rofi](https://github.com/davatorium/rofi) and for the emoji plugin to [Mange/rofi-emoji](https://github.com/Mange/rofi-emoji).

---

## Why this repo?

Debian Trixie ships rofi **1.7.5** (X11 only). Wayland support was only merged in rofi **2.0.0**. This repo gives you the latest rofi with full Wayland support on Trixie and Sid, plus the emoji plugin bundled and ready to go.

---

## What's included

- ✅ Official Wayland support via layer shell protocol
- ✅ X11/XCB support (dual backend, auto-detected)
- ✅ All standard rofi modes (run, drun, window, ssh, keys, filebrowser)
- ✅ Emoji picker via `rofi -show emoji`
- ✅ Debian 13 (Trixie) and Sid packages
- ✅ Stable and dev builds

---

## Releases

Two release tracks are available:

| Track | Badge | Built from | Use for |
|-------|-------|------------|---------|
| **Stable** | ![latest](https://img.shields.io/github/v/release/mmBesar/rofi-wayland-debian?label=stable&color=brightgreen) | Latest upstream tag | Daily use |
| **Dev** | ![dev](https://img.shields.io/github/v/release/mmBesar/rofi-wayland-debian?include_prereleases&label=dev&color=orange) | Latest upstream commit | Testing new features |

Both tracks build weekly and on every push to main.

---

## Installation

### Step 1 — Download

Go to the [Releases page](https://github.com/mmBesar/rofi-wayland-debian/releases) and pick your track:

- **Stable (recommended):** [Latest stable release](https://github.com/mmBesar/rofi-wayland-debian/releases/latest)
- **Dev:** Latest pre-release from the [releases list](https://github.com/mmBesar/rofi-wayland-debian/releases)

Download **two files** matching your Debian version:

| File | Purpose |
|------|---------|
| `rofi-wayland_*~trixie*_amd64.deb` | Rofi for Debian 13 (Trixie) |
| `rofi-emoji_*~trixie*_amd64.deb` | Emoji plugin for Debian 13 (Trixie) |
| `rofi-wayland_*~sid*_amd64.deb` | Rofi for Debian Sid |
| `rofi-emoji_*~sid*_amd64.deb` | Emoji plugin for Debian Sid |

Or grab them directly from the terminal:

**Debian 13 (Trixie) — Stable:**
```bash
curl -s https://api.github.com/repos/mmBesar/rofi-wayland-debian/releases/latest \
  | grep "browser_download_url.*trixie.*\.deb" \
  | cut -d '"' -f 4 \
  | xargs wget
```

**Debian Sid — Stable:**
```bash
curl -s https://api.github.com/repos/mmBesar/rofi-wayland-debian/releases/latest \
  | grep "browser_download_url.*sid.*\.deb" \
  | cut -d '"' -f 4 \
  | xargs wget
```

### Step 2 — Install

Always install rofi first, then rofi-emoji, then the color emoji font:

```bash
# Install rofi first
sudo apt install ./rofi-wayland_*.deb

# Then install the emoji plugin
sudo apt install ./rofi-emoji_*.deb

# Install color emoji font (required for colored emoji in the picker)
sudo apt install fonts-noto-color-emoji
```

> `rofi-wayland` conflicts with and replaces the official `rofi` package. `apt` handles this automatically.

---

## Usage

### Basic

Rofi automatically detects whether you're on Wayland or X11:

```bash
rofi -show drun      # Application launcher
rofi -show window    # Window switcher
rofi -show run       # Run command
rofi -show drun -x11 # Force X11 backend
```

### Emoji mode

After installing `rofi-emoji`, you need to enable the emoji mode in your rofi config. Edit `~/.config/rofi/config.rasi` and add `emoji` to the modes list:

```
configuration {
    modes: "window,drun,run,ssh,emoji";
}
```

If you don't have a config file yet, create one:

```bash
mkdir -p ~/.config/rofi
cat > ~/.config/rofi/config.rasi << 'EOF'
configuration {
    modes: "window,drun,run,ssh,emoji";
}
EOF
```

Then run:

```bash
rofi -show emoji
```

Type to search by name (e.g. "face", "heart", "cat"), then:
- **Enter** — insert emoji at cursor
- **Alt+Enter** — open copy/insert options menu

> **Color emoji:** Install `fonts-noto-color-emoji` for full color rendering in the picker:
> ```bash
> sudo apt install fonts-noto-color-emoji
> ```

#### Optional dependencies for emoji insertion

```bash
# Wayland sessions
sudo apt install wl-clipboard

# X11 sessions
sudo apt install xdotool
```

#### Bind to a key

**Hyprland** (`~/.config/hypr/hyprland.conf`):
```
bind = $mainMod, period, exec, rofi -show emoji
```

**Sway** (`~/.config/sway/config`):
```
bindsym $mod+period exec rofi -show emoji
```

---

## Configuration

Configuration works exactly as documented in the [official rofi docs](https://davatorium.github.io/rofi/). Existing configs work without changes.

Default config location: `~/.config/rofi/config.rasi`

---

## Troubleshooting

**Package conflict with official rofi:**
```bash
sudo apt remove rofi
sudo apt install ./rofi-wayland_*.deb
```

**Dependency errors:**
```bash
sudo apt install -f
```

**"Mode emoji not found":**
Make sure you installed **both** `.deb` files. The emoji plugin is a separate package — rofi alone is not enough.

**Wayland not working:**
Ensure your compositor supports the layer-shell protocol. Supported: Sway, Hyprland, River, Wayfire. GNOME Wayland has limited support — try the X11 backend with `-x11`.

**Theme issues:**
```bash
rofi-theme-selector
```

---

## License and Attribution

### This repository
- **License:** MIT
- **Copyright:** 2025 Mohammed Besar

### Rofi
- **Repository:** [davatorium/rofi](https://github.com/davatorium/rofi)
- **License:** MIT
- **Copyright:** 2012-2024 Dave Davenport and contributors

### rofi-emoji
- **Repository:** [Mange/rofi-emoji](https://github.com/Mange/rofi-emoji)
- **License:** MIT
- **Author:** Magnus Bergmark

This repository provides packaging only — no modifications to either upstream project.

---

## Support

| Issue type | Where to report |
|------------|----------------|
| Rofi functionality / bugs | [davatorium/rofi issues](https://github.com/davatorium/rofi/issues) |
| Emoji plugin issues | [Mange/rofi-emoji issues](https://github.com/Mange/rofi-emoji/issues) |
| Packaging / installation | [This repo's issues](https://github.com/mmBesar/rofi-wayland-debian/issues) |

---

## Acknowledgments

- **Dave Davenport** and contributors — [Rofi](https://github.com/davatorium/rofi)
- **lbonn** — original Wayland implementation later merged upstream
- **Magnus Bergmark** — [rofi-emoji](https://github.com/Mange/rofi-emoji)
- The **Debian** community for packaging standards
