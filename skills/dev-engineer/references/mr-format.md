# MR format

## Branch naming

`feature/T-001-<short-slug>` for tasks, `fix/bug-002-<short-slug>` for bug fixes. Base branch: `main`.

## MR description template

```markdown
## T-001: <task title>

**Implements:** FR-001, FR-002 (US-001) | **Task:** T-001 | **Spec:** v3 | **Initiative:** <name>

### What changed
<3–6 bullets>

### How to test (for QA)
<exact steps: environment, data setup, what to run, expected results per linked TC>

### Evidence
<test run output summary; screenshots for UI changes>

### Checklist
- [ ] Build, linters and tests green
- [ ] New behaviour covered by tests
- [ ] Self-reviewed the diff
- [ ] Scope matches the task — nothing extra
- [ ] `Spec:` version still current (spec.md unchanged since MR was opened)

### Notes
<deviations from spec, noticed-but-not-fixed issues with a reason, follow-up candidates>
```

## Commands (GitHub)

```bash
gh pr create --base main --head feature/T-001-booking --title "T-001: <title>" --body-file mr.md
gh pr checks <number>   # CI status before handing off to QA
```

GitLab remotes: the same flow via `glab mr create` when installed.

## Merge (performed by the PM, not the author)

Merging happens only after the QA verdict `merge-approved` is recorded in the backlog — and it is the PM who executes it (`gh pr merge <number> --squash --delete-branch`, or per repo convention), updates the backlog row to `merged`, and orders the post-merge smoke from QA. The author does not merge, delete branches, or edit the backlog.
