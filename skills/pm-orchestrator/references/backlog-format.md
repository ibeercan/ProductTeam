# File-based backlog (backlog.md)

No external tracker is required — the backlog is the file. One per initiative. **Only the PM writes this file**: sub-agents record verdicts in their own artifacts (run Verdicts in `testrun-report.md`, sections in `gate-report.md`) and return summaries; the PM transcribes statuses.

```markdown
# <Initiative> — Backlog

| ID | Task | Role | Status | Artifact | Notes |
|----|------|------|--------|----------|-------|
| A-001 | Elicit user stories from brief | BA | done | stories.md | |
| A-002 | Requirements gate re-run | SA | open | gate-report.md | FAIL on FR-003 |
| T-010 | Implement slot booking API | Dev | in-qa | MR #12 | |
| T-011 | Fix double-booking on retry | Dev | open | MR #14 | BUG-003 |
| A-003 | Choose payment provider | User | open | spec.md §8 | blocks T-012 |

## Next user decision
<the single item waiting on the user, with options if applicable>
```

## Two ID spaces

- **`A-xxx`** — analysis, admin and user-decision rows (stage work, gate re-runs, questions to the user). Numbered by the PM.
- **`T-xxx`** — implementation tasks, mirrored 1:1 from `tasks.md` (numbered by the SA during decomposition, starting fresh per initiative).

Never reuse or renumber an ID, never let the spaces mix: a backlog row for an implementation task uses the exact `T-xxx` from `tasks.md`.

## Task statuses (implementation stage)

`open → in-progress → in-review → in-qa → merge-approved → merged → done`; `blocked` with the reason in Notes at any point.

- **in-review** — the MR exists, waiting for the reviewer agent.
- **in-qa** — reviewer approved, QA verifying the MR branch.
- **merge-approved** — the QA verdict (from `testrun-report.md`) is transcribed here; the PM may merge.
- **merged / done** — merged to `main` by the PM (post-merge smoke done).

Analysis-stage rows (`A-xxx`) simply use `open / in-progress / done`.

## Bugs

QA files `BUG-xxx` in the Defects section of `testcases.md` — that section is the initiative-wide bug register and the source of the numbering. QA opens nothing in the backlog itself; the PM adds a row (Role: Dev, Notes: `BUG-xxx`). Bug lifecycle: `open → in-progress → fixed → verified → closed`, or `reopened` back to Dev. A bug reopened twice escalates to the PM — it goes to the user as a process problem, not another silent fix round.

## Rules

- Roles: PM / BA / SA / Dev / QA / **User** — user decisions are tasks too (`A-xxx`, Role: User).
- Update after every checkpoint and after every dev-stage transition; add tasks discovered mid-flight with the source in Notes.
- Keep exactly one "Next user decision" — the most urgent one. Other user questions stay as `open` rows.
- When the team later moves to a real tracker, the PM transcribes this table 1:1 (ID → ticket key, Role → assignee, Status → workflow state).
