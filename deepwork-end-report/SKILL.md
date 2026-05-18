---
name: deepwork-end-report
description: "**When: SHOULD — Run after all sections in handoff.md are 'done', or after deepwork-alt-autopilot completes.** Final project report for any completed deepwork project. Reads handoff.md + all .deepwork/ artifacts, produces a comprehensive end-report with: what was built, what was decided, what was learned, what still works / what doesn't, and detailed next-step instructions with enough specifics that someone new could immediately continue. Use after deepwork-03 or deepwork-alt-autopilot complete, or any time a project-phase is done and needs a comprehensive summary. Triggers: 'abschlussbericht', 'final report', 'project done', 'was haben wir gebaut', 'next steps', '/deepwork-end-report', or when all handoff.md sections are 'done'."
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
  - Bash
  - Task
  - Skill
---

# deepwork-end-report: Abschlussbericht

**Läuft nach allen Sections — der Exit-Punkt jedes Projekts.** Erstellt einen vollständigen Bericht der für jemanden nützlich ist, der das Projekt noch nie gesehen hat. Jeder Next Step muss konkret genug sein um sofort ausgeführt zu werden — ohne Rückfragen.

**Read first:**
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/native-protocols.md` — Code Review Protocol + Quality Gate Checklist
- `references/handoff-protocol.md`
- `references/documentation-standard.md`
- `references/model-selection.md`
- `references/self-reflection.md` — final controlling check
- `references/user-profile.md` — non-technical translation of all outputs

---

## Step 0 — Load All Artifacts ⚐

Read in this order:
1. `./handoff.md` — project state, sections, outcomes
2. `.deepwork/decisions.md` — all decisions made
3. `.deepwork/cost-log.md` — what it cost
4. `.deepwork/cost-summary.md` — aggregated cost
5. `.deepwork/journal/` — all journal entries (scan for key learnings)
6. `.deepwork/PLAN.md` — what was planned
7. `.deepwork/VERDICT.md` — the realism verdict
8. `.deepwork/research/SUMMARY.md` — what research found (if exists)
9. `.deepwork/AUTOPILOT-REPORT.md` — if autopilot was used

If handoff.md doesn't exist → tell user: "No deepwork project found here. Run /deepwork-00-bootstrap first."

---

## Step 1 — Project Status Assessment ⚐

Assess the project's actual state:

**Completion check:**
- How many sections are `done` vs `pending` / `in-progress` / `abandoned`?
- Does the final result meet the binary success criterion from handoff.md?

**Quality check (Code Review Protocol):**
If code was written: Execute Code Review Protocol aus `references/native-protocols.md` — kein externer Agent nötig. Read alle veränderten Dateien, prüfe auf Bugs/Security/Performance/Requirements. Output → `.deepwork/outputs/final-code-review.md`.

**Reality check:**
Compare `## Assumptions Reality Check` in handoff.md vs. original assumptions. Which held? Which didn't?

**Final self-reflection ⚐:** Look back at the entire project:
- Were there moments where the work drifted from the goal? What caused them?
- Which decisions were made on insufficient evidence (single sources, unverified assumptions)?
- What would have been done differently with today's knowledge?
Document findings in `PROJECT-COMPLETE.md` under `## What We'd Do Differently`.

---

## Step 2 — Write PROJECT-COMPLETE.md ⚐

Write `.deepwork/PROJECT-COMPLETE.md`:

```markdown
# Project Complete: <Project Name>
Date: <ISO-8601>
Deepwork phases used: <00 / 01 / 02 / 03 / 04>

---

## What Was Built
<3–5 sentences. Concrete: what exists now that didn't before. Link to key files/outputs.>

## Success Criterion Check
Original criterion: <from handoff.md>
Result: <MET / PARTIALLY MET / NOT MET>
Evidence: <what was tested and what it showed>

## What Was Decided (Key Decisions)
<Top 5–8 decisions from decisions.md, with brief reasoning>
| Decision | Why | Impact |
|----------|-----|--------|

## What Was Learned
<Top 5–8 learnings from journal + assumptions reality check>
- <learning 1>: <what changed from plan to reality>
- <learning 2>

## What Didn't Work As Planned
<Honest account of failures, pivots, cuts. Not a post-mortem — a record.>
| Section | Plan | Reality | Reason |
|---------|------|---------|--------|

## Costs
Total tokens: <from cost-summary.md>
Estimated cost: $<X.XX>
Most expensive phase: <phase name> (~$<X>)

## Known Limitations / Technical Debt
<Things that work but aren't ideal, and why they were left that way>
- <item>: <why acceptable now, what would fix it>

## Open Issues (Not Resolved)
<From handoff.md ## Open Issues — what was left unresolved and why>
```

---

## Step 3 — Next Steps Guide ⚐

This is the most important section. Every next step must be specific enough that someone with no context could immediately execute it.

Write `NEXT-STEPS.md` in the project root:

