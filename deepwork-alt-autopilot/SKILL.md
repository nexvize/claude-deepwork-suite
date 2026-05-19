---
name: deepwork-alt-autopilot
description: "**When: CAN — Alternative to deepwork-03-execute when you want fully autonomous multi-section execution without /clear sync points.** End-to-end autopilot for the complete deepwork suite. Runs bootstrap → discovery → refine → execute autonomously in one continuous session, pausing ONLY for: the initial mega-interview, NO-GO verdicts, killer risks, cost cap, outside-contract decisions, or repeated verification failures. Everything that would normally require user input is resolved upfront via the mega-interview and written into an AUTOPILOT-CONTRACT.md. No /clear between sections — the autopilot maintains context across sections via handoff.md + memory. Use when: 'autopilot', 'mach alles', 'run it all', 'ohne mich', 'von vorne bis hinten', 'ohne input von mir', '/deepwork-alt-autopilot'. This is the hands-off mode — deepwork-00 through 03 but fully automated with a single upfront setup session. Typ-bewusst: wählt automatisch die richtigen Protokolle und Swarm-Strategien basierend auf dem Projekttyp (coding, design, content, media, marketing, analysis, concept, education, automation, legal, finance, research)"
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

# deepwork-alt-autopilot: Vollautomatischer Modus

**Alternative zu deepwork-03-execute — für wenn du nicht Schritt für Schritt dabei sein willst.** Führt die gesamte deepwork-Pipeline (00→01→02→03) autonom durch. Einzige Momente die deine Aufmerksamkeit brauchen: das Mega-Interview am Anfang, und die 8 immer-aktiven Pause-Trigger (NO-GO, Killer-Risiko, Cost-Cap etc.).

