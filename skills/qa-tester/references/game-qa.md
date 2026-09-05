# Game QA (Phaser) — playtest, performance, saves

Read for game initiatives when designing tests and verifying builds. Phaser games run in the browser: the main agent can execute live checks with the `web-gui-tester` skill (sub-agents return checklists — they cannot load browser skills).

## Playtest protocol

A playtest is a run section in `testrun-report.md` (`scope: playtest`), not a vibe. Record per session:

- **First minute:** time to first interaction; what the player tries first; first confusion (where they click/press and nothing happens).
- **Core loop check:** N full loops executed (N = 3 minimum); where attention dropped (idle time, repeated deaths without learning).
- **Friction log:** timestamped entries `player did X, expected Y, got Z` — these are BUG candidates or GDD findings (a mechanic that is no fun is a design finding, route it to game-designer via the PM, not a bug).
- **Fun verdict per pillar:** one line each — is the pillar actually landing?

## Live execution (main agent only)

Via `web-gui-tester`: load the served build (`npm run dev` / preview URL), play the smoke script (boot → menu → start → one core loop → game over → restart), capture screenshots at each step, and check the browser console — zero errors is part of the pass criteria.

## Performance budgets (web defaults; confirm against spec §6)

| Check | Target |
|-------|--------|
| Frame time | p95 < 16.6 ms (60 fps); hard fail on sustained > 33 ms |
| Boot to menu (localhost, cold cache) | < 3 s |
| First playable frame after "Start" | < 1 s |
| Total asset payload | per the registry size budget |

Measure frame time via the debug overlay or `game.loop.actualFps` sampling over a 30 s scripted session; report p95 and worst, not averages alone.

## Save integrity (web storage)

- Save → reload page → state restored (the exact AC, usually from spec's save FR).
- Corrupt-save handling: tamper the localStorage key (invalid JSON, wrong version) → game degrades gracefully (fresh start with a notice), never a black screen.
- Schema version migration: save written by older schema loads after "upgrade" — one case per migration declared in the spec.

## Browser matrix

Chromium — agent-executable, primary. Firefox / Safari — manual checklist rows, status `blocked (manual)` until the user runs them; never silently skipped.

## Priority mapping

P1: crashes, black screens, save loss, core loop unplayable. P2: perf budget misses, friction log items with workarounds. P3: cosmetic, polish. A "not fun" finding is severity **major** as a design finding even when everything works.
