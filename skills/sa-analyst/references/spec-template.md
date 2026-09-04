# Technical specification template

Read before writing or updating `spec.md`. Section headings in the artifact language; ids, file and folder names stay English.

## File structure

```markdown
# <Initiative> — Technical Specification

> Version: 1 | Source: stories.md v2, brief.md v1

## 1. Overview
<2–4 sentences: what is being built and for whom.>

## 2. Scope
**In:** ...
**Out:** ...

## 3. Functional requirements

| ID | Story | Requirement | Priority |
|----|-------|-------------|----------|
| FR-001 | US-001 | The booking API accepts a slot id and patient id and returns a booking number. | Must |

## 4. Integrations

### 4.1 <External system>
- **Purpose:** ...
- **Direction:** outbound / inbound
- **Data exchanged:** ...
- **Protocol & auth:** ...
- **Error handling:** timeouts, retries, fallback behaviour.

## 5. Data model
<Entities, key fields, relations in prose; full diagram in diagrams.md.>

## 6. Non-functional requirements

| Category | Requirement | Target |
|----------|-------------|--------|

## 7. Dependencies & assumptions
## 8. Open questions

| # | Question | Who answers | Blocks |
|---|----------|-------------|--------|
```

## Rules

- One row per requirement; atomic — a single behaviour per row.
- Requirements are testable: QA must be able to write a test case from the row alone.
- Priorities inherit from the source story's MoSCoW unless the PM changed them.
- The FR table is ordered by story id so coverage is checkable at a glance.
