---
name: deepwork-03-execute
description: "**When: MUST — Run after deepwork-02-refine, once per section (use /clear between sections). Alternative: deepwork-alt-autopilot for autonomous multi-section run.** Executes ONE section of the project plan per invocation. Reads handoff.md, picks the next pending section, builds a mini execution plan, delegates to the right swarm/agent/skill (not inline by default), verifies the result against a binary criterion, documents everything, logs tokens, and signals a mandatory /clear before the next section. This strict one-section-per-clear discipline is the sync point — after clear, you know exactly what was done and what's next. Use after deepwork-02-refine, or when handoff.md has sections marked 'ready-to-execute'. Triggers: 'execute', 'umsetzen', 'build', 'los geht's', 'nächste section', '/deepwork-03'. For autonomous multi-section execution without /clear between sections → use deepwork-alt-autopilot instead."
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

**Part 4 of the deepwork suite.** One section per invocation. Quality over speed. Swarm/agent by default, not inline.

**Read first:**
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/native-protocols.md` — Verification, Debug, TDD, Code Review Protokolle (WICHTIG)
- `references/tool-awareness.md`
- `references/routing.md`
- `references/memory-persistence.md`
- `references/token-log-protocol.md`
- `references/documentation-standard.md`
- `references/handoff-protocol.md`
- `references/model-selection.md` — model selection guidance
- `references/self-reflection.md` — controlling at every ⚐
- `references/user-profile.md` — non-technical user assumption
- `references/decision-levels.md` — 5-Stufen-Empfehlung für alle User-Entscheidungen

---

## Step 0 — Load Context ⚐

**Read handoff.md.** If missing → tell user to run deepwork-01 and deepwork-02 first, stop.

**Brief-an-mich-selbst:** Read `.deepwork/decisions.md` + Ruflo memory search (`kind:decision`, `kind:learning` for this project). Write a 2–4 sentence anchor: what we're building, where we are, key constraints, watch-out risks.

**Verify preconditions:**
- handoff.md verdict is GO or GO-WITH-CUTS
- At least one section is `ready-to-execute`
- No section is `in-progress` (if one is, either resume it or mark it appropriately)

**Resume check:** Is any section marked `in-progress`?
- YES → It was interrupted. Ask via `AskUserQuestion`:
  - "Section `<name>` was in-progress when last session ended. Do you want to: (a) Resume it — check what was done and continue, (b) Restart it fresh, or (c) Mark as abandoned and start the next section?"
  - On Resume: read `.deepwork/outputs/<section-id>/` for any agent outputs that completed before interruption.
  - On Restart: reset status to `ready-to-execute`, clear any partial outputs.
  - On Abandon: mark as `abandoned` in handoff.md, note reason in decisions.md.

---

## Step 1 — Select Section ⚐

Pick the first section with status `ready-to-execute`. If multiple → ask user to confirm which one via `AskUserQuestion`.

**Parallel mode check:** Are there 2+ sections with `ready-to-execute` status AND no dependencies between them?
- If YES → Ask user: "Sections [A] and [B] (and [C]) are independent and could run in parallel via Swarm, saving time. Run them in parallel, or one at a time?"
- On parallel: use `ruflo-swarm:swarm` with worktree isolation, one worker per section. Each worker gets the section spec from handoff.md. Collect all outputs. Verify each section independently (Step 4). Update handoff.md for all completed sections.
- On sequential: proceed with first section as normal.

Update handoff.md: set selected section status to `in-progress`.

---

## Step 2 — Section Mini-Plan ⚐

Before any execution, write a mini-plan for this section:

```markdown
## Executing: Section <N> — <Name>
**Goal:** <from handoff>
**Verification criterion:** <binary check from handoff>
**Chosen tool/approach:** <from routing.md analysis>
**Why this tool:** <1 sentence>
**Steps:**
1. <step>
2. <step>
**Risks for this section:** <any that are section-specific>
**Estimated order:** <what happens first, second, etc.>
```

**Tool routing ⚐:** Read `references/routing.md`. Decide which tool/agent/swarm is right for this section. Don't default to inline — only choose inline when the section is genuinely trivial (1–2 file edits).

**Self-reflection check ⚐** (before starting execution):
- Is this the right section to execute right now? (correct dependencies?)
- Is the verification criterion still correct, or did something change in previous sections?
- Does anything from recently completed sections change how this section should be approached?
- Is the chosen tool still the right tool, or has new information changed the routing decision?

**Simplicity check:** Is there a simpler approach than what's planned? (Non-technical user principle: prefer the simpler solution if it meets the success criterion.)

**Vertical Slice Check:** Deckt diese Section ein vollständiges Feature über alle relevanten Schichten ab (UI + Logik + Daten)? Falls sie nur eine horizontale Schicht implementiert (z.B. nur Frontend ohne Datenbankanbindung) → prüfen ob das beabsichtigt ist. Vertical Slices ermöglichen frühes echtes Testen und konkretes Feedback — horizontal implementierte Schichten können erst am Ende getestet werden.

Document the decision in `.deepwork/decisions.md`.

---

## Step 3 — Execute via Swarm/Agent ⚐

**Default:** delegate, don't do it yourself inline.

### Swarm path (write-heavy, parallel, oder riskant)
Use `Skill` tool → `ruflo-swarm:swarm` mit worktree isolation. Provide the section goal, constraints, and verification criterion in the swarm spec.

### Specialist Agent path (fokussierte, abgeschlossene Aufgabe)
Spawn via `Agent` tool — **subagent_type immer explizit angeben:**

| Section-Typ | subagent_type |
|---|---|
| Codebase-Exploration | `Explore` |
| Architektur-Entscheidung | `Plan` |
| Code-Entwicklung | `general-purpose` |
| Code-Review | `feature-dev:code-reviewer` |
| Debugging | `gsd-debugger` |
| Allgemeine Aufgaben | `general-purpose` |

Provide full context: project goal, section spec, verification criterion, relevant file paths.

### Native path (direkter Protokoll-Aufruf)
Für TDD → `references/native-protocols.md` → TDD Protocol (direkt anwenden, kein externer Skill nötig)  
Für Security-Fragen → `security-review` Skill (optional, wenn verfügbar)  
Für Frontend/UI → `frontend-design` oder `ui-ux-pro-max` Skill (optional, wenn verfügbar)

### Inline path (trivial only)
Direct Read/Edit/Write/Bash calls — only when the section genuinely fits in 1–2 tool calls.

**Capture agent outputs:** As task notifications arrive (containing `total_tokens`, `duration_ms`), record them immediately in `.deepwork/journal/`. Don't batch — capture at notification time.

---

## Step 4 — Verification (BLOCKING) ⚐

Verification is not optional. It is blocking — don't proceed to Step 5 without passing it.

**Führe das Verification Protocol aus** (→ `references/native-protocols.md` → Verification Protocol):

1. Binary Criterion aus `handoff.md` lesen
2. Passenden Check ausführen (Tests, Endpoint, Artefakt, Browser, manuell)
3. Bei Failure → Debug Protocol (→ `references/native-protocols.md` → Debug Protocol)
4. Nach 3 fehlgeschlagenen Zyklen → User-Block (Format in native-protocols.md)
5. Pass: Nur weiter wenn Criterion nachweislich erfüllt ist

**4. Pass:** Only proceed to Step 5 once the binary criterion is met.

**Insight-integration check ⚐:** During execution or verification, did anything emerge that changes the plan for remaining sections? If yes → apply `references/self-reflection.md` "Insight check" before proceeding to Step 5. Document in `decisions.md`.

**Manual verification steps:** If the verification involves something that can only be done by a human (e.g., "does this UI look correct?", "does this email send correctly?"), pause and give detailed instructions:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DEINE PRÜFUNG ERFORDERLICH
Ich kann das nicht selbst prüfen — das musst du kurz ansehen.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Was du prüfen sollst:
<genaue Beschreibung, worauf du achten sollst>

Wie du dahin kommst:
<URL, Befehl oder konkrete Schritte>

Was du sehen solltest (wenn alles klappt):
<genau beschrieben — was bedeutet "bestanden">

Antworte danach: "Geprüft — [alles gut / Problem: <beschreiben>]"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Step 4.5 — Recap: Was wurde gebaut? ⚐

Nach erfolgreicher Verifikation — bevor dokumentiert wird.

**Durchführen (inline oder per Agent-Instruktion):**
1. "Erkläre in 3–5 Sätzen was gebaut wurde und wie es funktioniert — ohne Fachbegriffe"
2. "Welche Dateien wurden verändert und warum?"
3. "Wie interagiert diese Section mit dem Rest des Systems — was kommt rein, was geht raus?"

**Warum:** Nach mehreren Sections verliert der User schnell den Überblick über was das Tool alles kann und wie es funktioniert. Wenn dieses Gefühl entsteht, ist das ein Signal dass Recap-Phasen gefehlt haben. Die Erklärung geht in das Section-Journal (Step 5) unter `User-facing explanation`.

---

## Step 5 — Document Outputs ⚐

**Refactor vor dem Dokumentieren:** Führe das Refactor Protocol aus (→ `references/native-protocols.md` → Refactor Protocol). KI-Agents tendieren zu unnötig komplexem Code — ein kurzes aktives Aufräumen nach jeder Section verhindert Schuldenberg über die Iterationen.

**Read:** `references/documentation-standard.md`

**Layer 1 — Raw output:**
- Store all agent/swarm outputs in `.deepwork/outputs/<section-id>/`
- Use format: `<agent-type>-<YYYY-MM-DD-HHmm>.md`

**Layer 2 — Synthesis:**
Write section-completion journal entry in `.deepwork/journal/<date>-03-<section-name>.md`:
```markdown
## Section Complete: <Name> — <date>

