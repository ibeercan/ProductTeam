# Asset registry format (assets.md) — Phaser pipeline

Read before writing or updating `assets.md`.

## File structure

```markdown
# <Game> — Asset Registry

> Version: 1 | Source: gdd.md v1 | Repo path: public/assets/

## Style guide
<palette (hex list), outline rule, base grid (e.g. 16×16 or 32×32), animation fps convention, audio loudness target>

## Registry

| ID | Need (from) | Type | File | Spec | Status | Source / license |
|----|-------------|------|------|------|--------|------------------|
| ASSET-001 | MECH-001 dash | spritesheet | dash_fx.png | 6 frames 32×32, atlas row | placeholder | code-drawn |
| ASSET-002 | LVL-001 walls | tileset | tiles_dungeon.png | 16×16, 1 margin, 1 spacing | sourced | kenney.nl pixel-pack, CC0 |
| ASSET-010 | Menu | audio | theme_loop.ogg | seamless loop, -18 LUFS, ≤ 1.5 MB | needed | — |

## Placeholder plan
<which placeholders ship into the first playable; replacement criteria per row>

## Size budget
<per-group and total MB vs the perf budget in spec.md §6>
```

## Phaser import specs — fill `Spec` with these exact fields

- **Spritesheet:** frame width/height (px), margin, spacing — `this.load.spritesheet(key, path, { frameWidth, frameHeight, margin, spacing })`.
- **Texture atlas:** atlas PNG + JSON (Phaser format or TexturePacker array) — prefer atlases over loose sheets for anything animated.
- **Tilemap:** Tiled map exported as **JSON** (`.tmx` → File → Export As → JSON) + tileset image; map ids match `LVL-xxx`.
- **Audio:** `.ogg` (Chrome/Firefox) + `.mp3` fallback for Safari; music as `.ogg` loop points verified; keep every file ≤ 1.5 MB unless the budget says otherwise.
- **Bitmap font / UI:** bitmap font PNG+XML or web font (woff2 in repo, not CDN — offline builds).

## Rules

- Keys in code (`this.load.*` first argument) equal the `ASSET-xxx` id — greppable from registry to code.
- One row per loadable unit (an atlas is one row, not one per frame).
- Status values: `placeholder` / `sourced` / `needed` / `integrated` (loaded from the game's Boot scene).
- The SA task list references ASSET ids where integration work exists (e.g. preload manifest task); the registry pins gdd.md version.
