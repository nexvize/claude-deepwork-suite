---
name: deepwork-00-bootstrap
description: "**When: MUST — Run first for every new project. Sets up project structure, project type, tools, and foundation.** Entry point for ALL new projects — coding, research, content writing, design, media, marketing, analysis, concept/strategy, education, automation, legal, finance. Detects project type, creates adaptive folder structure, and offers Co-Planning or Autopilot mode. Use ALWAYS when: starting any new project, 'I have an idea', 'let's build X', 'neues Projekt', 'let's start', '/deepwork', '/deepwork-00'. Even for rough, half-formed ideas — this skill decides what to do."
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
  - Task
  - AskUserQuestion
  - Skill
---

**Lies zuerst:**
- `references/plain-language.md` — Klartext-Pflicht (Status-Updates, Pre-Permission-Blocks, Pause-Blöcke)
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/project-profiles.md` — Projekttypen + adaptive Ordnerstruktur
- `references/tool-awareness.md` — Tool-Routing bei jedem ⚐
- `references/user-profile.md` — default assumption: non-technical user

# deepwork-00: Bootstrap

**Part 1 of the deepwork suite.** Bringt das Projekt zum Standing Start — mit der richtigen Struktur für den richtigen Projekttyp, damit deepwork-01 echte Discovery-Arbeit machen kann.

---

## Step 0 — Existing Project Check + Tool Inventory ⚐

**First: Check if this project already has deepwork structure.**

Does `./handoff.md` or `./.deepwork/planning/PROJECT.md` exist?

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

**YES, but `.deepwork/` directory is empty or missing foundation docs:** Continue bootstrap but skip steps already done.

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
- Design (Figma MCP): <yes/no>
- Media generation (higgsfield): <yes/no>
```

---

## Step 1 — Quick Triage ⚐

Ask via `AskUserQuestion` — alle Rounds in einem Aufruf, dann auswerten:

**User Profile Check ⚐** (read `references/user-profile.md` before interviewing):
- Assume the user is non-technical. Adjust all questions accordingly.
- Watch for knowledge gaps — note in `.deepwork/decisions.md` as `kind:user-profile`.

**Round 1:** What stage is this?
- Rough idea / vague inspiration
- Concrete concept with some clarity
- Defined project with clear goals

**Round 2:** What exists already?
- Any prior research, docs, or code?
- Any constraints already decided?

**Round 1.5 — Projekttyp:** Welcher Typ ist dieses Projekt?

```
(1)  Coding / Software      — Code schreiben, debuggen, deployen
(2)  Recherche              — Themen erforschen, Wissen zusammenführen
(3)  Inhalte / Texte        — Artikel, Bücher, Skripte, Dokumentation
(4)  Design / UX            — Wireframes, UI, DesignSystem, Figma
(5)  Media                  — Bilder, Videos, kreative Assets
(6)  Marketing              — Kampagnen, Copy, Strategie, Ads
(7)  Analyse / Daten        — Reports, Dashboards, Datenauswertung
(8)  Konzept / Strategie    — Ideen, Roadmaps, Pitches, Frameworks
(9)  Education              — Kurse, Tutorials, Lernmaterial
(10) Automation             — Workflows, Scripts, Integrationen
(11) Legal                  — Verträge, Compliance, Legal Research
(12) Finance                — Finanzmodelle, Prognosen, Reports

Falls mehrere zutreffen: Haupt-Typ wählen + optionalen Zweit-Typ nennen.
```

Lade nach Antwort das passende Profil aus `references/project-profiles.md`.
Schreibe `project_type: <typ>` (und ggf. `project_type_secondary: <typ2>`) in `PROJECT.md` (Step 3.5).

**Round 3 — Arbeitsmodus:** Wie soll gearbeitet werden?

```
(a) Standard-Pipeline     → Discovery → Refine → Execute (klassisch)
(b) Co-Planning           → wir bauen den Plan gemeinsam Schritt für Schritt
(c) Autopilot             → /deepwork-alt-autopilot — vollautomatisch
(d) Nur Struktur anlegen  → dann selbst entscheiden
```

**Round 4:** Was muss heute passieren?
- Explore and brainstorm first?
- Dive into discovery (research + planning)?
- Start building immediately?

---

## Step 2 — Routing Decision ⚐

Based on triage answers, choose the path:

| Situation | Action |
|-----------|--------|
| Modus (c) Autopilot gewählt | Handoff zu /deepwork-alt-autopilot — Projekttyp mitgeben |
| Modus (b) Co-Planning gewählt | Co-Planning-Modus starten (siehe unten) |
| Idea very vague | Native Brainstorm Protocol (→ `references/native-protocols.md`), dann Step 3 |
| Clear enough | Continue to Step 3 |
| Already have research/docs | Document Ingest Protocol (→ `references/native-protocols.md`), dann Step 3 |
| Specific technical question | Spike Protocol (→ `references/native-protocols.md`), dann Step 3 |
| Plan already exists | Handoff to deepwork-03 directly |

Document routing decision in `.deepwork/decisions.md`.

### Co-Planning-Modus (Modus b)

Wenn Co-Planning gewählt:
1. Nach Step 3 + 3.5: PLAN.md Sektion für Sektion gemeinsam entwickeln
2. Pro Sektion: "Hier ist mein Vorschlag für Sektion X — dein Feedback?"
3. User korrigiert/ergänzt/bestätigt → Section wird festgeschrieben
4. Weiter mit nächster Sektion — bis Plan komplett
5. Danach: direkt in deepwork-03 oder Pause