**Read first:**
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/native-protocols.md` — alle nativen Protokolle (Verification, Debug, Code Review, etc.)
- `references/tool-awareness.md`
- `references/memory-persistence.md`
- `references/token-log-protocol.md`
- `references/handoff-protocol.md`
- `references/documentation-standard.md`
- `references/contract-template.md` — the contract schema
- `references/routing.md` — section tool routing
- `references/model-selection.md` — Sonnet vs Opus decisions
- `references/research-substeps.md` — tellerrand research guide
- `references/verdict-rubric.md` — GO/GO-WITH-CUTS/NO-GO criteria
- `references/interview-rounds.md` — question bank for mega-interview
- `references/self-reflection.md` — autonomous controlling between sections
- `references/research-verification.md` — source verification in research phase
- `references/user-profile.md` — non-technical user in mega-interview
- `references/decision-levels.md` — 5-Stufen-Empfehlung für alle User-Entscheidungen
- `references/project-profiles.md` — Projekttyp-Profile (Protokolle, MCPs, Verification-Kriterien, Swarm-Sizing)

## Projekttyp-Präambel ⚐

Am Start jeder Session:

1. `PROJECT.md` lesen (`.deepwork/planning/PROJECT.md`)
2. `project_type` auslesen (coding | research | content | design | media | marketing | analysis | concept | education | automation | legal | finance)
3. Falls nicht vorhanden: kurz fragen welcher Typ
4. `references/project-profiles.md` — Profil für diesen Typ laden
5. Profil-Einstellungen übernehmen: bevorzugte Protokolle, MCPs, Verification-Kriterien, Swarm-Sizing

---

## Step 0 — Initial Mega-Interview ⚐

**This is the only guaranteed interview moment.** The goal: surface everything that would normally require user input during phases 01–03, so it can run without stopping.

Read `references/contract-template.md` to understand what needs to be filled.

**Interview structure** (use `AskUserQuestion`, as many rounds as needed — this is the one time to ask everything):

**Round A — Project Essence (matches 01-discovery)**
- What, for whom, binary success criterion, scope, constraints, Don'ts
- (If a handoff.md already exists: read it and skip answered questions)

**User Profile ⚐** (see `references/user-profile.md`): Conduct the mega-interview with the assumption that the user is non-technical. Explain all concepts before asking about them. Run the Non-Technical User Checklist before finalizing the contract. Watch for knowledge-gap-based assumption errors — flag them explicitly in the contract.

**Round B — Anticipatory Decisions (matches 02-refine)**
- For each likely implementation choice: what's the default preference?
- Tech stack preferences, architectural biases, quality vs speed tradeoffs
- What to do with scope creep discoveries?

**Round C — Risk and Assumption Fallbacks (matches 01-discovery)**
- For each major assumption: what if it's false?
- For each significant risk: continue, mitigate, or pause?

**Round D — Caps and Tool Policy**
- Cost cap (USD or tokens), time cap, sections per run
- Tool preferences and prohibitions
- What requires approval before doing?

**Round E — Escalation Rules**
- Beyond the 8 default always-pause triggers (see contract-template.md ## Always-Pause Triggers), what else must pause?
- Push notifications desired?

**Round G — Projekttyp & Profil**
- Welcher Typ? (12 Optionen aus `references/project-profiles.md`: coding | research | content | design | media | marketing | analysis | concept | education | automation | legal | finance)
- Zweit-Typ falls Mischprojekt?
- Auto-Discovery erlaubt? (Soll Suite neue Tools empfehlen wenn sie Lücken findet?)
→ Schreibe in AUTOPILOT-CONTRACT.md:
  ```yaml
  project_type: <typ>
  project_type_secondary: <typ2 | none>
  auto_discovery_enabled: <true|false>
  ```

**Round F — Autopilot Auto-Permissions**
Explain each permission in plain language before asking. Default for all is `true` (autopilot is the hands-off mode — these defaults exist so it can actually run without stopping). User can set any to `false` to get a pause for that specific action.

Ask in one `AskUserQuestion` batch (multi-select: keep as true / set to false):
- **Automatische Projekt-Umstrukturierung** (`allow_auto_migration`): Wenn dein Projekt eine veraltete Ordnerstruktur hat, soll ich sie automatisch aktualisieren ohne zu fragen?
- **Wissens-Ordner automatisch anlegen** (`allow_auto_vault_bootstrap`): Soll ich den Obsidian-Ordner anlegen ohne nachzufragen, falls er noch nicht existiert?
- **Fehlende Hilfsprogramme automatisch installieren** (`allow_auto_mcp_install`): Wenn ein benötigtes Hilfsprogramm fehlt (z.B. für Web-Recherche), soll ich es automatisch einrichten?
- **Automatische Einstellungen** (`allow_auto_hooks_setup`): Soll ich die empfohlenen Verhaltensregeln (Hooks) automatisch aktivieren?
- **Viele parallele Helfer starten** (`allow_large_swarms`): Soll ich bei großen Aufgaben viele Helfer gleichzeitig starten können (z.B. 50–200 für einen Mega-Prototyp), ohne vorher zu fragen?
- **Parallele Abschnitte bevorzugen** (`prefer_parallel_sections`): Sollen unabhängige Arbeitsschritte automatisch gleichzeitig erledigt werden?
- **Technik-Vorankündigungen ins Protokoll** (`skip_pre_permission_blocks`): Sollen die technischen Vorankündigungen nur ins Projektprotokoll geschrieben werden statt in den Chat?

**Research depth setting** — zeige dem User die 5-Stufen-Auswahl (aus `references/decision-levels.md`, Kategorie B):

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RECHERCHE-TIEFE — wie gründlich soll ich recherchieren?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Überblick: Nur offensichtliche Quellen, 1–2 Agents — sehr schnell, minimale Kosten
2. Basis: Bekannte Alternativen prüfen, 3–5 Agents — schnell, niedrige Kosten
⭐ 3. Standard (empfohlen): Vollständige Tellerrand-Recherche, 6–10 Agents — moderat, gute Abdeckung
4. Tiefgehend: Contrary research intensiv, alle Optionen durchleuchtet, 10–20 Agents — höhere Kosten, maximale Abdeckung
5. Exhaustiv: Alles + Expert-Level Quellen, keine Abkürzungen, 20+ Agents — maximale Kosten, vollständiges Bild

Mein Tipp für diese Situation: Option <N> — <konkreter Grund warum>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Schreibe die gewählte Stufe (1–5) ins AUTOPILOT-CONTRACT.md als `research_depth`.

**Contract template fields (add to AUTOPILOT-CONTRACT.md):**
```yaml
project_type: <typ>
project_type_secondary: <typ2 | none>
auto_discovery_enabled: true
```

**Protokoll-Stack:** wird aus `references/project-profiles.md` für den gewählten Typ geladen — nicht hardcoded.

Output: `.deepwork/AUTOPILOT-CONTRACT.md` (using template from `references/contract-template.md`)

---

## Step 1 — Contract Hardening ⚐

Run in parallel to catch gaps:

**Stress-test:** If `kreuzverhoer` skill available → invoke it on the contract. Otherwise: walk through each section of the contract and ask "what situation would cause this to fail? Is that covered?"

**Gap-finder:** Spawn 1 `Plan`-type Agent: "Given this autopilot contract [paste key sections], what unexpected decisions might arise during a typical project of this type that the contract doesn't cover? List gaps with suggested defaults."

For each gap → run a targeted mini re-interview (Round F: just the gaps, not everything again).

---

## Step 2 — Loop Setup ⚐

**Tier 1 (preferred): Ruflo Autopilot**
```
Skill tool → ruflo-autopilot:autopilot-loop
mcp__ruflo__autopilot_enable with contract config
```
Configure with: cost cap, escalation triggers, section iteration, reporting frequency.

**Tier 2: Ruflo Loop Worker**
```
Skill tool → ruflo-loop-workers:loop-worker
```
Set up a loop that iterates through phases 01→02→03 sequentially.

**Tier 3: Inline loop with ScheduleWakeup**
If no Ruflo: use `ScheduleWakeup` between phases to manage context, with handoff.md as the state carrier. Each wake re-reads the handoff and continues.

**In all cases:** hard-wire escalation triggers and cost caps into the loop configuration.

---

## Step 3 — Phase 00: Bootstrap (autonomous) ⚐

Execute the deepwork-00 bootstrap logic internally (no user input needed if contract covers it):

- Tool inventory → `.deepwork/tool-inventory.md`
- Routing decision: contract says "project is clear" → skip brainstorming, go direct
- Foundation docs: PROJECT.md, REQUIREMENTS.md, ROADMAP.md, STATE.md nativ schreiben (→ `.deepwork/planning/`)
- If routing says "idea too vague" (shouldn't happen after mega-interview, but possible) → **PAUSE + PushNotification**

Persist: journal + memory + cost-log entry.

---

## Step 4 — Phase 01: Discovery (autonomous) ⚐

Execute the discovery logic without the user interview (contract already answered those questions):

**Interview: SKIP** — contract provides all project essence answers. Use them to seed the research.

**Research:** Run the full 4-step tellerrand research (see `references/research-substeps.md`) at the depth configured in the contract. All research via parallel Swarm agents.

**Re-interview:** Only if research uncovers a Killer-risk or directly falsifies a core assumption. Apply contract fallback first — if no fallback covers it → **PAUSE + PushNotification**.

**Research Verification ⚐** (see `references/research-verification.md`): In autonomous mode, verification is even more critical — there's no user interaction to catch errors. All key findings used in plan decisions must have ≥2 independent sources. Mark unverified findings explicitly in SUMMARY.md.

**Plan draft:** Write `.deepwork/PLAN.md` with contract preferences as guide.

**Hardening:** Run kreuzverhoer + counter-proposal Agent in parallel.

**Verdict:** 
- GO → continue
- GO-WITH-CUTS → apply scope cuts per contract `## Cut if needed` list → continue
- **NO-GO → ALWAYS PAUSE** — this is a hard stop. User decides.

