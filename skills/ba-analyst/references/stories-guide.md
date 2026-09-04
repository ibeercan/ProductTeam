# User stories standard

Read this before writing or updating `stories.md`.

## File structure

```markdown
# <Initiative title> — User Stories

> Version: 1 | Source: brief.md v1 | Status: draft

## Summary

| ID | Title | MoSCoW | Status |
|----|-------|--------|--------|
| US-001 | Booking an appointment | Must | draft |

## US-001: Booking an appointment

**As a** patient, **I want** to book an available slot online, **so that** I don't have to call the clinic.

### Acceptance criteria

- **AC1** Given the schedule has free slots, when I select a slot and confirm, then the slot is booked and I see a confirmation.
- **AC2** Given the slot was taken a second ago, when I confirm, then I see an explicit "slot is no longer available" message and alternative slots.

### Notes
- <constraints, links, open questions>

## Traceability

| Source | Stories |
|--------|---------|
| brief.md «Online booking» | US-001, US-002 |
```

## Rules

- Title is a short capability phrase; the full sentence goes in the As-a / I-want / So-that line.
- Typical story: 3–7 acceptance criteria. More than that — split the story.
- MoSCoW: **Must** — release fails without it; **Should** — painful, but a workaround exists; **Could** — nice to have; **Won't** — explicitly out of this release. Keep Won't items listed: they prevent scope debates later.
- Status values: `draft` / `reviewed` / `agreed`. Update the header `Date` and Summary `Status` on every edit.
- Bump `Version` on every substantive change — a story, AC or priority changed, not a typo fix. Downstream artifacts (spec, test cases) pin this version, so an invisible edit is a false contract.

## INVEST checklist

Independent (no hard ordering), Negotiable (outcome, not a contract), Valuable (user or business gains), Estimable (team can size it), Small (fits in a sprint), Testable (ACs exist). A story failing I or S usually hides two stories.

## Example fragments

Russian:

- **US-003:** Как пациент, я хочу перенести запись на другое время, чтобы не терять запись при изменении планов.
- **AC1:** Дано у меня есть активная запись, когда я выбираю «Перенести» и новый слот, то старый слот освобождается и новая запись подтверждается за одно действие.

English:

- **US-003:** As a patient, I want to reschedule my appointment so that I keep it when plans change.
- **AC1:** Given I have an active appointment, when I pick "Reschedule" and choose a new slot, then the old slot is released and the new booking is confirmed in one action.
