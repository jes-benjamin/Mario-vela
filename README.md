# Mario Vela — Meow Rio (喵哩奥)

A Cat Mario style 2D platformer built as a **VelaOS Quick App** for Xiaomi and Redmi wearables.
Guide the little cat through traps, enemies and lucky blocks — and try to clear all **150 levels**.

![Version](https://img.shields.io/badge/version-1.0.5-orange)
![Platform](https://img.shields.io/badge/platform-VelaOS%20Quick%20App-blue)
![Device](https://img.shields.io/badge/device-watch-red)

---

## Features

- **150 unique levels** — procedurally generated from per-level seeds, no duplicates, with a difficulty curve
- **Auto-save system** — checkpoints and level completion are stored automatically, up to **10 rotating save slots**, browse with a scrollable list and **long-press to delete** a slot
- **Coin economy** — pick up coins in levels, spend them in the shop
- **Shop** — buy and switch between **5 character skins**, and purchase **consumable items**:
  - **Shield (20 coins)** — survives one hit; if you fall off a cliff you are teleported back to the edge
  - **Speed Shoes (20 coins)** — temporary movement speed boost
  - **Giant Mushroom (20 coins)** — start the next level big
  - Items are carried over to the next level; the "big" effect is not
- **Power-ups in the level** — mushrooms (grow big), coins, and **lucky blocks** you punch from below (may drop a power-up *or* spawn an enemy)
- **Whole-level rendering** — the full map is loaded once and scrolled with a single container offset, the player stays centered; no per-step scene rebuilding, so it stays smooth on very low-end watches
- **Adaptive layout** — runtime screen detection fits the HUD, play field, controls and lists to the real display

## Supported devices

| Device | Resolution |
|---|---|
| Xiaomi Watch S4 45mm | 466 × 466 (round) |
| Xiaomi Watch S5 46mm | 466 × 466 (round) |
| Xiaomi Watch S4 41mm | 466 × 466 (round) |
| Xiaomi Watch S5 41mm | 466 × 466 (round) |
| Xiaomi Smart Band 9 Pro | 336 × 480 |
| Xiaomi Smart Band 10 Pro | 336 × 480 |
| Redmi Watch 5 | 432 × 514 |
| Redmi Watch 5 eSIM | 432 × 514 |
| REDMI Watch 6 | 432 × 514 |

The layout is resolution-independent (`designWidth: 466`), so other square/round VelaOS watches should work as well.

## Controls

- **← / →** on-screen buttons — move
- **跳** on-screen button — jump
- **Long-press** a save slot — delete it
- **Swipe right** — go back on list screens

## Build from source

```bash
npm install          # installs aiot-toolkit 2.0.5
npx aiot build       # debug build
npx aiot release     # signed release build -> dist/*.rpk
```

The produced `.rpk` can be installed on the watch through the Vela / Mi Fitness developer workflow.

## Project structure

```
src/
  manifest.json              # package id, designWidth, features, router
  pages/index/index.ux       # the whole game: engine, level gen, shop, saves, UI
  common/images/             # pixel-art tiles, characters, items, app icon
sign/                        # signing certificate used by aiot release
dist/                        # built .rpk packages
```

### Technical notes

- `.ux` single-file components (template / style / script) with MVVM bindings
- The game loop runs at 20 FPS with dirty-checked DOM updates and bit-shifted integer math
- The level is rendered **once** into a world container; the camera only updates the container's `left` offset and the player's screen position
- Saves use an in-memory mirror plus `@system.storage` persistence (no sync I/O inside `onBackPress`)
- VelaOS CSS limitations are respected: no `object-fit: fill`, no `z-index`, no `overflow`, no `background` shorthand, no `opacity` on overlays, explicit `width`/`height` on inline styles

## Author

**jes-benjamin** — [@jes-benjamin](https://github.com/jes-benjamin)

## License

GNU General Public License v3.0 — free and open source, secondary distribution allowed.
