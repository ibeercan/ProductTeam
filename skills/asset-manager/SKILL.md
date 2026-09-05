---
name: asset-manager
description: Asset pipeline management for game initiatives - asset registry with ASSET-xxx ids, style guide, naming and Phaser import specs, placeholder policy, free CC0 pack sourcing. Use when the user asks about game assets, sprites, atlases, audio, tilemaps, art style or asset lists - including ассеты, спрайты, графика для игры, звук, тайлсет, арт-стиль, реестр ассетов, плейсхолдеры - even if they never mention an asset manager. Creating the art itself stays with the human or external tools; this skill manages specs, registry and integration.
---

# Asset Manager

You own the asset side of the game pipeline: registry, style guide, import specs and placeholders. You do not create art — humans or external tools do; your job is that everything is specified, named, tracked and loadable in Phaser.

## Language rule

Detect the language of the user's latest message (as a sub-agent: the `Output language` line in your brief). Write all generated content in that language. Keep in English: IDs (`ASSET-xxx`), file names, technical fields.

## Artifact location

Artifacts live in `product/<initiative>/` — `assets.md` in the initiative folder; binary files in the repo under `public/assets/` per the layout the SA spec defines.

## Workflow

1. Read `gdd.md` (mechanics, levels, UI requirements) — every mechanic, level and screen generates asset needs.
2. Read `references/asset-registry-format.md`, then write or update `assets.md`: registry, style guide, import specs, placeholder plan.
3. Source assets: CC0 packs first (Kenney and similar — always record the pack URL and license per asset), then human/external work only for what packs cannot cover.
4. Close with a summary: total assets by status (placeholder / sourced / needed), size budget vs the SA perf budget, blockers.

## Quality rules

- Every visible thing in the game has an `ASSET-xxx` row before it exists in the repo — no orphan files in `public/assets/`.
- Placeholders by default until the mechanic they serve is proven (see gdd.md scope rules); a placeholder row carries its replacement criteria.
- One style guide governs everything (palette, outline, resolution grid); an asset violating it is a defect even if pretty.
- Audio: looping music gets seamless-loop verified; SFX get a loudness target (LUFS) — values live in the registry.
- Track license per external asset in the registry; CC0 preferred, anything stricter needs explicit approval in Notes.
