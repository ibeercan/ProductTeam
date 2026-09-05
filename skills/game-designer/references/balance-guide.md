# Balance tables standard (balance.md / .xlsx)

Read before producing balance tables. They are the single source of truth for tunable numbers — SA binds them to code as one constants module; changing balance must never require touching game logic.

## Format (balance.md for small sets)

```markdown
# <Game> — Balance

> Version: 1 | Source: gdd.md v1

| ID | Group | Parameter | Value | Unit | Notes / curve |
|----|-------|-----------|-------|------|---------------|
| BAL-01 | dash | distance | 160 | px | |
| BAL-02 | dash | i-frames | 120 | ms | |
| BAL-03 | dash | cooldown | 1.0 | s | |
| BAL-10 | waves | enemy hp growth | ×1.15 | per wave | geometric |
| BAL-11 | economy | scrap per kill | 3 | — | see wave table |
```

## When to use .xlsx instead

More than ~2 screens of numbers, or multi-axis tables (level × enemy × stat): use the xlsx document skill — one sheet per group (combat, economy, progression), a `README` sheet with the version, and the same `BAL-xxx` ids in the first column. Export a markdown mirror only if asked.

## Rules

- Every `BAL-xxx` id is referenced from `gdd.md` (or a level brief) — unreferenced rows are dead numbers, delete them.
- No balance value ever appears inline in `gdd.md`, spec or code — only the id.
- Progression/economy values carry their curve or rule ("×1.15 per wave"), not just the base — QA tests the rule, not one point.
- Sanity pass before handoff: min/max/starting values produce a playable first minute (first kill ≤ 10s, first upgrade ≤ 60s — or the game's own stated pacing).
- Version bump on any value change; SA's constants module pins the version it generated from.
