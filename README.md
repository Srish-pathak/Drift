# Drift — a fluid playground

Drift is a single-file, no-dependency HTML canvas toy. Touch or drag anywhere on the screen to paint with particles, stars, portals, or rain — no install, no build step, just open `index.html` in a browser.

## Quick start

1. Download `index.html`.
2. Open it directly in any modern browser (Chrome, Safari, Firefox, Edge).
3. Drag your mouse or finger across the canvas to begin.

No server, bundler, or dependencies required — everything (HTML, CSS, and JS) lives in one file.

## Modes

The bottom control panel lets you switch between seven drawing modes:

| Mode | Behavior |
|---|---|
| **Ink** | Soft, dark, flowing trails with light drag and gravity. |
| **Fire** | Warm, buoyant embers that rise and fade (additive blending). |
| **Neon** | Bright, glowing streaks with no gravity — pure color trails. |
| **Water** | Heavier, slower droplets that fall and pool. |
| **Universe** | Drag to sprinkle stars across a nebula backdrop; **hold** (without moving) to place a gravity well that pulls nearby stars in. Shooting stars appear periodically. |
| **Portal** | Tap to open a swirling portal. Choose a portal "flavor" (Space, Fire, Ocean, Cyber, Magic) from the flavor picker that appears above the panel. |
| **Rain** | Drag to wipe condensation off a foggy glass surface, revealing drips and splashes underneath. |

## Controls

- **Draw**: click-and-drag (mouse) or touch-and-drag (mobile/tablet), works with pointer events so it supports mouse, touch, and stylus input.
- **Save image** (down-arrow icon): exports the current canvas as a PNG (`drift-<timestamp>.png`).
- **Clear canvas** (trash icon): wipes all particles, stars, portals, and rain, and resets the background for the current mode.

## How it works (technical overview)

- **Rendering**: a single `<canvas>` element with a 2D context, redrawn every frame via `requestAnimationFrame`.
- **Particle system**: each drawing mode (`ink`, `fire`, `neon`, `water`) is defined by a palette object in `PALETTES` — controlling hue range, saturation, lightness, gravity, drag, lifespan, spread, and blend mode (`source-over` vs `lighter`/additive).
- **Trail effect**: instead of clearing the canvas each frame, a semi-transparent rectangle is painted over the whole canvas, letting old particles fade out gradually.
- **Universe mode**: a separate particle system (`uniStars`) layered over a parallax starfield and drifting nebula clouds, plus gravity wells (`uniWells`) that attract nearby stars, and randomly spawned shooting stars.
- **Portal mode**: swirling particle rings (`portalBits`) emitted from up to 3 active portals, each with its own color palette from `PORTAL_TYPES`.
- **Rain mode**: a fogged-glass simulation where dragging "wipes" a clear path, and physics-driven raindrops trickle and occasionally splash.
- **Responsive canvas**: automatically resizes to the window and accounts for device pixel ratio (capped at 2x) for crisp rendering on high-DPI screens.

## Browser support

Requires a browser with support for the Canvas 2D API and Pointer Events (all modern desktop and mobile browsers). No external libraries or network requests are used.

## File structure

```
index.html   — everything: markup, styles, and script in one file
README.md    — this file
```

## Customization ideas

- Add new palettes to `PALETTES` for additional drawing modes.
- Add new portal flavors to `PORTAL_TYPES`.
- Tweak `MAX_PARTICLES`, `MAX_STARS`, or `MAX_PORTAL_BITS` to trade visual density for performance.
- Adjust `gravity`, `drag`, and `life` values per palette to change how particles move and fade.