```markdown
# Next Steps: <Project Name>
Generated: <date>

---

## Immediate (Do These First)

For each item: be specific enough that execution doesn't require questions.

### 1. <Next Step Name>
**Why:** <what problem this solves or what value it adds>
**How:**
1. <exact command or sequence of steps>
2. <specific file to edit, what to change>
3. <verification: how to know it worked>
**Effort estimate:** <rough time>
**Prerequisite:** <anything that must be done first, or "none">

### 2. <Next Step Name>
...

---

## Short-Term (Next 2–4 Weeks)

### <Item>
**Why:** <rationale>
**Approach:** <how to tackle it>
**Skill to use:** <deepwork-XX / gsd-XX / other>

---

## Long-Term / If Product Grows

### <Item>
**Trigger:** <when to consider this — "when user count exceeds X" / "if Y happens">
**Approach:** <direction, not full plan>

---

## Maintenance Checklist

What needs regular attention once the project is live:
- [ ] <recurring task>: <how often, how to do it>
- [ ] <monitoring check>: <what to watch for>
- [ ] <dependency update>: <which deps, how to check for updates>

---

## If You Need to Continue Development

To resume work on this project with deepwork:
1. Run `/deepwork-00-bootstrap` — it will detect the existing handoff.md
2. If adding a new feature: run `/deepwork-01-discovery` for the new feature scope
3. If fixing a bug: run `/deepwork-03-execute` and pick the relevant section (or create a new section in handoff.md)
4. If doing a full re-run: `/deepwork-alt-autopilot`

Key files to read first: `./handoff.md`, `./NEXT-STEPS.md`, `.deepwork/decisions.md`

---

## Knowledge Gaps to Address

Things the user should learn or get help with to maintain and grow this project:
| Topic | Why It Matters | Resource to Start With |
|-------|---------------|----------------------|
| <technical topic user wasn't familiar with> | <impact on their project> | <specific resource, not just "google it"> |

---

## Missing Pieces (Not Built)

Items from the original scope that were cut or not completed:
| Item | Why Not Done | Effort to Add | Next Step to Add It |
|------|-------------|---------------|---------------------|
| <from handoff ## Scope / Out> | <cut in GO-WITH-CUTS / time / deprioritized> | <rough estimate> | <specific first action> |
```

---

## Step 3.5 — Kreuzverhoer: Next-Steps Stress-Test ⚐

**Invoke kreuzverhoer:** Run `Skill` tool → `kreuzverhoer` auf `NEXT-STEPS.md`. Für jeden nächsten Schritt hinterfragen:
- Ist der Aufwands-Estimate realistisch — oder systematisch zu optimistisch?
- Ist die Prerequisite-Kette vollständig — fehlt eine versteckte Abhängigkeit?
- Löst dieser Schritt tatsächlich das Problem das er vorgibt zu lösen?
- Ist die Priorisierung richtig — oder gibt es einen anderen Schritt der mehr Impact hat?

Output → Anpassungen in `NEXT-STEPS.md` einarbeiten, Begründungen in `.deepwork/decisions.md` dokumentieren.

---

## Step 4 — Knowledge Base Update ⚐

Update or create `.deepwork/KNOWLEDGE-BASE.md` (format from `references/documentation-standard.md`):
- Aggregate all `kind:learning` journal entries
- Summarize architecture decisions
- List what was tried and abandoned (and why)
- Link to key raw outputs

---

## Step 5 — Quality Gate + Obsidian Sync ⚐

**Quality Gate (Pflicht):** Führe die Quality Gate Checklist "Nach deepwork-end-report" aus `references/native-protocols.md` aus. Alle Punkte müssen abgehakt sein bevor fortgefahren wird.

**Obsidian sync (if vault configured):** Sync these files to vault:
- `PROJECT-COMPLETE.md` → `<vault>/Projects/<slug>/Project-Complete.md`
- `NEXT-STEPS.md` → `<vault>/Projects/<slug>/Next-Steps.md`
- `KNOWLEDGE-BASE.md` → `<vault>/Projects/<slug>/Knowledge-Base.md`

See `references/tool-awareness.md` for vault setup.

---

## Step 6 — Final Memory + Cost Log ⚐

**Memory:** Store a final memory entry in Ruflo: `kind:project-complete`, tagged `projekt:<slug>`, with a 3-sentence summary of what was built, key decisions, and open items.

**Token log:** Final entry in `.deepwork/cost-log.md` for this reporting session.

**Cost summary:** Final update to `cost-summary.md` including this phase.

---

## Step 7 — Output

```
═══════════════════════════════════════════
ABSCHLUSSBERICHT FERTIG
═══════════════════════════════════════════
Projekt: <Name>
Stand: <ABGESCHLOSSEN | TEILWEISE — N von M Abschnitten fertig>
Ziel erreicht: <JA | TEILWEISE | NEIN>

Was wurde erstellt:
  .deepwork/PROJECT-COMPLETE.md  (vollständige Projekt-Zusammenfassung) ✓
  ./NEXT-STEPS.md                (konkrete nächste Schritte) ✓
  .deepwork/KNOWLEDGE-BASE.md    (gesammeltes Wissen aus dem Projekt) ✓
  Quality Gate Checklist abgehakt ✓

Gesamtkosten des Projekts: ~$<X.XX> | ~<N> Tokens
═══════════════════════════════════════════
```
