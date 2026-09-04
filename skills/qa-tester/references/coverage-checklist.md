# Coverage checklist

Walk per story before declaring coverage done:

- **Equivalence classes:** for every input with a range — one valid class and each invalid class.
- **Boundaries:** min, min+1, max−1, max, empty, zero; date and money edges.
- **Negative paths:** invalid input, permission denied, required data missing, network/timeout failure, double submission, concurrent modification.
- **State transitions:** every arrow in the entity's state model has a case (create → activate → suspend → …).
- **CRUD & cascade:** create / read / update / delete, plus what happens to dependent entities.
- **i18n / data:** long strings, unicode/emoji, wrong locale formats — when the story touches free text.
- **Authorization:** each role mentioned in the story — allowed and forbidden actions.

## Prioritization

- **P1** — money movement, data loss, security, the single core flow of the initiative.
- **P2** — all main scenarios of Must stories.
- **P3** — Could-story scenarios and cosmetics.

## Gaps

If a class cannot be tested (no environment, no test data), list it under "Not testable" in the report with the reason — never drop it silently.
