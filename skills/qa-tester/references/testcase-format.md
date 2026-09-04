# Test case standard

## File structure (testcases.md)

```markdown
# <Initiative> — Test Cases

> Source: stories.md v<date>, spec.md v<date>

## Coverage summary

| Story | AC | Cases | Types |
|-------|----|-------|-------|
| US-001 | AC1 | TC-001 | positive |

## TC-001: <Short title>

- **Linked:** US-001/AC1
- **Type:** positive | negative | boundary
- **Priority:** P1 | P2 | P3
- **Preconditions:** ...

| # | Step | Expected |
|---|------|----------|
| 1 | ... | ... |

- **Postconditions:** ...
```

## Rules

- Title states the verified behaviour, not the action ("Booking fails when the slot is already taken").
- Every step has its own expected result; a case has exactly one verification objective.
- Preconditions only state what the case itself does not create.
- Found defects go to a `## Defects` section as `BUG-001`-style entries (steps to reproduce, actual vs expected, severity) — not into the cases. That section is the initiative-wide bug register: numbering continues here (next free = the max across all initiative artifacts); testrun reports and backlog rows reference it, they never renumber it.
- Coverage summary is regenerated on every edit: every AC of every story appears there with at least one TC id.
