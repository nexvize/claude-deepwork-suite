---
name: deepwork-02-refine
description: "**When: MUST — Run after deepwork-01-discovery. Turns the plan into executable sections with clear criteria.** Bridge between discovery and execution for any project type — coding, research, content, design, media, marketing, analysis, concept, education, automation, legal, finance. Reads handoff.md + memory from deepwork-01, runs a clarifying interview when there are gaps, then does a deep discuss-phase-style walkthrough of how exactly each planned section will be implemented. Updates the plan, then produces an updated handoff.md ready for deepwork-03-execute."
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

# deepwork-02: Refine

**Part 3 of the deepwork suite.** Takes a stichfest discovery output and turns it into an executable plan.

**Read first:**
- `DEEPWORK-CONFIG.md`
- `references/native-protocols.md`
- `references/tool-awareness.md`
- `references/memory-persistence.md`
- `references/token-log-protocol.md`
- `references/handoff-protocol.md`
- `references/routing.md`
- `references/model-selection.md`
- `references/self-reflection.md`
- `references/user-profile.md`
- `references/decision-levels.md`
- `references/project-profiles.md` — type-specific protocols, MCP routing, verification criteria, swarm sizing

---

## Projekttyp-Präambel ⚐

Führe dies am Start jeder Session aus:

1. `PROJECT.md` lesen (falls vorhanden unter `.deepwork/planning/PROJECT.md`)
2. `project_type` Feld auslesen
3. Falls nicht vorhanden: kurz fragen
4. `references/project-profiles.md` lesen — Profil für diesen Typ laden
5. Profil-Einstellungen übernehmen: Protokolle, MCPs, Verification-Kriterien, Swarm-Sizing

---

## Step 0 — Load Context ⚐

**Read handoff.md** (project root). Parse all sections. If missing → tell user to run deepwork-01 first, stop.

**Read memory:** `.deepwork/decisions.md` + `.deepwork/journal/`.

**Brief-an-mich-selbst:** synthesize in 3–4 sentences: what the project is, what deepwork-01 decided, key constraints.

**Self-reflection check ⚐:** Is the plan I'm about to refine still the right plan?

---

## Step 1 — Clarifying Interview (only if needed) ⚐

Check the handoff.md for gaps: Open Questions, vague verification criteria, unverified assumptions, sections too broad to execute.

If gaps exist → focused `AskUserQuestion` rounds.

---

## Step 2 — Section-by-Section Deep Discussion ⚐

For each section in the handoff.md execution plan:

**Vertical Slice Check:** Jede Section muss ein vollständiges Ergebnis liefern, nicht nur eine Zuarbeit.

**Sections nach Projekttyp:**
- coding: Sections = Features / Module / API-Endpoints / Layers
- research: Sections = Themenbereiche / Quellen-Cluster / Synthese-Ebenen
- content: Sections = Kapitel / Artikel / Abschnitte
- design: Sections = Screens / Flows / Component-Gruppen
- media: Sections = Szenen / Asset-Typen / Produktions-Phasen
- marketing: Sections = Kampagnen-Teile / Copy-Formate / Kanäle
- analysis: Sections = Datenbereiche / Fragestellungen / Report-Kapitel
- concept: Sections = Konzept-Bereiche / Stakeholder-Gruppen / Roadmap-Phasen
- education: Sections = Module / Lerneinheiten / Assessment-Blöcke
- automation: Sections = Workflow-Schritte / Integration-Punkte / Test-Szenarien
- legal: Sections = Vertrags-Teile / Compliance-Bereiche / Recherche-Felder
- finance: Sections = Modell-Komponenten / Analyse-Bereiche / Report-Kapitel

For each section:
- Tool routing ⚐ (see `references/tool-awareness.md`)
- Verification criterion (must be binary)
- Section risks
- Non-technical explanation
- Self-reflection check

Update handoff.md `## Sections` table as you go.

---

## Step 3 — Re-Research (if needed) ⚐

If discussion revealed a concrete technical uncertainty → spawn 1–2 parallel agents with focused queries.

---

## Step 4 — Plan Update ⚐

Update `.deepwork/PLAN.md` based on section discussions.

---

## Step 4.5 — Kreuzverhoer: Execution Plan Stress-Test ⚐

**Invoke kreuzverhoer:** Run `Skill` tool → `kreuzverhoer` on the full refined execution plan.

---

## Step 5 — Handoff Update + Token Log + Clear ⚐

**1. Update `./handoff.md`:** all sections `ready-to-execute`
**2. Token log:** Write Phase 02 entry.
**3. Memory persist:** decisions + Ruflo memory.
**4. Update cost-summary.md** Phase 02 aggregate.

**5. Clear-trigger output:**
```
═══════════════════════════════════════════
PLAN-VERFEINERUNG ABGESCHLOSSEN
═══════════════════════════════════════════
Abschnitte bereit zur Umsetzung: <N>
Alle Abschnitte: bereit ✓
Übergabe-Dokument (handoff.md) aktualisiert ✓
Kosten protokolliert ✓

Wie es weitergeht:
  → /clear eingeben
  → dann /deepwork-03-execute
═══════════════════════════════════════════
```
