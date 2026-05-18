---
name: deepwork-00-bootstrap
description: "**When: MUST — Run first for every new project. Sets up the project structure, tools, and foundation.** First entry point for any new project — even if the idea is still vague. Decides whether deepwork-01-discovery is the right next step, or whether a native brainstorm, spike, or reality check should come first. Creates foundational project documents (PROJECT.md, REQUIREMENTS.md, ROADMAP.md, STATE.md) natively — no external skills required. Use ALWAYS when: starting any new project, 'I have an idea', 'let's build X', 'neues Projekt', 'I want to make', 'let's start', '/deepwork', '/deepwork-00'. Even for rough, half-formed ideas — this skill decides what to do with them."
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
  - Task
  - AskUserQuestion
  - Skill
---

**Read first:**
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/tool-awareness.md` — Tool-Routing bei jedem ⚐
- `references/user-profile.md` — default assumption: non-technical user

# deepwork-00: Bootstrap

**Part 1 of the deepwork suite.** This skill's job is simple: get the project to a standing start so deepwork-01 can do real discovery work.

---

## Step 0 — Existing Project Check + Tool Inventory ⚐

**First: Check if this project already has deepwork structure.**

Does `./handoff.md` exist in the current working directory?

**YES → Read it. Parse the `current_phase` field:**
- `current_phase: 00-bootstrap` → Bootstrap was interrupted. Continue from Step 1 below.
- `current_phase: 01-discovery` or later → Bootstrap already complete. Output:
  ```
  Bootstrap already done (found handoff.md).
  Current phase: <value from handoff>
  Next skill to run: /deepwork-<NN>-<name>
  ```
  Stop here. Don't overwrite anything.
- `verdict: NO-GO` → Inform user: project was previously abandoned with NO-GO verdict. Offer to restart or continue from discovery with adjusted scope.

**YES, but `.deepwork/` directory is empty or missing foundation docs:** Continue bootstrap but skip any steps that are already done.

**NO → Continue with Tool Inventory below.**

---

Before anything else, run a tool check. Read the system-reminder for available skills, check `.mcp.json` for MCP servers, and scan for active Ruflo plugins.

Write `.deepwork/tool-inventory.md`:
```markdown
# Tool Inventory — <Project Name> — <date>

## Skills available
- <list from system-reminder>

## MCP servers
- <list from ~/.claude/.mcp.json + session-injected>

## Ruflo plugins
- ruflo-swarm: <yes/no>
- ruflo-autopilot: <yes/no>
- ruflo-loop-workers: <yes/no>
- ruflo-cost-tracker: <yes/no>
- ruflo-knowledge-graph: <yes/no>

