# Code review checklist

Findings format (in the artifact language):

| # | Severity | Location | Issue | Suggestion |
|---|----------|----------|-------|------------|
| 1 | major | api/booking.ts:42 | No handling for a slot taken a second ago (FR-002) | Return 409 with alternative slots |

Severity: **blocker** — must not merge (breaks the spec, data loss, security); **major** — will cause defects or rework; **minor** — readability/style.

## Walk the diff

- **Spec fidelity:** the diff implements exactly the linked FRs; edge cases from the story's ACs are handled.
- **Correctness:** error paths handled; concurrency/state issues; boundary conditions; no magic values.
- **Tests:** new behaviour has tests; tests assert behaviour, not implementation details; existing tests stay meaningful.
- **Security:** no secrets, keys or tokens; inputs validated; authorization checked server-side.
- **Scope:** nothing outside the task; no "small" refactors riding along; no dead code or debug leftovers.
- **Maintainability:** naming matches the domain; copy-paste that begs for a function is flagged; new dependencies are justified.

## Verdict

- `approve` — no open blockers or majors; minors may stay when fixing them is not worth the churn.
- `request-changes` — findings table attached; the author fixes in the same MR, then re-requests review.

Review etiquette: discuss the code, not the author; every finding states *why* it matters, not just taste.
