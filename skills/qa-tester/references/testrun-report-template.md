# Test run journal (testrun-report.md)

One file per initiative, **append-only**: every run is a new dated section. Never rewrite or delete earlier sections — they are the merge-gate evidence chain.

## Section template

```markdown
## <YYYY-MM-DD> — <scope> — <T-xxx / MR #n>

> Build/env: <...> | Branch: feature/T-010-... | MR head: <commit> | Executed by: <agent/user>

### Summary

| Result | Count | % |
|--------|-------|---|
| Passed | 4 | 100% |
| Failed | 0 | 0% |
| Blocked | 0 | 0% |

### Verdict

merge-approved | hold (<what blocks it and what unblocks it>)

### Failures

| TC | BUG | Symptom | Severity |
|----|-----|---------|----------|

### Not testable

| TC/Class | Reason |
|----------|--------|

### Notes & next steps
<retest list, regression risk, evidence paths>
```

`<scope>` is one of: `task verification` | `smoke` | `regression` | `full`.

## Rules

- A **task verification** section (one per MR) must contain the Verdict: `merge-approved` is the QA command that allows the PM to merge; `hold` states exactly what blocks it and what unblocks it.
- The verified build must be the MR head commit; if new commits landed after testing, re-run before approving.
- Percentages are of executed cases; **blocked** means a precondition was not met — that is not a failure.
- Every failure references a TC and, once filed, a BUG id (register: Defects section of `testcases.md`).
- Evidence (screenshot paths from live runs) goes into the run's Notes.
- End full/regression runs with a release recommendation (go / no-go / conditional).