## Key capabilities
- Swarm/parallel execution: <yes/no>
- Memory/vector persistence: <yes/no — which tier(s)>
- Autopilot loop: <yes/no>
- Deep web research (exa/firecrawl): <yes/no>
```

This file is read by every subsequent deepwork skill to know what's available.

---

## Step 1 — Quick Triage ⚐

Ask via `AskUserQuestion` — use as many questions as needed to understand the situation:

**User Profile Check ⚐** (read `references/user-profile.md` before interviewing):
- Assume the user is non-technical. Adjust all questions and explanations accordingly.
- Watch for questions that reveal knowledge gaps — note them in `.deepwork/decisions.md` as `kind:user-profile`.
- If the user shows technical knowledge, note which areas — but stay vigilant for gaps in adjacent domains.

**Round 1:** What stage is this?
- Rough idea / vague inspiration
- Concrete concept with some clarity
- Defined project with clear goals

**Round 2:** What exists already?
- Any prior research, docs, or code?
- Any constraints already decided?

**Round 3:** What needs to happen today?
- Explore and brainstorm first?
- Dive into discovery (research + planning)?
- Start building immediately (skip to deepwork-03)?

---

## Step 2 — Routing Decision ⚐

Based on triage answers, choose the path:

| Situation | Action |
|-----------|--------|
| Idea very vague, need to explore possibilities | Native Brainstorm Protocol ausführen (→ `references/native-protocols.md`), dann weiter zu Step 3 |
| Clear enough to investigate feasibility | Continue to Step 3 |
| Already have research/docs | Document Ingest Protocol ausführen (→ `references/native-protocols.md`), dann Step 3 |
| Want to spike a specific technical question first | Spike Protocol ausführen (→ `references/native-protocols.md`), dann Step 3 |
| Jumping straight to execution (plan already exists) | Handoff to deepwork-03 directly |

Document routing decision in `.deepwork/decisions.md`.

---

## Step 3 — Standard-Projektstruktur anlegen ⚐

Lege zuerst die vollständige Standard-Ordnerstruktur an.

**Anlegen (nur wenn noch nicht vorhanden):**
```
<project-root>/
├── .deepwork/
│   ├── planning/          ← Projektdefinition (PROJECT.md etc.)
│   ├── research/          ← Wird von deepwork-01 befüllt
│   ├── outputs/           ← Wird von deepwork-03 befüllt
│   ├── journal/           ← Fortschrittsnotizen aller Phasen
│   ├── decisions.md       ← Alle Entscheidungen chronologisch
│   ├── cost-log.md        ← Token/Kosten-Protokoll
│   ├── cost-summary.md    ← Kosten-Zusammenfassung
│   └── tool-inventory.md  ← (bereits in Step 0 erstellt)
```

**Wachstum über das Projekt-Leben (entsteht organisch):**
- `handoff.md` + `PLAN.md` + `VERDICT.md` → nach deepwork-01-discovery
- `outputs/<section-id>/` → nach jeder deepwork-03-Sektion
- `PROJECT-COMPLETE.md`, `NEXT-STEPS.md` → nach deepwork-end-report

**Obsidian-Sync vorbereiten** (wenn Vault aus `DEEPWORK-CONFIG.md` existiert):
Lege `<DEEPWORK_VAULT_PATH>\Projects\<project-slug>\Deepwork\` an — leer, bereit für spätere Synchronisation.

---

## Step 3.5 — Foundation Documents ⚐

Ensure the foundational project documents exist. These are not optional — deepwork-01 reads them.

Write these files unter `.deepwork/planning/` (native, direkt — kein externer Skill nötig):

`PROJECT.md` — What: project name, domain, core problem, target user, primary goal, key constraints.

`REQUIREMENTS.md` — Must-haves vs nice-to-haves vs explicitly-out-of-scope.

`ROADMAP.md` — High-level phases (no detail yet — deepwork-01 fills this in).

`STATE.md` — Current state: which phase, what's done, what's open.

These files are the foundation that every downstream agent reads to avoid re-asking decided questions.

---

## Step 4 — Token Log + Memory Init ⚐

Initialize `.deepwork/cost-log.md` and `.deepwork/decisions.md` (empty with headers).

Log bootstrap token cost (see `references/token-log-protocol.md` for format).

If Ruflo memory is available: store a bootstrap memory entry tagged `projekt:<slug>`, `phase:00`, `kind:decision`.

---

## Step 5 — Handoff to deepwork-01

Produce a clear block output:
```
Bootstrap abgeschlossen.
─────────────────────────────
Grundlagen-Dokumente: .deepwork/planning/ (oder .planning/)
Werkzeug-Übersicht:   .deepwork/tool-inventory.md
─────────────────────────────
WAS JETZT?

→ /clear eingeben (leert den Kontext für einen sauberen Start)
→ dann: /deepwork-01-discovery

Wenn du die Setup-Details nochmal nachschlagen möchtest:
  .deepwork/tool-inventory.md  ← welche Tools verfügbar sind
  .deepwork/planning/PROJECT.md  ← Projekt-Definition

Wenn du später wiederkommst (nach einer Pause):
  Das Projekt-Setup ist in .deepwork/ gespeichert.
  Tippe /deepwork-entry-analyze um den Stand zu analysieren,
  oder direkt /deepwork-01-discovery um mit der Discovery zu starten.
─────────────────────────────
```
