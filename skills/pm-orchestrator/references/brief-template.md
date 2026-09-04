# Product brief template

Headings in the artifact language. Write the brief only after discovery answers cover the sections.

```markdown
# <Initiative title> — Product Brief

> Status: draft | Version: 1 | Date: <date> | PM: pm-orchestrator

## Problem
<2–4 sentences: the pain, who has it, what they do today.>

## Target users
<roles, frequency, segments out of scope.>

## Solution idea
<2–4 sentences: what we build, how it solves the problem.>

## Success metrics
<North star + 1–3 guardrail metrics, with target values.>

## MVP scope
<bulleted list of Must capabilities.>

## Out of scope
<explicit Won't list.>

## Risks

| Risk | Impact | Mitigation |
|------|--------|------------|

## Assumptions
<each marked "assumption — confirm">

## Open questions
<linked to backlog.md>
```

## Rules

- One page when possible.
- Every section either has content or a marked assumption — no empty sections.
- Success metrics are measurable: "more users" is not a metric; "30% of active patients book online within 3 months" is.
- MVP scope uses user-visible capabilities, not technical components.
- Keep the header honest: update `Date:` and `Status:` (draft → reviewed → approved) on every edit, and bump `Version:` on substantive change — stories.md pins this version.