**Status:** done
**Verification:** <what was checked, result>
**What was produced:** <concrete artifacts — files, endpoints, etc.>

**Key decisions during execution:**
- <decision 1>

**Learnings vs plan:**
- <what was different>

**Impact on remaining sections:**
- <any dependencies affected>

**New risks discovered:**
- <any>

**Raw outputs:** .deepwork/outputs/<section>/

**Self-reflection summary:**
- Did I stay on plan, or drift? <stayed on plan | drift: <what changed>>
- Errors caught during execution: <none | <what was caught and fixed>>
- Impact on remaining sections: <none | <adjust sections X,Y because Z>>
- User-facing explanation of what was built: <plain language — no jargon>
```

**Memory:** Persist via `references/memory-persistence.md` with tags `phase:03`, `section:<id>`, `kind:learning`.

---

## Step 6 — Handoff Update + Token Log + Clear ⚐

**1. Update handoff.md:**
- Section status: `in-progress` → `done`
- Fill `Outcome` column
- Add to `## Learnings` (if anything surprising)
- Add to `## Assumptions Reality Check` if any assumption was tested and the result differs from expectation
- Update `last_updated` timestamp

**2. Token log:** Write section entry in `.deepwork/cost-log.md` (include all agent notification data captured in Step 3).

**3. Update cost-summary.md** Phase 03 aggregate.

