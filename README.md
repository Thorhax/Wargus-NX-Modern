# Wargus NX Modern (Nintendo Switch Port)

[![Support me on Ko-fi](https://img.shields.io/badge/Ko--fi-Support%20me-FF5E5B?logo=kofi&logoColor=white)](https://ko-fi.com/thorhax)
[![GitHub Release](https://img.shields.io/github/v/release/Thorhax/Wargus-NX-Modern?include_prereleases&color=blue)](https://github.com/Thorhax/Wargus-NX-Modern/releases)

Modern Nintendo Switch port of **Wargus** (Warcraft II) and **War1gus** (Warcraft: Orcs & Humans) running on the Stratagus RTS engine.

Based on **Stratagus v3.3.2** with handheld controller and touchscreen support inspired by Northfear's Vita port, updated for Nintendo Switch libnx and devkitPro.

---

## Installation & Setup

Wargus requires extracted game data from an original retail CD or GOG version of **Warcraft II: Tides of Darkness / Beyond the Dark Portal** (or Warcraft 1 for War1gus).

### 1. Extract Game Data on PC
1. Download the official Wargus 3.3.2 release for your PC (Windows/Linux/macOS):
   - [Wargus Releases](https://github.com/Wargus/wargus/releases) (v3.3.2 recommended)
   - [War1gus Releases](https://github.com/Wargus/war1gus/releases) (if playing Warcraft I)
2. Run the installer / setup on your PC and point it to your Warcraft II CD / GOG directory to extract and convert the game data (graphics, sounds, music, videos).
3. Verify that the PC game runs and generates the data folders.

### 2. Copy Data to SD Card
1. Download `wargus.nro` from the [Releases](https://github.com/Thorhax/Wargus-NX-Modern/releases) page.
2. Place `wargus.nro` onto your SD card at:
   - `sdmc:/switch/wargus/wargus.nro`
3. Copy the extracted data folders from your PC into `sdmc:/switch/wargus/`:
   - `campaigns/`
   - `graphics/`
   - `maps/`
   - `music/`
   - `sounds/`
   - `videos/`
   - `scripts/wc2-config.lua` (into `sdmc:/switch/wargus/scripts/wc2-config.lua`)
4. *(Optional for War1gus)*: If playing Warcraft 1, place files in `sdmc:/switch/war1gus/` with `scripts/wc1-config.lua`.

### 3. Launch
Launch `wargus.nro` from the Homebrew Menu (launch via title override/holding R on any installed game recommended for full RAM access).

---

## Controls

| Switch Button | Action |
| --- | --- |
| **Left Analog Stick** | Move Cursor / Pointer |
| **Right Analog Stick** | Scroll Map |
| **A** | Left Mouse Button (Select, Confirm, Order) |
| **B** | Right Mouse Button (Cancel, Move / Attack order) |
| **Y** | Attack command |
| **X** | Stop command |
| **D-Pad (Up / Right / Down / Left)** | Select Control Group 1, 2, 3, 4 |
| **L + D-Pad** | Assign Control Group 1, 2, 3, 4 (Ctrl + 1..4) |
| **R (Hold)** | Fast Cursor Movement / Shift modifier |
| **Plus (+)** | Escape / In-game Menu |
| **Minus (-)** | F10 / Options Menu |
| **Touchscreen** | Direct cursor tap and drag selection |

### Preferences
You can adjust controller pointer speed and bilinear filtering by editing:
`sdmc:/switch/wargus/wc2/preferences.lua`
- `ControllerSpeed`: Adjust cursor movement speed (default: `1400`)
- `BilinearFilter`: Set to `true` or `false` for scaling filter

---

## Building from Source

Build requires [devkitPro](https://devkitpro.org/) with `devkitA64` and `switch-portlibs`.

```bash
# Using Docker with devkitpro/devkita64:
docker run --rm -v $(pwd):/work -w /work devkitpro/devkita64:latest bash -c "
    source /opt/devkitpro/switchvars.sh && \
    mkdir -p build && cd build && \
    cmake .. -DCMAKE_TOOLCHAIN_FILE=/opt/devkitpro/cmake/Switch.cmake \
             -DENABLE_STATIC=ON \
             -DENABLE_USEGAMEDIR=ON \
             -DEAGER_LOAD=ON \
             -DCMAKE_BUILD_TYPE=Release \
             -DWITH_OPENMP=OFF && \
    make -j\$(nproc)
"
```
The output executable `wargus.nro` will be in `build/`.

---

## Support & Donations

If you enjoy this port and want to support future Nintendo Switch homebrew ports and updates, consider donating:

[![Support me on Ko-fi](https://img.shields.io/badge/Ko--fi-Support%20me-FF5E5B?style=for-the-badge&logo=kofi&logoColor=white)](https://ko-fi.com/thorhax)

---

## Credits & License

- **Stratagus RTS Engine Team**: [Stratagus](https://github.com/Wargus/stratagus)
- **Wargus & War1gus Team**: [Wargus](https://github.com/Wargus/wargus)
- **Northfear**: For the incredible PS Vita port and gamepad/touch integration foundation ([stratagus-vita](https://github.com/Northfear/stratagus-vita))
- **devkitPro & libnx contributors**: Bare-metal Nintendo Switch toolchain and libraries
- **Thorhax**: Modern Nintendo Switch port, build system integration, and updates

Licensed under the **GNU General Public License v2.0** (GPL-2.0). See [COPYING](COPYING) for details.
