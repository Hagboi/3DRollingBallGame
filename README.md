# Rollway

A 3D rolling-ball obstacle course game in a single self-contained `index.html`
(Three.js r160 + cannon-es 0.20 from jsDelivr; no build step).

Open `index.html` in a desktop or mobile browser. It needs network access to
`cdn.jsdelivr.net` for the two libraries; if your browser blocks ES modules
from `file://`, serve the folder instead (e.g. `python3 -m http.server`).

## Controls

| | Desktop | Mobile |
|---|---|---|
| Roll | WASD / arrow keys (gamepad stick works too) | hold anywhere to roll, drag left/right to steer, pull down to brake |
| Jump | Space (gamepad A) | swipe up (or tap with a second finger) |
| Pause | Esc / P | II button |
| Restart | R | pause menu |

Debug keys: `N` next level (Shift+N: +10), `B` previous level, `K` finish the
current level instantly, `F` FPS/draw-call overlay. URL params: `?level=42`
starts a level directly, `?unlock` unlocks all levels.

## What's in it

- **120 levels** from a seeded generator (the same level number always builds the
  same course). 12 themed worlds; every 10th level is a hand-authored boss course.
- **16 obstacle types**, two new ones per world: gaps, bounce pads, moving platforms
  and lifts, speed boosts and jump ramps, ice, rotating sweepers, lava and spikes,
  crumbling tiles, spinning discs, narrow beams, pendulums, pistons, sticky mud,
  conveyor belts, wind zones and teleporters.
- Checkpoints, a per-level timer, 1–3 stars against par times, collectible gems,
  and 12 ball skins bought with gems. Progress saves to `localStorage`.
- Procedural sound effects (Web Audio) and particles; no external assets.

## Code layout (inside `index.html`)

1. Constants & utilities
2. Themes, obstacle schedule, boss definitions
3. Level generator + `validateLevel` (checks every gap against the jump physics)
4. Save system
5. Audio
6. Renderer, shared geometry/materials
7. Physics world
8. Particles
9. Ball skins
10. Level runtime (build/unload meshes and bodies)
11. Input
12. Game state, physics step, triggers
13. Camera
14. UI
15. Main loop
16. Boot

`window.ROLLWAY` exposes test hooks (`validateAll()`, `generateLevel(n)`,
`startLevel(n)`, `step()`, …).