**4. Memory sync:** Final flush to Ruflo / MCP memory.

**5. Check remaining sections:** Read handoff.md. Are there more `ready-to-execute` sections?

**Planungsdokumente aktuell halten:** `.deepwork/planning/`-Dateien NICHT löschen — sie sind das persistente Gedächtnis zwischen Sessions. Aber: wenn diese Section etwas geändert hat das in den Planungsdokumenten steht (Anforderung entfallen, Ansatz geändert, Constraint gefunden) → jetzt updaten. Veraltete Planungsdokumente verwirren zukünftige Agent-Sessions genauso wie gar keine.

**Rollback note:** If you need to undo this section's changes:
- If git is initialized: `git revert` the commits from this section (see journal entry for commit hashes)
- Manual: the section journal entry lists all files modified — restore from `.deepwork/outputs/<section-id>/` pre-execution state if saved
- Mark section status back to `ready-to-execute` in handoff.md if reverting

Always document a rollback in `decisions.md` with reason.

**6. Clear-trigger output:**
```
═══════════════════════════════════════════
ABSCHNITT FERTIG: <Name des Abschnitts>
═══════════════════════════════════════════
Geprüft: ✓ (<was genau geprüft wurde>)
Was wurde gebaut: <kurze Beschreibung in normaler Sprache>
Kosten dieses Abschnitts: ~<N> Tokens | Gesamt bisher: ~<N> Tokens
Noch ausstehende Abschnitte: <N>

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BEVOR DU /clear eingibst — kurz prüfen:
  ✓ Schau dir den Output dieses Abschnitts an (falls relevant)
  ✓ handoff.md zeigt den Abschnitt als "done" ✓
  ✓ Wenn etwas nicht stimmt: jetzt ist der richtige Moment zum Korrigieren
    (nach /clear ist der Kontext weg)

SYNC-PUNKT — bitte /clear eingeben
(Das leert den Kontext, damit der nächste Abschnitt sauber startet.)

NACH /clear — genau das eingeben:
  /deepwork-03-execute  → nächsten Abschnitt einzeln ausführen
  /deepwork-alt-autopilot → alle restlichen Abschnitte automatisch durchlaufen

Der Skill liest handoff.md und weiß sofort welcher Abschnitt als nächstes dran ist.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

If all sections are done, instead:
```
═══════════════════════════════════════════
ALLE ABSCHNITTE FERTIG ✓
Das Projekt ist vollständig umgesetzt.
═══════════════════════════════════════════
Gesamtkosten: ~<N> Tokens — Details in .deepwork/cost-summary.md

Was jetzt sinnvoll wäre:
  /deepwork-end-report          → Abschlussbericht + Next Steps erstellen
  /security-review              → Optionaler Sicherheits-Check (wenn verfügbar)
  Code Review Protocol          → aus references/native-protocols.md ausführen
═══════════════════════════════════════════
```