---

## Step 3 — Adaptive Projektstruktur anlegen ⚐

Lege die Ordnerstruktur basierend auf dem Projekttyp an. Lies das Profil aus `references/project-profiles.md` für den gewählten Typ.

In Klartext erklären (Projekttyp nennen):
> "Ich lege jetzt die Ordnerstruktur für dein [Typ]-Projekt an — angepasst an diese Art von Arbeit."

**Basis-Struktur (immer):**
```
.deepwork/
├── planning/      ← Projektdefinition
├── research/      ← Wird von deepwork-01 befüllt
├── outputs/       ← Wird von deepwork-03 befüllt
├── journal/       ← Fortschrittsnotizen
├── decisions.md
├── cost-log.md
├── cost-summary.md
└── tool-inventory.md  (aus Step 0)
```

**Typ-spezifische Erweiterungen (aus project-profiles.md):**

| Typ | Zusätzliche Ordner |
|---|---|
| coding | `src/` (stub), `tests/` (stub), `docs/` (stub) |
| research | `sources/`, `synthesis/`, `reports/` |
| content | `drafts/`, `published/`, `assets/` |
| design | `wireframes/`, `specs/`, `assets/`, `components/` |
| media | `prompts/`, `assets/`, `exports/`, `storyboards/` |
| marketing | `copy/`, `campaigns/`, `assets/`, `briefs/` |
| analysis | `data/`, `reports/`, `insights/`, `models/` |
| concept | `ideas/`, `roadmaps/`, `pitches/`, `stakeholders/` |
| education | `modules/`, `exercises/`, `assessments/`, `resources/` |
| automation | `scripts/`, `configs/`, `tests/`, `workflows/` |
| legal | `contracts/`, `research/`, `compliance/` |
| finance | `models/`, `data/`, `reports/`, `forecasts/` |

Bei Mischtypen: Basis + Haupt-Typ + top-3 Ordner des Zweit-Typs.

**Wachstum über das Projekt-Leben (wird NICHT jetzt angelegt):**
- `handoff.md` + `PLAN.md` + `VERDICT.md` → nach deepwork-01
- `outputs/<section-id>/` → nach jeder deepwork-03-Sektion
- `PROJECT-COMPLETE.md`, `NEXT-STEPS.md` → nach deepwork-end-report

**Obsidian-Sync vorbereiten** (wenn Vault aus `DEEPWORK-CONFIG.md` existiert):
`<DEEPWORK_VAULT_PATH>\Projects\<project-slug>\` anlegen — leer, bereit für Sync.

---

## Step 3.5 — Foundation Documents ⚐

Die folgenden Dateien sind Pflicht — deepwork-01 liest sie.

Schreibe unter `.deepwork/planning/` (nativ, kein externer Skill nötig):

**`PROJECT.md`** — Projektname, Domain, Kernproblem, Zielgruppe, Haupt-Ziel, Constraints.
**Pflichtfeld:** `project_type: <typ>` (und ggf. `project_type_secondary: <typ2>`)

```yaml
# .deepwork/planning/PROJECT.md
name: <Projektname>
project_type: <coding|research|content|design|media|marketing|analysis|concept|education|automation|legal|finance>
project_type_secondary: <typ2 | none>
domain: <Bereich>
core_problem: <Was soll gelöst werden>
target_user: <Für wen>
primary_goal: <Messbares Ziel>
key_constraints: <Bekannte Einschränkungen>
work_mode: <standard|co-planning|autopilot>
```

**`REQUIREMENTS.md`** — Must-haves vs. Nice-to-haves vs. Explizit außerhalb.

**`ROADMAP.md`** — Grobe Phasen (kein Detail — deepwork-01 füllt aus).

**`STATE.md`** — Aktueller Stand: Phase, Was erledigt, Was offen.

---

## Step 4 — Token Log + Memory Init ⚐

Initialize `.deepwork/cost-log.md` und `.deepwork/decisions.md` (leer mit Headers).

Log bootstrap token cost (see `references/token-log-protocol.md`).

Falls Ruflo Memory verfügbar: Bootstrap-Memory-Eintrag speichern mit Tags `projekt:<slug>`, `phase:00`, `typ:<project_type>`.

---

## Step 5 — Handoff

```
Bootstrap abgeschlossen.
─────────────────────────────────────────────────
Projekttyp:     <typ> (→ Profil geladen: references/project-profiles.md)
Arbeitsmodus:   <standard | co-planning | autopilot>
Struktur:       .deepwork/ + <typ-spezifische Ordner>
Grundlagen:     .deepwork/planning/PROJECT.md
─────────────────────────────────────────────────
WAS JETZT?

Standard / Co-Planning:
→ /clear eingeben (leert Kontext für sauberen Start)
→ dann: /deepwork-01-discovery

Autopilot:
→ /deepwork-alt-autopilot (Projekttyp wird übergeben)

Wenn du die Setup-Details nachschlagen willst:
  .deepwork/tool-inventory.md    ← welche Tools verfügbar
  .deepwork/planning/PROJECT.md  ← Projekt-Definition + Typ

Wenn du später wiederkommst:
  /deepwork-entry-analyze — analysiert den aktuellen Stand
─────────────────────────────────────────────────
```
