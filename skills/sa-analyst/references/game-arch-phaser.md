# Game architecture — Phaser 3 (web) conventions

Read for game initiatives before writing `spec.md`; these conventions extend (not replace) the standard spec template.

## Stack

- **Phaser 3 + TypeScript + Vite**, strict mode; npm scripts: `dev`, `build`, `preview`, `test`.
- Unit tests: **Vitest** for pure logic (no Phaser imports in tested modules where possible).
- No engine fork, no CDN — everything from npm, offline-friendly.

## Scene architecture

- Fixed scene set: `Boot` (loads the preload manifest) → `Preload` → `Menu` → `Game` → `UI` overlays as separate scenes, plus `GameOver`. No god-scenes: `Game` orchestrates, systems do work.
- Game logic lives in plain classes/modules **outside scenes** (combat resolution, progression, economy) — scenes only wire input, rendering and scene flow. This is what makes the logic unit-testable and the whole engine swappable.
- State: explicit state objects passed to systems; no hidden globals; Phaser registry only for cross-scene flags.

## Tuning constants (the balance binding)

- One generated module `src/config/balance.ts` — every value carries its `BAL-xxx` id in a comment; generated from `balance.md`/xlsx, version-pinned (`// source: balance.md v3`). Game code reads constants, never hardcodes numbers — reviewer flags any literal that has a BAL id.

## Assets wiring

- Single `src/config/assets.ts` manifest: keys = `ASSET-xxx` ids, paths under `public/assets/`, loaded in Boot/Preload per the asset registry. Registry is the contract; code never loads unregistered files.

## Saves

- localStorage (small state) or IndexedDB (large); **versioned schema** `{ version, data }` with a migration chain; corrupt/unknown versions → fresh start + user notice (matches the QA save-integrity cases).

## Input & platforms

- Keyboard + mouse first; gamepad behind an input-adapter interface if the GDD demands it. Desktop browser primary; mobile/touch only if the brief says so (then input adapter from day one).

## Testing strategy (feeds QA)

- Pure logic → Vitest (damage math, progression rules from BAL curves, save migrations).
- Scene smoke → the QA live protocol (`game-qa.md`): boot → menu → one core loop → restart, console clean.
- Each task in `tasks.md` states which layer it touches; a task adding logic without tests is a review finding.
