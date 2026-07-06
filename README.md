# 🎯 PracticeUtils – A CS2 Practice Config & Script

A powerful **Counter-Strike 2** practice tool that brings **lineup finder**, **teleport utils**, **damage/flash/nade logging**, and a host of other utilities to your offline practice sessions.
It's implemented fully with tools provided by valve: configs and cs_script. 

> **Author:** Leiti  

<img width="1440" height="1080" alt="202607~4" src="https://github.com/user-attachments/assets/51c5a75d-8607-4524-947a-bcb4d9f39a70" />

---

## 📦 Installation

1. Place the folder `practiceutils` in your `csgo/cfg/` directory.
2. Adjust settings in `practiceutils/main.cfg`, `practiceutils/settings.cfg` and `practiceutils/practiceConvars.cfg`
3. Add following section to your launch options `-disable_workshop_command_filtering +exec "practiceutils/main"`. (`disable_workshop_command_filtering` is required for the cfg to work on workshop maps)
4. Enter an offline Map and enter following command into the console `+practiceutils`.

---

## 🚀 Features

### 🔹 TeleportUtils
Manage saved positions, spawn points, and teleport between players or locations.

- **Save & Load Positions** – save your current position/angle, list them, and teleport yourself or others.
- **Saved Positions are persistent** - Up to 10 positions per map can be saved. Those positions can be loaded again on new sessions.
- **Spawn Squares** – interactable squares on spawn points to teleport to them.
- **Position Balloons** – interactable balloon markers on saved positions that you can interact with to teleport.
- **Player Swapping** – swap positions with another player.
- **Teleport (tp)** – teleport any player to any other player’s location.
- **Bot Placement** – place bots on saved positions.
- **Autosave lineup positions** - setting option to automatically save the position when you throw a grenade.

### 🔹 LineupFinder
Find grenade lineups automatically by scanning a range of angles.

- **Define Target Zones** – set up to 6 zones (boxes) where you want grenades to land.
- **Scan Angles** – the script automatically throws grenades at many pitch/yaw combinations and records those that land in your zones.
- **Preview Throws** – test a single throw with the current reference.
- **List & Dump Results** – browse found lineups and get console commands to reproduce them.
- **Supported Throw Styles:** Left/Middle/Right (Duck) (Jump) (W, A, S, D)

### 🔹 Printers (Logging)
Get real‑time feedback in team radio chat.

- **Print Flash** – shows flashbang exposure duration, distance, and angle.
- **Print Nade** – reports grenade air time.
- **Print Damage** – enables godmode and displays damage dealt to players and the weapon used.

### 🔹 Other Practice Features
- **X‑Ray Glow** – see all players through walls.
- **Noblind** – prevents flashbangs from blinding you (spawns balloons to block them).
- **Settings** – tune dozens of parameters like scan speed, sound, auto‑save, and more.
- **Menu Navigation** – use `menu_up`/`menu_down` to navigate interactive HUD menus.

---

## 📋 Command Reference

| Command | Arguments | Description |
|---------|-----------|-------------|
| `+practiceutils` | – | Enable PracticeUtils in your local map. |
| `practiceutils` | – | Show the help screen with all commands. |
| **TeleportUtils** |
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
| `printpos` | – | Print your current position/angles to console (useful for copying setpos/setang). |
| `printplayerpos` | – | Print positions of all players. |
| **Lineupfinder** |
| `lineup_target <1-6>` | `<1-6>` | Select and edit a target zone (zone number). |
| `lineup_scan [pitchRange] [yawRange] [step]` | `[pitchRange]` `[yawRange]` `[step]` (all optional) | Start a scan for lineups. Default ranges 20°, step 2°. |
| `lineup_preview` | – | Open/close preview mode to test throws (debug tool). |
| `lineup_menu` | – | Open/close the lineup results menu after a scan. |
| `lineup_dump` | – | Print all found lineups as console commands (setpos/setang). |
| `lineup_clear` | – | Clear all zones and lineup results. |
| **Printers** |
| `printflash [on/off]` | `[on/off]` (optional) | Toggle flashbang exposure reporting. |
| `printnade [on/off]` | `[on/off]` (optional) | Toggle grenade air time reporting. |
| `printdamage [on/off]` | `[on/off]` (optional) | Toggle godmode and damage reporting. |
| **Other** |
| `xray [on/off]` | `[on/off]` (optional) | Toggle global X‑Ray glow outline on all players. |
| `noblind [on/off]` | `[on/off]` (optional) | Toggle flashbang immunity. |
| `settings [--setting value ...]` | `--setting value` (multiple) | View or change script settings. Use without args to list all. |
| `menu_up` | – | Navigate up in an active menu. |
| `menu_down` | – | Navigate down in an active menu. |
| `-practiceutils` | – | Clean up all entities created by the script (balloons, glows, squares, menus, etc.). |

> **Note:** Most boolean toggles accept `on`/`off`, `true`/`false`, `1`/`0`, or no argument to flip the current state.

---

## ⚙️ Settings (via `settings` command)

Run `settings` without arguments to see the full list with descriptions and current values.  
Common settings:

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
| `autosave_lineups` | bool | Automatically save position/angles when throwing a grenade (useful for recording lineups). |
| `use_opens_buy_menu` | bool | Restores your `cl_use_opens_buy_menu` setting after menus close. |
| `auto_menuscroll_remap` | bool | Enables mouse wheel navigation in menus. |
| `path` | string | Base folder path between `cfg` and `practiceutils` (e.g., `mycfg/addon`) – empty means `cfg/`. |
| `noblind` | bool | Prevent flashbangs from blinding. |

---

## 🧠 Usage Tips

- **Interactive Menus** – many features (like `loadpos` and `lineup_menu`) use HUD hints. Use `menu_up`/`menu_down` to navigate, and `USE`/`RELOAD`/`INSPECT` to interact.
- **Scanning** – define at least one zone with `lineup_target`, then run `lineup_scan`. The script will freeze you, simulate many throws, and show results.
- **Bots** – use `placebots` to position bots on your saved spots for testing nades or angles.
- **Cleanup** – run `-practiceutils` to cleanly remove the script without restarting the map.

---

## 📝 License & Credits

**PracticeUtils** is a free tool created by **Leiti**.  
[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)

---

Enjoy practicing! 🎮
