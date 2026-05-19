---
name: deepwork-03-execute
description: "**When: MUST — Run after deepwork-02-refine, once per section (use /clear between sections). Alternative: deepwork-alt-autopilot for autonomous multi-section run.** Executes ONE section of the project plan per invocation for any project type — coding, research, content, design, media, marketing, analysis, concept, education, automation, legal, finance. Reads handoff.md, picks the next pending section, builds a mini execution plan, delegates to the right swarm/agent/skill, verifies the result against a binary criterion, documents everything, logs tokens, and signals a mandatory /clear before the next section."
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Task
  - AskUserQuestion
  - Skill
---

# deepwork-03: Execute

**Part 4 of the deepwork suite.** One section per invocation. Quality over speed.

**Read first:**
- `DEEPWORK-CONFIG.md`
- `references/native-protocols.md`
- `references/tool-awareness.md`
- `references/routing.md`
- `references/memory-persistence.md`
- `references/token-log-protocol.md`
- `references/documentation-standard.md`
- `references/handoff-protocol.md`
- `references/model-selection.md`
- `references/self-reflection.md`
- `references/user-profile.md`
- `references/decision-levels.md`
- `references/project-profiles.md` — type-specific protocols, MCP routing, verification criteria, swarm sizing

---

## Projekttyp-Präambel ⚐

Führe dies am Start jeder Session aus:

1. `PROJECT.md` lesen
2. `project_type` auslesen
3. Falls nicht vorhanden: kurz fragen
4. `references/project-profiles.md` — Profil laden
5. Einstellungen übernehmen: Protokolle, MCPs, Verification-Kriterien, Swarm-Sizing

---

## Step 0 — Load Context ⚐

**Read handoff.md.** If missing → tell user to run deepwork-01 and deepwork-02 first, stop.

**Brief-an-mich-selbst:** 2–4 sentences: what we're building, where we are, key constraints.

**Verify preconditions:** handoff.md verdict is GO. At least one section `ready-to-execute`.

---

## Step 1 — Select Section ⚐

Pick the first `ready-to-execute` section.

**Parallel mode check:** 2+ independent sections? Ask user: run in parallel (Swarm) or sequential?

Update handoff.md: selected section → `in-progress`.

---

## Step 2 — Section Mini-Plan ⚐

Before execution, write mini-plan. Choose tool via `references/routing.md`.

**Self-reflection check ⚐:** Is this the right section? Is the verification criterion still correct?

---

## Step 3 — Execute via Swarm/Agent ⚐

**Default:** delegate, don't do it yourself inline.

### Swarm path: `ruflo-swarm:swarm` with worktree isolation
### Specialist Agent path: `Agent` tool with explicit `subagent_type`
### Native path: TDD, security-review, frontend-design protocols
### Inline path: only for trivial 1–2 file edits

---

## Step 4 — Verification (BLOCKING) ⚐

**Typ-spezifische Verification:**
Lese die Verification-Kriterien aus `references/project-profiles.md` für den aktiven Typ.

"Fertig" bedeutet je nach Typ:
- coding: Tests grün, Code läuft, kein Lint-Fehler
- content: Text gelesen, Ton stimmt, Fakten geprüft
- design: Figma-File korrekt, Spec vollständig
- research: Quellen verifiziert, Widersprüche aufgelöst
- media: Asset exportiert, Qualität geprüft, Format stimmt
- marketing: Copy reviewed, CTA klar, Zielgruppe passt
- analysis: Zahlen nachvollziehbar, Methodik dokumentiert
- concept: Logik konsistent, Stakeholder-Perspektiven berücksichtigt
- education: Lernziel erreichbar, Verständlichkeit geprüft
- automation: Workflow getestet, Edge-Cases abgedeckt
- legal: Quellen zitiert, Aussagen rechtlich geprüft
- finance: Zahlen geprüft, Annahmen dokumentiert

---

## Step 4.5 — Recap: Was wurde gebaut? ⚐

Nach erfolgreicher Verifikation: 3–5 Sätze was gebaut/erstellt wurde.

**Recap-Sprache nach Projekttyp anpassen** (aus `references/project-profiles.md`).

---

## Step 5 — Document Outputs ⚐

**Refactor vor dem Dokumentieren:** Refactor Protocol aus `references/native-protocols.md`.

Raw output → `.deepwork/outputs/<section-id>/`
Journal entry → `.deepwork/journal/<date>-03-<section-name>.md`
Memory sync via `references/memory-persistence.md`.

---

## Step 6 — Handoff Update + Token Log + Clear ⚐

**1. Update handoff.md:** section → `done`
**2. Token log:** section entry in cost-log.md
**3. Update cost-summary.md**
**4. Memory sync**

**6. Clear-trigger output:**
```
═══════════════════════════════════════════
ABSCHNITT FERTIG: <Name>
═══════════════════════════════════════════
Geprüft: ✓
Was wurde gebaut: <kurze Beschreibung>
Noch ausstehende Abschnitte: <N>

SYNC-PUNKT — bitte /clear eingeben

NACH /clear:
  /deepwork-03-execute  → nächsten Abschnitt
  /deepwork-alt-autopilot → alle restlichen automatisch
═══════════════════════════════════════════
```
