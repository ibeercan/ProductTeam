# Worked example — the ID chain end to end

A miniature initiative showing how every ID links. Initiative folder: `product/clinic-booking/`. Use it as the anchor for consistency: every ID has exactly one home artifact, every link references an existing ID.

## brief.md (excerpt)

> Status: approved | Date: 2026-09-04

- **Problem:** patients book clinic visits by phone; reception drowns in calls.
- **MVP scope:** online booking of available slots; rescheduling; cancellation.

## stories.md (excerpt)

| ID | Title | MoSCoW | Status |
|----|-------|--------|--------|
| US-001 | Book an appointment online | Must | agreed |

**US-001:** As a patient, I want to book an available slot online, so that I don't have to call the clinic.

- **AC1** Given free slots exist, when I confirm a slot, then I receive a booking number.
- **AC2** Given the slot was taken a second ago, when I confirm, then I see "slot unavailable" and alternative slots.

## spec.md (excerpt)

| ID | Story | Requirement | Priority |
|----|-------|-------------|----------|
| FR-001 | US-001 | POST /bookings accepts a slot id and patient id and returns a booking number. | Must |
| FR-002 | US-001 | Booking an already-taken slot returns 409 with alternative slot ids. | Must |

## tasks.md (excerpt)

| ID | Parent | Task | FR | Depends on | MR scope | Status |
|----|--------|------|----|------------|----------|--------|
| T-001 | — | Booking API endpoints | FR-001, FR-002 | — | api/ + tests | merged |
| T-002 | — | Slot conflict handling | FR-002 | T-001 | conflict module + tests | in-qa |

## testcases.md (excerpt)

| Story | AC | Cases | Types |
|-------|----|-------|-------|
| US-001 | AC1 | TC-001 | positive |
| US-001 | AC2 | TC-002, TC-003 | negative, boundary |

## backlog.md (excerpt, written by the PM only)

| ID | Task | Role | Status | Artifact | Notes |
|----|------|------|--------|----------|-------|
| A-001 | Elicit user stories from brief | BA | done | stories.md | |
| A-002 | Requirements gate | SA+QA | done | gate-report.md | PASS 2026-09-04 |
| T-001 | Booking API endpoints | Dev | merged | MR #7 | |
| T-002 | Slot conflict handling | Dev | in-qa | MR #9 | |

## Where each verdict lives

- **Requirements gate** → `gate-report.md`: dated SA-audit and QA-testability sections, PASS/FAIL.
- **Merge command** → `testrun-report.md`: a task-verification run section ends with Verdict `merge-approved` or `hold`.
- **Statuses** → `backlog.md`: transcribed by the PM from the verdicts above — the only place statuses live.

## The chain, one line

`US-001` (stories) → `FR-001/FR-002` (spec) → `T-001/T-002` (tasks) → `TC-001..003` (testcases) — every AC covered, every task linked to FRs, every verdict recorded in its home artifact.
