# Physics Sandbox (Single-File HTML Physics Lab)

A zero-dependency, single-file HTML physics sandbox. Open `a.html` in a browser and play — no build step, no server, no network required.

---

## Quick Start

```text
Double-click a.html -> opens in your browser (Chrome / Edge recommended; backdrop-filter required)
```

- **Drag** symbols from the right-hand palette onto the canvas
- **Merge** letters on contact to synthesize formulas (strict pairing)
- **Double-click** walls / cars / springs to open their control panels; double-click a letter to split it
- **Right-click** to copy an entity; drag entities onto the trash bin to delete them; double-click the bin to empty everything

---

## Features

### 1. Gravity System
- 9 directions: up, down, left, right + 4 diagonals + none
- Magnitude: Earth 9.8 / Moon 1.62 m/s²; the magnitude selector hides when gravity is off
- Everything is affected except black holes, static constructs and dragged objects

### 2. Movable / Collapsible Palette
- The palette can be dragged anywhere and collapsed into a round badge
- The round badge is draggable too; click it to expand

### 3. Custom Walls
- Straight wall (rotatable at any angle) and arc wall (left/right flip + adjustable curve angle, 20°–330°)
- Double-click panel: flip (arc only), curve angle, rotation, friction, delete
- Real collision geometry — balls, sliders, cars and letters roll and bounce on walls
- Walls can be dragged and deleted

### 4. Ball & Slider
- Circle / rectangle rigid bodies with gravity, collisions and free angular velocity
- Balls roll and spin in contact with walls according to their speed

### 5. Parabola Trails
- Top-bar toggle; records ball / slider / car paths; auto-hidden without gravity
- Trails use each entity's own color with a fading tail; toggling off clears history

### 6. Spring
- Each end is **free**, **fixed in place**, or **bound to an entity** (ball / slider / car / formula)
- Panel: rest length, min length, pull limit (N), push limit (N), live force readout
- Breaks beyond 2× rest length or over the force limits; clamps at min length
- Springs can hang a car in mid-air; rotate them with the ↻ handle

### 7. Car
- Chassis + two wheels whose spin is coupled to motion
- Panel sets wheel radius (cm), which changes ride height immediately
- Springs can bind to the car; affected by gravity

### 8. Save / Load (JSON)
- **Save** exports the whole scene as `physics_sandbox_<timestamp>.json`
- **Load** restores it from a file
- Saved data: every entity + parameters, gravity, trail toggle, and all settings
- Spring bindings are stored as entity references and re-linked on load; transient effects (particles, shockwaves, shards) are cleared

### 9. Settings
| Setting | Range / Default | Description |
|---|---|---|
| mc² blast radius | 100–800 px / 300 | Scales shockwave physics and particle size |
| mc² fuse time | 0.3–5.0 s / 1.1 | Bomb countdown before detonation |
| Rotate-handle linger | 0–5000 ms / 1500 | How long the ↻ handle stays visible after you leave the entity, so you can actually reach it |
| Hint bar material | Normal / Acrylic / Liquid Glass / Mica | Bottom hint bar skin |
| Palette material | Normal / Acrylic / Liquid Glass / Mica | Palette skin |

The two materials are chosen independently, and all values persist inside the save file. Out-of-range values are clamped automatically.

> Note: the in-app UI labels are in Chinese; the material order above matches the dropdown order.

---

## Formula Lab

- Contact-to-merge synthesis with strict pairing (`mc²` needs `m+c+c` or `m+c²`)
- `mg` falls under gravity · `mc²` is a bomb · `E = mc²` spawns a black hole · `½mv²` sheds elastic-collision shards on wall impact
- Single `E` / `B` letters create electric / magnetic fields · `μ` creates a friction field
- Drag `t` onto `g` / `q` / `v` for small combos; `vt` combos become rotatable rods
- Black holes feature tidal tearing, an accretion disk and matter consumption
- High-speed flight, hard landings and black-hole proximity fracture multi-letter formulas
- The **Formula Grimoire** button lists every recipe with descriptions

---

## Interface Guide

| Location | Purpose |
|---|---|
| Top bar | Clear all · Pause · Gravity · Trails · Save · Load · Settings |
| Top left | Entity / particle / magnet counters and pause tag |
| Right | Letter palette (draggable, collapsible) |
| Bottom | Hint bar (material selectable) |
| Bottom right | Trash bin: drag to delete, double-click to empty |
| ↻ handle | Appears when hovering a wall / ball / slider / car / spring / rod; drag to rotate |

Tool panels are movable and close automatically when their entity is deleted. Mouse and touch input are both supported.

---

## File Layout

```text
a.html        <- the whole game (single file)
README.md     <- this file (English)
README_zh.md  <- Chinese readme
```

---

## Development & Testing

- The source is one `<script>` block; the regression suite lives in the dev sandbox:
  - `extract.js` — pulls the script block out and syntax-checks it
  - `s4_smoke.js` — 113 assertions: fracture, walls, ball/slider, car, trails, spring
  - `bh_smoke.js` — black hole / fields / merge integrity
  - `s5_smoke.js` — 50 assertions: save/load round-trip, value clamping, blast radius, fuse time, rotate-handle linger, materials
- Every stage is backed up as `back/a_<timestamp>_<stage>.html` without overwriting

---

## Browser Support

Modern Chromium (Chrome / Edge) or Firefox with `backdrop-filter` support. No internet access is required after the file loads.