**Persist** all of this: journal, memory, cost-log.

---

## Step 5 — Phase 02: Refine (autonomous) ⚐

Execute the refine logic using contract defaults for all decisions:

**Clarifying interview:** SKIP if handoff is complete. Run only if a section has no viable implementation approach in context.

**Section discussion:** For each section, determine implementation approach using contract's tool policy and decision defaults. If genuinely ambiguous and no contract default applies → **PAUSE + PushNotification**.

**Re-research:** If a specific technical question arises → spawn focused agent, don't pause.

**Plan update:** Apply any refinements. Document in decisions.md.

**Update handoff.md** with all section specs.

---

## Step 6 — Phase 03: Execute (Loop, NO /clear between sections) ⚐

Unlike deepwork-03-execute (which clears between sections), the autopilot runs sections back-to-back in a continuous loop.

For each `ready-to-execute` section:

**A. Knowledge synthesis:** `mcp__ruflo__memory_search` for `kind:decision` + `kind:learning` → brief-an-mich-selbst for this section.

**B. Tool routing ⚐:** Read `references/routing.md` + apply contract tool policy.

**C. Execute:** Spawn appropriate swarm/agent/skill. Capture `total_tokens` and `duration_ms` from each notification.

**D. Verify (BLOCKING):** Binary criterion check. On failure:
- Attempt 1: diagnose + fix
- Attempt 2: alternative approach
- Attempt 3: alternative approach
- Failure 3: **PAUSE + PushNotification**

