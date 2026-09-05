# Changelog

All notable changes to this project are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and versioning follows [SemVer](https://semver.org/).

## [1.2.0] — 2026-09-05

### Added — game dev mode (indie games on Phaser 3)

- **`game-designer` skill**: GDD standard (pillars, core loop, `MECH-xxx` mechanics with "fun because…" + testable behavior), balance tables (`BAL-xxx`, markdown or xlsx via the document skill), level briefs (`LVL-xxx`), optional narrative standard (characters, quests `QUEST-xxx`, dialogue trees in mermaid). Replaces the BA stage for game initiatives.
- **`asset-manager` skill**: asset registry (`ASSET-xxx` = Phaser load keys), style guide, Phaser import specs (spritesheets, atlases, Tiled-JSON tilemaps, ogg/mp3 audio), placeholder-first policy, CC0 sourcing with per-asset license tracking.
- **`sa-analyst` game architecture reference (Phaser 3)**: TS + Vite stack, scene architecture with logic outside scenes, generated balance constants module bound to `BAL-xxx`, versioned save schema with migrations, Vitest strategy.
- **`qa-tester` game QA reference**: playtest protocol (first minute, core loop N≥3, friction log, per-pillar fun verdict), frame-time performance budgets, save-integrity cases (corrupt/upgrade), browser matrix; live smoke via `web-gui-tester` (main agent).
- **`pm-orchestrator`**: game pipeline branch (game-designer stage instead of BA; asset-manager stage after SA decomposition) and a game block in the discovery question bank (engine, session shape, scope fence, art policy, release target).

## [1.1.2] — 2026-09-04

### Added

- Concurrency guardrails in `pm-orchestrator`: parallel sub-agent runs are allowed only in safe slots (reviewers, QA verifiers, the two requirements-gate reviews — all read-only over diffs). Parallel dev-authors over one working copy are explicitly forbidden (shared git index); if parallel authoring is needed, the PM must first create separate `git worktree` checkouts, one per task. Merges stay serialized.

## [1.1.1] — 2026-09-04

### Changed

- Sub-agent brief template: skill loading is now a strict two-step — primary route is the Skill tool by name (uniform `Skill: <role>` trace, catches broken installs early), explicit SKILL.md file read as fallback, Context/Rules of the brief as the last resort. Previously the wording allowed both routes, so different agents picked different ones.

## [1.1.0] — 2026-09-04

### Added

- **Artifact versioning across the pipeline**: every artifact (brief, stories, spec, tasks, test cases) carries an integer `Version` bumped on substantive change; downstream artifacts pin exact source versions (`Source: spec.md v3`) instead of dates.
- **Drift protection**: a bumped upstream forces dependents to update or record "checked — no impact"; a spec bump after the requirements gate re-runs the gate; MR descriptions pin the spec version (`Spec: v3`) and reviewers flag an MR whose spec moved instead of approving; test run journal records the doc versions verified (`Docs: spec v3, tasks v2`).
- Worked example extended with the version chain (spec v1 fails the gate → v2 passes → all pins follow).

## [1.0.1] — 2026-09-04

### Added

- Marketplace support: `.claude-plugin/marketplace.json` index — the repository can now be added directly as a plugin marketplace in ZCode (and Claude Code-compatible clients).
- Claude-compatible plugin manifest `.claude-plugin/plugin.json` alongside the native `.zcode-plugin/plugin.json`.
- Plugin icon (`assets/icon.svg`), marketplace category and keywords.

## [1.0.0] — 2026-09-04

Initial release.

### Added

- **pm-orchestrator** — product manager entry point: discovery question bank, product brief template, file-based backlog (single-writer), sub-agent brief templates for every stage, requirements gate, user checkpoints, merge execution after the QA verdict.
- **ba-analyst** — user stories with Given/When/Then acceptance criteria, INVEST checks, MoSCoW prioritization, as-is/to-be process maps with mermaid conventions, glossary, traceability table.
- **sa-analyst** — technical specification template (FR ↔ story traceability, integrations, data model), NFR checklist, C4/sequence/ER diagram conventions, spec and code review checklist, implementation decomposition into one-MR tasks (`tasks.md`).
- **dev-engineer** — author workflow (one task = one MR, conventional commits, self-test before handoff, MR description format with QA instructions) and a separate reviewer workflow with a code-review checklist; merge and backlog writes belong to the PM.
- **qa-tester** — requirements testability gate, test case standard with AC coverage, coverage checklist (equivalence classes, boundaries, negative paths), per-MR verification with the `merge-approved`/`hold` verdict, append-only test run journal, bug lifecycle with escalation, smoke/regression checklists; live browser execution stays with the main agent.
- Cross-cutting conventions: initiative artifacts in `product/<initiative>/`, ID chain `US-xxx → FR-xxx → T-xxx → TC-xxx` with `A-xxx` backlog admin rows and a `BUG-xxx` register, artifact language follows the user's latest message, bilingual trigger descriptions.
