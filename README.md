<p align="center">
  <a href="" rel="noopener">
    <img width="96px" height="96px" src="docs/app-icon.png" alt="DontDoze logo">
  </a>
</p>

<h3 align="center">DontDoze</h3>

<div align="center">

[![Platform](https://img.shields.io/badge/platform-macOS%2012%2B-lightgrey.svg)](https://www.apple.com/macos/)
[![Architecture](https://img.shields.io/badge/arch-Universal%20(x86__64%20%7C%20arm64)-blue.svg)](https://github.com/IqyRily/DontDoze)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

<br>

[![Download Latest Release](https://img.shields.io/badge/Download-DontDoze--macOS.zip-2ea44f?style=for-the-badge&logo=apple&logoColor=white)](https://github.com/IqyRily/DontDoze/releases/latest/download/DontDoze-macOS.zip)

</div>

---

<p align="center">
  A lightweight macOS menu bar utility to keep your Mac awake, prevent sleep on lid close, control Intel Turbo Boost, and manage power settings from a single menu bar icon.
  <br>
</p>

## Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Usage](#usage)
- [Built Using](#built_using)
- [Authors](#authors)
- [Acknowledgements](#acknowledgement)
- [License](#license)

## About <a name="about"></a>

macOS's built-in `caffeinate` prevents idle and display sleep, but it cannot stop your Mac from sleeping when you close the lid without an external monitor. **DontDoze** combines `caffeinate`, `pmset` (`SleepDisabled` & power management flags), Intel Turbo Boost control, and optional app suspension into a minimal native menu bar app.

<p align="center">
  <img src="docs/banner.png" alt="DontDoze Menu">
</p>

## Getting Started <a name="getting_started"></a>

### Prerequisites

- **macOS 12 Monterey** or newer (Universal Binary: Intel `x86_64` & Apple Silicon `arm64`)
- **Xcode Command Line Tools** (`swiftc`) if building from source:
  ```bash
  xcode-select --install
  ```
- *(Optional, Intel Macs only)* `DisableTurboBoost.64bits.kext` placed in `resources/` or `/Applications/Turbo Boost Switcher.app`

### Installation

#### Option 1: Download Prebuilt App
1. Download `DontDoze-macOS.zip` from [Releases](https://github.com/IqyRily/DontDoze/releases).
2. Unzip and move `DontDoze.app` to `/Applications`.
3. Open `DontDoze.app` (if macOS warns about an unidentified developer, right-click → **Open**).

#### Option 2: Build from Source
```bash
git clone https://github.com/IqyRily/DontDoze.git
cd DontDoze
chmod +x build.sh
./build.sh
open DontDoze.app
```

## Usage <a name="usage"></a>

- **Left-Click Icon:** Quickly toggle **Keep Device Awake** / **Allow Device Sleep** (runs `caffeinate -d -i -m -s` and sets `pmset -a disablesleep 1/0` when the Helper is installed).
- **Right-Click Icon:** Open the menu:
  - **Turbo Boost Status** *(Intel `x86_64` only)*: Switch between **Always Enabled**, **Disable When Lid Close**, or **Always Disabled**.
  - **Preferences:**
    - **Launch at Login:** Start DontDoze automatically via `~/Library/LaunchAgents/com.rizki.DontDoze.plist`.
    - **Advanced Mode:** Unlocks independent **Keep Display Awake** (`caffeinate`) and **Keep System Awake on Lid Close** (`pmset -a disablesleep`) toggles, **Suspend Running Apps** (`SIGSTOP`/`SIGCONT` on lid close + `~/Library/Logs/DontDoze.log`), and **Power Management** (`standby`, `autopoweroff`, `hibernatemode`, `disksleep`, `powernap`, `womp`, `proximitywake`, `tcpkeepalive`, `ttyskeepawake`, plus **Reset to Defaults...**).
    - **Install / Remove Helper...:** One-time `/etc/sudoers.d/dontdoze` setup (prompted only when using features that need `sudo`, such as `pmset` or Turbo Boost), plus clean uninstallation.
    - **Menu Bar Icon:** Choose **Default** (`Zzz`), **MacBook**, or **Coffee Cup**.
    - **Language:** Follow System, Indonesia, or English.

> **Note on Turbo Boost:** macOS requires third-party kernel extensions to be authorized once in **System Settings → Privacy & Security** (click **Allow** and restart) before `kextload` can load `DisableTurboBoost.64bits.kext`.

## Built Using <a name="built_using"></a>

- [Swift](https://www.swift.org/) — Compiled directly into a Universal (`x86_64` + `arm64`) binary via `swiftc` & `lipo`
- **AppKit / Cocoa** — Native `NSStatusBar` & `NSMenu` UI
- **IOKit** — Clamshell / lid state detection (`AppleClamshellState`)
- **macOS `caffeinate` & `pmset`** — Display, idle, disk, and system sleep management

## Authors <a name="authors"></a>

- [@IqyRily](https://github.com/IqyRily) — Creator & Maintainer

## Acknowledgements <a name="acknowledgement"></a>

- `DisableTurboBoost.64bits.kext` from [Turbo Boost Switcher](https://github.com/rugarciap/Turbo-Boost-Switcher) by Rubén García Pérez

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for more information.
