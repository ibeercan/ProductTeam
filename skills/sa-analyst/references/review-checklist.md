# Spec / code review checklist

Findings table format (headings and text in the artifact language):

| # | Severity | Location | Issue | Recommendation |
|---|----------|----------|-------|----------------|
| 1 | blocker | spec.md §4 | Payment provider undefined | Choose provider; blocked stories US-004, US-005 |

Severity: **blocker** — development cannot proceed; **major** — will cause rework or defects; **minor** — clarity/style.

## Walk the checklist

- **Ambiguity:** terms without a glossary definition; "etc.", "fast", "user-friendly"; unbounded lists.
- **Contradictions:** two requirements conflict; spec vs stories; two diagrams disagree.
- **Completeness:** error paths undefined; NFR categories empty; integration error handling missing; data retention unstated.
- **Traceability:** FR without a source story; stories without FR coverage; a test case impossible to write from the requirement as stated.
- **Testability:** requirement cannot be verified pass/fail as written.
- **Scope:** requirements with no story and no brief section — report to the PM, never silently expand the spec.

Close the review with a one-paragraph verdict: ready for development / ready after N fixes / blocked on <list>.
