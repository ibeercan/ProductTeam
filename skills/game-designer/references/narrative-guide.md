# Narrative standard (narrative.md) — optional

Only for games where story carries value. Skip this file entirely otherwise.

## File structure

```markdown
# <Game> — Narrative

> Version: 1 | Source: gdd.md v1

## 1. Tone & framing
<3–5 sentences: genre voice, what the writing must never do>

## 2. Characters

| ID | Name | Role | Voice note |
|----|-------|------|-----------|
| CHR-01 | Mo the Engineer | guide | short sentences, never explains twice |

## 3. Quests / story beats

| ID | Beat | Gate (mechanic) | Pays into (pillar) |
|----|------|-----------------|--------------------|
| QUEST-01 | First signal | completes LVL-002 | Mystery |

## 4. Dialogue trees
```mermaid
flowchart TD
    D1{Mo: "You heard that?"} -->|Ask what| D2[Mo explains the signal]
    D1 -->|Ignore| D3[Mo shrugs; QUEST-01 hint stays in log]
    D2 --> E([end: QUEST-01 accepted])
    D3 --> E2([end: QUEST-01 available later])
```

## 5. Text inventory
<every player-visible string group: UI labels, item names, death messages — count them; localization decisions live here>

## 6. Open questions
```

## Rules

- Every `QUEST-xxx` gates on a mechanic or level (`MECH-xxx`/`LVL-xxx`) — a quest that is only text is a cutscene, mark it as such.
- Dialogue trees are mermaid `flowchart` with explicit branch outcomes; every branch ends somewhere (no dead options).
- Writing quality bar: the tone section is the contract; every drafted line is checked against it.
- SA derives from here exactly like from GDD: dialogue trees → data files, text inventory → strings module. Text content is data, not code.
- Version discipline as everywhere else.
