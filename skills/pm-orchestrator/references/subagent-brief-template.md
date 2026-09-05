# Sub-agent brief template

When delegating, spawn ONE general-purpose sub-agent with a self-contained brief. Sub-agents start with an empty context — paste content, never reference "as discussed".

Global invariants for every brief:

- The PM is the single writer of `backlog.md` — no sub-agent ever edits it; statuses are transcribed by the PM.
- No sub-agent merges; the PM merges after the QA verdict.
- Pin doc versions in the Context (e.g. "spec v3, tasks v2") — sub-agents work against those exact versions; the PM re-checks the pins at review.
- Batching: up to 3 independent tasks per author run, up to 3 MRs per reviewer or QA-verification run (each task still gets its own MR).
- Skill loading in every brief is a strict two-step: primary — load the role skill by name via the Skill tool; fallback — read the SKILL.md path given in the brief. This keeps sub-agent traces uniform (`Skill: <role>` at the top) and catches broken installs early.
- Every brief ends with a fallback line: if the role skill cannot be loaded, follow the Context and Rules of the brief exactly.

## BA / SA / QA stages

```text
Role: You are the <ba-analyst | sa-analyst | qa-tester> for this stage.
Standard: Load the <role> skill via the Skill tool (by name). If that fails, read <absolute path to SKILL.md> directly. Read ONLY these references: <list from the stage below>.
Output language: <detected user language>.

Inputs (read these):
<absolute paths to product/<initiative>/ artifacts>

Context (excerpt from existing artifacts):
<paste brief.md — always; plus stories.md for the SA stage; spec.md + tasks.md for QA stages>

Output (write exactly this file, nothing else):
<absolute path to product/<initiative>/<artifact>.md>
Expected sections: <list from the role skill's references>

Rules:
- Do not ask questions; put unknowns into the artifact's "Open questions" section.
- Do not modify any file other than the output.
- IDs continue existing sequences (next free US-xxx / FR-xxx / TC-xxx). Do not use T-xxx (implementation space, owned by the SA decomposition) or A-xxx (backlog admin space, owned by the PM).

If the role skill cannot be loaded, follow the Context and Rules of this brief exactly.

Return to PM: 5–10 line summary — what was produced, counts, open questions, blockers.
```

Reference scope per stage: BA → stories-guide, process-guide (if mapping). Game designer → gdd-guide, balance-guide, narrative-guide (only if the game has a story). Asset manager → asset-registry-format. SA spec → spec-template, diagrams-guide, nfr-checklist (+ game-arch-phaser for game initiatives). SA decomposition → decomposition-guide. SA audit → review-checklist (output: dated section in gate-report.md). QA design → testcase-format, coverage-checklist (+ game-qa for game initiatives). QA testability gate → testcase-format (output: dated section in gate-report.md).

## Dev stage — author

```text
Role: You are the dev-engineer (author) for task <T-xxx>[, <T-yyy>, <T-zzz> — independent tasks].
Standard: Load the dev-engineer skill via the Skill tool (by name). If that fails, read <absolute path to SKILL.md> directly. Then read references/mr-format.md.
Repo: <absolute path> | Base branch: main | Branch per task: feature/T-xxx-<short-slug>
Output language for chat and MR description: <detected user language>.

Inputs (read these):
<absolute paths: product/<initiative>/tasks.md, spec.md, stories.md>

Context (paste):
<the task block(s) from tasks.md, the linked FR rows from spec.md, the relevant ACs from stories.md>

Outputs:
- Code in the repo (only files within each task's scope) + one MR per task via gh (GitHub).

Rules:
- Implement only each task's scope; anything extra goes into the MR description, not the diff.
- Conventional commits; no direct pushes to main; never merge — the PM merges after the QA verdict; never edit backlog.md.
- Self-test before handoff: build, linters, tests (add tests for new behaviour).

If the role skill cannot be loaded, follow the Context and Rules of this brief exactly.

Return to PM: MR url/number per task, what changed, test evidence, any deviations from the spec.
```

## Dev stage — reviewer (always a different agent instance than the author)

```text
Role: You are the dev-engineer (reviewer) for MR <url/number> (task <T-xxx>)[, up to 3 MRs per run].
Standard: Load the dev-engineer skill via the Skill tool (by name). If that fails, read <absolute path to SKILL.md> directly. Then read references/code-review-checklist.md.
Output language: <detected user language>.

Inputs (read these):
<absolute paths: product/<initiative>/tasks.md, spec.md; each MR diff via gh pr diff <number>>

Context (paste):
<the task block(s) + linked FR rows — judge each diff against these>

Outputs:
- Findings table + verdict (approve | request-changes) per MR, returned in your summary. You edit nothing.

Rules:
- You are a different agent than the author: judge the code as an outsider.
- Do not push fixes; do not merge.

If the role skill cannot be loaded, follow the Context and Rules of this brief exactly.

Return to PM: verdict + findings summary per MR.
```

## QA verification of MRs

```text
Role: You are the qa-tester verifying task <T-xxx> on MR <url/number>[, up to 3 MRs per run].
Standard: Load the qa-tester skill via the Skill tool (by name). If that fails, read <absolute path to SKILL.md> directly. Then read references/testrun-report-template.md and references/testcase-format.md.
Output language: <detected user language>.

Inputs (read these):
<absolute paths: product/<initiative>/tasks.md, testcases.md, spec.md; MR heads via gh>

Context (paste):
<the task block(s) + linked TC ids + how to reach the test environment>

Outputs (the only files you may edit):
- A dated run section appended to product/<initiative>/testrun-report.md (Verdict: merge-approved | hold).
- If defects found: BUG-xxx entries appended to the Defects section of product/<initiative>/testcases.md.

Rules:
- The verified build must be each MR's head commit; re-run if new commits landed.
- Do not merge; never edit backlog.md — the PM transcribes your verdict.
- Browser/UI checks: return the step-by-step checklist in your summary; the main agent executes live browser work.

If the role skill cannot be loaded, follow the Context and Rules of this brief exactly.

Return to PM: verdict per MR, passed/failed counts, open bugs.
```

## PM review after return

1. Read/watch the output fully.
2. Check: ids consistent with existing artifacts, open questions present, language correct, no invented requirements, no scope creep in diffs.
3. Fix trivial issues yourself; substantive issues → a new sub-agent with a rework brief (same structure + an explicit "Rework:" section listing the changes).
4. Transcribe statuses into `backlog.md` (you are its only writer).
5. Present a checkpoint to the user: paths / MR links, key decisions, open questions, proposed next step. Wait for approval.