**E. Document:** Raw output → `outputs/`, synthesis → journal, memory sync.

**F-autonomous. Self-reflection check ⚐** (see `references/self-reflection.md`):
After each section completes, before moving to the next:
- Controlling Triangle: Goal ← Plan ← Execution — still aligned?
- Did this section produce unexpected results that affect remaining sections?
- Should any remaining section be revised given what was just learned?
- Have errors crept into the work that need correction before proceeding?

If course correction is needed in autonomous mode:
- Small adjustment → apply and continue (log in decisions.md)
- Plan change → update PLAN.md and handoff.md, continue
- Major insight that invalidates approach → **PAUSE + PushNotification** (this is a new pause trigger)

**F. Token log:** Section entry in cost-log.md.

**G. Cost cap check:** If at 80% of cap → warn via PushNotification. At 100% → **PAUSE**.

**H. Update handoff.md:** Section done, outcome filled.

**I. Continue to next section.** No /clear. No user confirmation needed (it's in the contract).

---

## Pause Rulebook

**ALWAYS PAUSE (send PushNotification, wait for user):**
1. Bootstrap routing says "idea too vague"
2. Realismus verdikt = NO-GO
3. Killer-risk materializes during execution
4. Cost cap 100% reached
5. Outside-contract decision required (no default available)
6. Verification fails 3 consecutive times on same section
7. Core assumption massively falsified with impact on multiple remaining sections
8. Any user-defined escalation from contract
9. Self-reflection check reveals major course correction needed (invalidates 2+ remaining sections)

**NEVER pause for:**
- Research findings within configured depth
- Plan pivots when contract default applies
- Assumption confirmations
- Low/Mid risk mitigations
- Section completion

---

## Step 7 — Final Report

When all sections are done, or the loop is stopped (cap / pause / user abort):

Write `.deepwork/AUTOPILOT-REPORT.md`:

```markdown
# Autopilot Report: <Project Name>
Run date: <date>
Stop reason: <all-complete | cost-cap | time-cap | user-abort | pause-trigger>

## Sections Completed
| Section | Status | Verification | Notes |
|---------|--------|-------------|-------|

## Sections Remaining
| Section | Status | Why not completed |
|---------|--------|------------------|

## All Decisions Made
<Link to decisions.md — every choice during the run>

## Token Summary
| Phase | Input | Output | Cache | Est. Cost |
|-------|-------|--------|-------|-----------|
| (from cost-summary.md) |

## Assumptions Reality Check
<Which assumptions held, which were falsified, impact>

## Learnings
<Key things discovered that weren't in the plan>

## Recommended Follow-ups
- /gsd-code-review (if code was written)
- /security-review
- /gsd-ui-review (if UI was built)
- /gsd-docs-update

## Contract Adherence
<Did the contract cover everything? What gaps appeared? Suggestions for next autopilot run.>
```

**Post-report actions:**

**Obsidian sync:** If vault configured, sync all key documents (handoff.md, PLAN.md, VERDICT.md, AUTOPILOT-REPORT.md, decisions.md, knowledge base) to vault. See `references/tool-awareness.md`.

**Missing tools log:** If any tools were flagged as missing during the run, produce a summary at the end of the report:
```
## Missing Tools (flagged during this run)
| Tool | When needed | Impact | How to install |
|------|------------|--------|----------------|
| <name> | <phase/section> | <what was lost> | <install path> |
```

**Final token log:** Update cost-summary.md with full aggregate.

**Final memory sync:** All Ruflo memory + journal flushed.

**Output:**
```
═══════════════════════════════════════════
AUTOPILOT DURCHGELAUFEN
═══════════════════════════════════════════
Beendet wegen: <Grund>
Abschnitte erledigt: <N>/<Gesamt>
Verbrauchte Token: ~<N> | Geschätzte Kosten: ~$<X.XX>
Bericht (AUTOPILOT-REPORT.md): .deepwork/AUTOPILOT-REPORT.md ✓
═══════════════════════════════════════════
```
