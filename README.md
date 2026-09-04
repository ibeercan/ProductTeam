# ProductTeam

A virtual product team for [ZCode](https://z.ai): five role skills that take a product initiative from a raw idea to a merged pull request — a product manager orchestrating business analysts, a system analyst, developers and QA, all as briefed sub-agents with user checkpoints.

> Extend ZCode with skills, commands, and MCP servers from plugins.

## How it works

You always talk to the product manager. The specialists are sub-agents the PM briefs and supervises; every stage ends at a checkpoint where you review artifacts and approve the next step.

```
You  ↔  PM (pm-orchestrator)          ← discovery, checkpoints, backlog, merge
            ├─ BA  (ba-analyst)   → stories.md, process.md
            ├─ SA  (sa-analyst)   → spec.md, diagrams.md, tasks.md
            ├─ Dev (dev-engineer) → one MR per task + cross-review
            └─ QA  (qa-tester)    → testcases.md, run journal, merge verdict
```

Pipeline: **discovery → brief → user stories → spec + task decomposition → requirements gate → test design → [implement → review → verify → merge] per task → final regression.** Documentation-only initiatives finish after test design; the implementation cycle activates when the initiative is tied to a code repository.

## The five skills

| Skill | Role |
|-------|------|
| `pm-orchestrator` | Product manager: discovery, brief, backlog (single writer), sub-agent briefs, requirements gate, the only actor who merges |
| `ba-analyst` | Business analyst: user stories with Given/When/Then acceptance criteria, MoSCoW, as-is/to-be process maps, traceability |
| `sa-analyst` | System analyst: technical spec (FR ↔ story), integrations, NFRs, C4/sequence/ER diagrams, decomposition into one-MR tasks, spec audits |
| `dev-engineer` | Developer: one task = one MR, conventional commits, self-test before handoff; separate reviewer workflow with a code-review checklist |
| `qa-tester` | QA: requirements testability gate, test cases with AC coverage, per-MR verification, `merge-approved`/`hold` verdicts, append-only run journal, bug lifecycle |

## Built-in quality gates

- **Requirements gate** — an SA audit plus a QA testability review (both recorded in `gate-report.md`) must pass before development starts.
- **Cross-review** — the MR author and the code reviewer are always different agent instances.
- **Merge gate** — merging into `main` happens only after the QA verdict `merge-approved` is recorded in the run journal; the PM executes the merge. User overrides are possible but must be explicit and are recorded.
- **Bug loop** — failed test → `BUG-xxx` → fix MR → re-test with adjacent regression; a bug reopened twice escalates to the user.

## Artifacts and conventions

Each initiative lives in `product/<initiative>/` in the project root: `brief.md`, `backlog.md`, `stories.md`, `process.md`, `spec.md`, `tasks.md`, `gate-report.md`, `diagrams.md`, `testplan.md`, `testcases.md`, `testrun-report.md` (append-only journal).

- **ID chain:** `US-xxx` (stories) → `FR-xxx` (spec) → `T-xxx` (tasks) → `TC-xxx` (test cases); backlog admin and user-decision rows use `A-xxx`; defects use `BUG-xxx` with a single register.
- **Single writers:** only the PM writes `backlog.md` and merges; QA owns verdicts; SA owns the task list.
- **Versioning:** every artifact carries an integer `Version` bumped on substantive change; downstream artifacts pin source versions (`Source: spec.md v3`), so a bumped upstream makes drift visible — dependents update or record "checked — no impact", and an open MR whose spec moved gets flagged at review instead of merging silently.
- **Language:** artifacts follow the language of your latest message — work in Russian, English or anything else. IDs, Gherkin keywords, mermaid syntax and file names stay English.
- **VCS:** GitHub via `gh` out of the box; GitLab via `glab` when installed.

## Installation

### As a plugin marketplace (recommended)

This repository is a plugin marketplace index. In ZCode: Settings → Plugin Management → add marketplace → point it at this repo (`ibeercan/ProductTeam`), then install **ProductTeam** from it.

### Manual

```bash
git clone https://github.com/ibeercan/ProductTeam.git
# per-skill, for all your projects:
cp -r ProductTeam/skills/* ~/.agents/skills/
# or per-project (versioned with the repo):
cp -r ProductTeam/skills/* <your-project>/.agents/skills/
```

After installing, start a fresh session and check Settings → Skills lists all five skills.

## Usage

Open ZCode in your project folder and talk to the PM — in any language:

- «есть идея: онлайн-запись к врачу» / "I have an idea: online appointment booking"
- «составь user stories по этому брифу» / "turn this brief into user stories"
- «нужен тест-план для US-001…US-007» / "write a test plan for US-001…US-007"
- «реализуй задачу T-003» / "implement task T-003" (goes to dev-engineer)
- «проверь MR #12» / "verify MR #12" (goes to qa-tester)

Force-load any skill directly with `/skill <name>`.

## Development

The skills are plain markdown (a `SKILL.md` with YAML frontmatter plus `references/` per skill) — edit them like any documentation. The recommended loop comes from the `skill-creator` skill: draft → try 2–3 realistic test prompts in a fresh session → review outputs → adjust the wording, especially the trigger descriptions. See [CHANGELOG.md](CHANGELOG.md) for release history; versioning follows SemVer.

## License

[MIT](LICENSE)
