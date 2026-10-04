# 🎯 PracticeUtils – A CS2 Practice Config & Script

A powerful **Counter-Strike 2** practice tool that brings **lineup-finder**, **teleport-utils**, **damage/flash/nade logging**, and a host of other utilities to your offline practice sessions.  
It's implemented fully with tools provided by Valve: configs and `cs_script`.

> **Author:** Leiti

![PracticeUtils screenshot](https://github.com/user-attachments/assets/51c5a75d-8607-4524-947a-bcb4d9f39a70)

---

## 📦 Installation

1. Place the folder `practiceutils` in your `csgo/cfg/` directory.
2. Adjust settings in `practiceutils/settings.cfg` (global settings) and optionally create map‑specific spawn configs in `practiceutils/maps/` (see [Spawn Management](#-spawn-management) below).
3. Add the following snippet to your **launch options**: `-disable_workshop_command_filtering +exec "practiceutils/main"`(`-disable_workshop_command_filtering` is required for the cfg to work on workshop maps.)
4. Enter an offline map and type the following into the console: `+practiceutils`

---

## 🚀 Features

### 🔹 TeleportUtils
- Save & load positions (persistent across sessions, up to 10 per map)
- Interactable spawn squares and position balloons (teleport on use/attack)
- Swap positions with another player
- Teleport any player to any other player (`tp` command)
- Place bots on saved positions
- Autosave position on grenade throw (optional)

### 🔹 LineupFinder
- Define up to 6 target zones (boxes)
- Scan a range of pitch/yaw angles to find grenade lineups
- Preview individual throws
- Browse and dump found lineups as console commands
- Supports left/right/middle clicks, jump, duck, and movement (WASD) throws

### 🔹 Printers (Logging)
- **Print Flash** – flashbang exposure duration, distance, and angle
- **Print Nade** – grenade air time
- **Print Damage** – godmode + damage reporting with weapon/hitgroup info

### 🔹 Spawn Management
- Define custom spawn points per map without editing the script
- Map‑specific configs (`practiceutils/maps/<mapname>.cfg`) with `settings --addspawn` commands
- Auto‑generated fallback from `info_player_*` entities if no custom spawns exist

### 🔹 Other Practice Features
- X‑Ray glow for all players
- Noblind – prevents flashbangs from blinding
- Fully configurable via `settings` command
- Interactive HUD menus with mouse wheel navigation

---

## 📋 Command Reference

| Command | Arguments | Description |
|---------|-----------|-------------|
| **General** |||
| `+practiceutils` | – | Enable PracticeUtils in your local map. |
| `practiceutils` | – | Show the help screen with all commands. |
| `-practiceutils` | – | Clean up all entities created by the script (balloons, glows, squares, menus, etc.). |
| **TeleportUtils** |||
| `savepos` | – | Save your current position and view angles. |
| `listpos` | – | List all saved positions with console commands to teleport. |
| `clearpos [index]` | `[index]` (optional) | Clear a specific saved position by index (1‑based) or all if no index given. |
| `loadpos` | `[--pos <n>] [--player <name>]` | Open a menu to teleport a selected player to a saved position. Use `--pos` and `--player` to jump directly. |
| `spawnsquares [on/off] [keepangle]` | `on/off`, `keepangle` (optional) | Toggle spawn squares. With `keepangle`, teleport keeps your current view angle. |
| `posballoons [on/off] [keepangle]` | `on/off`, `keepangle` (optional) | Toggle interactable position balloons. With `keepangle`, teleport keeps your current view angle. |
| `listspawns` | – | List all spawn points on the current map. |
| `swap [player]` | `[player]` (optional name) | Swap positions with the player in your crosshair or a named player. |
| `tp [source] <target>` | `<target>` (required), `[source]` (optional) | Teleport `source` (default is you) to `target`'s location. |
| `placebots [T/CT]` | `[T/CT]` (optional) | Place bots (all or team‑filtered) on saved positions. |
| `printpos` | – | Print your current position/angles to console. |
| `printplayerpos` | – | Print positions of all players. |
| **LineupFinder** |||
| `lineup_target <1-6>` | `<1-6>` | Select and edit a target zone (zone number). |
| `lineup_scan [pitchRange] [yawRange] [step]` | `[pitchRange]` `[yawRange]` `[step]` (all optional) | Start a scan for lineups. Default ranges 20°, step 2°. |
| `lineup_preview` | – | Open/close preview mode to test throws (debug tool). |
| `lineup_menu` | – | Open/close the lineup results menu after a scan. |
| `lineup_dump` | – | Print all found lineups as console commands (setpos/setang). |
| `lineup_clear` | – | Clear all zones and lineup results. |
| **Printers** |||
| `printflash [on/off]` | `[on/off]` (optional) | Toggle flashbang exposure reporting. |
| `printnade [on/off]` | `[on/off]` (optional) | Toggle grenade air time reporting. |
| `printdamage [on/off]` | `[on/off]` (optional) | Toggle godmode and damage reporting. |
| **Spawn Management** |||
| `settings --addspawn { ... }` | See syntax below | Add a custom spawn point for the current map. |
| `settings --clearspawns` | – | Remove all custom spawn points for the current map. |
| **Other** |||
| `xray [on/off]` | `[on/off]` (optional) | Toggle global X‑Ray glow outline on all players. |
| `noblind [on/off]` | `[on/off]` (optional) | Toggle flashbang immunity. |
| `settings [--setting value ...]` | `--setting value` (multiple) | View or change script settings. Use without args to list all. |
| `menu_up` | – | Navigate up in an active menu. |
| `menu_down` | – | Navigate down in an active menu. |

> **Note:** Most boolean toggles accept `on`/`off`, `true`/`false`, `1`/`0`, or no argument to flip the current state.

---

## 🧭 Spawn Management

Spawn squares are defined in **map‑specific configuration files**.

### 📁 Map Config Files
Place a file named `<mapname>.cfg` in `cfg/practiceutils/maps/` (e.g., `de_mirage.cfg`). The script executes this file on map load.

### ✏️ Syntax: `settings --addspawn`
`settings --addspawn { label "..." id "..." origin "x y z" angles "pitch yaw roll" color "r g b a" idangle "pitch yaw roll" idcolor "r g b a" }`

**Required fields:**
- `label` – the name shown on the spawn square (e.g., `"[T] Spawn"`).
- `id` – a number (e.g., `"1"`) displayed on the square.
- `origin` – three space‑separated floats: `x y z`.
- `angles` – three space‑separated floats: `pitch yaw roll` (for the player's view angle).
- `color` – four space‑separated integers: `r g b a` (0–255).

**Optional fields:**
- `idangle` – three space‑separated floats: `pitch yaw roll` – rotation of the ID text on the square (default: `0 90 0`).
- `idcolor` – four space‑separated integers: `r g b a` – color of the ID text (default: same as `color` but with alpha `100`).

**Example:**
`settings --addspawn { label "[T] Spawn" id "1" origin "-2994 1312 -127.07091522216797" angles "0 -26.99993896484375 0" color "222 155 53 255" idangle "0 90 0" idcolor "222 155 53 100" }`


### 🔁 Fallback
If no custom spawns are defined for a map, the script automatically generates spawns from `info_player_terrorist` and `info_player_counterterrorist` entities. You can still use `listspawns` to see them.

---

## ⚙️ Settings (via `settings` command)

Run `settings` without arguments to see the full list with descriptions and current values.

| Setting | Type | Description |
|---------|------|-------------|
| `debug_logs` | bool | Print debug messages. |
| `lineup_max_projectiles` | int | Max simultaneous simulated grenades during a scan. |
| `lineup_scan_speed` | float | `host_timescale` during scan. |
| `lineup_zone_padding` | float | Extra units added around each zone. |
| `xray` | bool | X‑Ray glow for all players. |
| `print_damage` | bool | Print damage taken. |
| `print_flash` | bool | Print flash exposure. |
| `print_nade` | bool | Print grenade flight time. |
| `posballoons` | bool | Show position balloons. |
| `posballoons_keepangle` | bool | Keep view angle when teleporting via balloons. |
| `spawnsquares` | bool | Show spawn squares. |
| `spawnsquares_keepangle` | bool | Keep view angle when teleporting via squares. |
| `play_sounds` | bool | Play UI sounds (clicks, confirmations, etc.). |
| `autosave_lineups` | bool | Automatically save position/angles when throwing a grenade. |
| `auto_menuscroll_remap` | bool | Enables mouse wheel navigation in menus. |
| `path` | string | Base folder path between `cfg` and `practiceutils` (e.g., `mycfg/addon`) – empty means `cfg/`. |
| `noblind` | bool | Prevent flashbangs from blinding. |

---

## 🧠 Usage Tips

- **Interactive Menus** – many features (like `loadpos` and `lineup_menu`) use HUD hints. Use `menu_up`/`menu_down` to navigate, and `USE`/`RELOAD`/`INSPECT` to interact.
- **Scanning** – define at least one zone with `lineup_target`, then run `lineup_scan`. The script will freeze you, simulate many throws, and show results.
- **Custom Spawns** – create a map‑specific `.cfg` in `practiceutils/maps/` to define your own spawn points. The script loads them on map start.
- **Bots** – use `placebots` to position bots on your saved spots for testing nades or angles.
- **Cleanup** – run `-practiceutils` to cleanly remove the script without restarting the map.

---

## 📝 License & Credits

**PracticeUtils** is a free tool created by **Leiti**.  
[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)

Enjoy practicing! 🎮
