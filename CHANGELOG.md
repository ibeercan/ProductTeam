# Changelog

All notable changes to this project are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and versioning follows [SemVer](https://semver.org/).

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
