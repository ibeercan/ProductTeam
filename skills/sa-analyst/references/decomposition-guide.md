# Implementation decomposition (tasks.md)

Read before writing or updating `tasks.md`. Decompose only when the spec is complete — tasks derive from FRs, not from imagination.

## File structure

```markdown
# <Initiative> — Implementation Tasks

> Version: 1 | Source: spec.md v3 | Order: dependency-first

## Summary

| ID | Parent | Task | FR | Depends on | MR scope | Status |
|----|--------|------|----|------------|----------|--------|
| T-001 | — | Project skeleton + CI | — | — | repo config | open |
| T-002 | — | Slot booking API | FR-001, FR-002 | T-001 | api/ + tests | open |
| T-003 | T-002 | Booking number generator | FR-002 | T-001 | 1 module + tests | open |

## T-002: Slot booking API

- **Implements:** FR-001, FR-002 (US-001)
- **Scope (one MR):** booking endpoint, validation, unit tests.
- **Not in scope:** UI, notifications (T-005).
- **Acceptance:** linked FRs demonstrably satisfied; tests green.
- **QA hints:** <data setup, environment specifics>
```

## Rules

- Pin the exact spec version (`Source: spec.md v3`). If spec.md bumps after decomposition, either update the affected tasks and bump this version, or record "spec v4 checked — no impact" in Notes. Unchecked drift silently invalidates MR contracts.
- `T-xxx` numbering starts fresh per initiative (implementation space) and is mirrored 1:1 in `backlog.md`; analysis/admin rows there use `A-xxx` — never mix the two spaces.
- One task = exactly one reviewable MR. A task that obviously needs several MRs becomes a parent task with subtasks (`Parent` set, flat ID numbering — no dotted ids).
- Every FR is covered by at least one task; every task links at least one FR (infrastructure/setup tasks are the only exception — mark `FR: —`).
- `Depends on` lists only task ids; keep the hierarchy shallow (parent + one level of subtasks).
- Order rows so the dependency chain can start from the first one.
- Statuses mirror the backlog: `open → in-progress → in-review → in-qa → merge-approved → merged → done`.
- Size tasks by "fits in one MR", not by time estimates — estimate only if the user asks.
