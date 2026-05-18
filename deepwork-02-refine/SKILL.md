---
name: deepwork-02-refine
description: "**When: MUST — Run after deepwork-01-discovery. Turns the plan into executable sections with clear criteria.** Bridge between discovery and execution. Reads handoff.md + memory from deepwork-01, runs a clarifying interview when there are gaps, then does a deep discuss-phase-style walkthrough of how exactly each planned section will be implemented — tools, agents, swarms, tests, verification. If needed: new research to evaluate the implementation approach. Updates the plan, then produces an updated handoff.md ready for deepwork-03-execute. Use after deepwork-01-discovery, or whenever handoff.md exists and you need to turn a plan into an executable spec. Triggers: 'refine', 'discuss implementation', 'how do we build this', 'klären wie wir das umsetzen', '/deepwork-02', or when handoff.md exists with status 'GO'."
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

**Part 3 of the deepwork suite.** Takes a stichfest discovery output and turns it into an executable plan — with every section specified precisely enough that deepwork-03 can run without asking questions.

**Read first:**
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/native-protocols.md` — native Protokolle für Verifikation, Debugging, etc.
- `references/tool-awareness.md`
- `references/memory-persistence.md`
- `references/token-log-protocol.md`
- `references/handoff-protocol.md`
- `references/routing.md` — tool routing for each section
- `references/model-selection.md` — model selection guidance
- `references/self-reflection.md` — controlling at every ⚐
- `references/user-profile.md` — non-technical user assumption
- `references/decision-levels.md` — 5-Stufen-Empfehlung für alle User-Entscheidungen

---

## Step 0 — Load Context ⚐

**Read handoff.md** (project root). Parse all sections. If missing → tell user to run deepwork-01 first, stop.

**Read memory:** `.deepwork/decisions.md` + `.deepwork/journal/`. If Ruflo available: `mcp__ruflo__memory_search` with tags `projekt:<slug>` + `kind:decision` + `kind:risk` → top 10 entries.

**Brief-an-mich-selbst:** synthesize in 3–4 sentences: what the project is, what deepwork-01 decided, which sections need to be executed, what key constraints and risks apply. This brief is your context anchor for this session.

**Self-reflection check ⚐:** Is the plan I'm about to refine still the right plan? Does anything in the decisions.md or journal suggest a different direction would be better?

**User profile ⚐:** Re-read `references/user-profile.md`. Before any section discussion, confirm you're thinking about the user's actual context, not just the technical problem.

**Read tool-inventory:** `.deepwork/tool-inventory.md` — what tools are available?

---

## Step 1 — Clarifying Interview (only if needed) ⚐

Check the handoff.md for gaps:
- Open Questions still unresolved?
- Sections with vague verification criteria?
- Assumptions marked `unverified` that are critical for implementation?
- Any section so broad that it can't be executed without more context?

If gaps exist → focused `AskUserQuestion` rounds, **as many as needed to close the gaps**. Don't re-ask already decided questions (they're in decisions.md).

Persist answers → `.deepwork/journal/<date>-02-clarification.md`.

---

## Step 2 — Section-by-Section Deep Discussion ⚐

For each section in the handoff.md execution plan, work through:

**2.1 Implementation approach** (via AskUserQuestion if ambiguous, or decide from context):
- For **software:** What's the data flow? Which components? Which interfaces? Which libraries/frameworks?
- For **non-technical:** What's the workflow? Who does what? What are the touch points? What's the output format?

**Vertical Slice Check:** Ist diese Section ein vollständiger Feature-Slice (UI + Logik + Daten gemeinsam) oder eine horizontale Schicht (z.B. nur UI, nur Backend)? Horizontal-Schnitte können erst am Ende getestet werden — Vertical Slices ermöglichen frühes echtes Feedback. Falls die Section nur eine horizontale Schicht ist und das nicht explizit notwendig ist → prüfe ob ein Vertical Slice möglich wäre und empfehle diesen via AskUserQuestion.

**2.2 Tool routing** ⚐ (see `references/tool-awareness.md`):
- Which skill, agent, swarm, or MCP is best for this section?
- Braucht es TDD? → `references/native-protocols.md` → TDD Protocol
- Braucht es Worktree-Isolation? → Agent tool mit `isolation: "worktree"` (für riskante Writes)
- Profitiert es von einem Swarm? → `ruflo-swarm:swarm` (für parallele, unabhängige Teile)
- Kann ein `general-purpose` oder `Explore` Agent es erledigen?

Justify the choice in 1 sentence. Document it.

**Manual Step Check:** If the chosen tool/approach requires user action before execution (e.g., API key setup, Supabase project creation, GitHub repo initialization, Obsidian vault setup), **pause here**.

Output a detailed manual-step block:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DEINE AKTION NÖTIG — Abschnitt <N>: <Name>
Bevor ich hier weitermachen kann, musst du kurz selbst etwas einrichten.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Was du tun musst:
1. <konkreter Schritt mit genauen Anweisungen>
2. <konkreter Schritt>

Warum das nötig ist:
<1–2 Sätze — was wird dadurch möglich>

Wie du weißt, dass es geklappt hat:
<konkreter Check — "du siehst X" oder "führe Y aus und bekommst Z">

Danach:
Antworte mit: "Erledigt — <was eingerichtet wurde>"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**2.3 Verification criterion** (must be binary):
- "Tests pass" is binary if there are specific tests.
- "User can do X in Ys" is binary if testable.
- "Looks good" is NOT binary — specify what "good" means precisely.

**2.4 Section risks:**
- What could go wrong specifically in *this* implementation approach?
- Is there a dependency on another section (ordering matters)?

**2.5 Non-technical explanation (for each section):**
Write a plain-language description of what this section will produce and why it matters for the user's goal. This is not documentation — it's the explanation you give the user when presenting the refined plan. Use `references/user-profile.md` templates.

**2.6 Self-reflection check per section ⚐:**
- Is this section still necessary given everything I now know?
- Is there a simpler way to achieve the same outcome?
- Did any research finding (from deepwork-01) make this section easier or harder than planned?

Falls die Diskussion komplex wird → mehr `AskUserQuestion` Runden, Thema eingrenzen, Annahmen explizit machen.

Update handoff.md `## Sections` table as you go — each section should end this step with a complete row.

---

## Step 3 — Re-Research (if needed) ⚐

If discussion revealed a concrete technical uncertainty (e.g., "is library X actually usable for Y?", "does API Z support this use case?"), run a targeted mini-research.

Spawn 1–2 parallel agents (Explore, general-purpose) with focused queries. Use `mcp__context7__*` for library questions. Don't re-do the full research — just answer the specific question.

Write findings → `.deepwork/research/implementation-research.md` (append if file exists).

---

## Step 4 — Plan Update ⚐

Update `.deepwork/PLAN.md` based on the section discussions:

- **Small adjustments:** Edit in place, note the change in decisions.md.
- **Significant changes (approach changes, section restructuring):** Archive current plan as `.deepwork/PLAN-v<N>.md`, write a fresh `PLAN.md`, note the diff in `.deepwork/decisions.md`.

Note in decisions.md:
```markdown
### <date> — Plan updated in refine phase
- What changed: <brief>
- Why: <reason from discussion>
- Impact: <which sections affected>
```

---

## Step 4.5 — Kreuzverhoer: Execution Plan Stress-Test ⚐

**Invoke kreuzverhoer:** Run `Skill` tool → `kreuzverhoer` on the full refined execution plan (the updated `PLAN.md` + the sections table in `handoff.md`). For each section, challenge:
- Is the tool routing correct — or is there a simpler/better tool for this?
- Is the verification criterion actually binary and testable — or is it vague?
- Are the dependencies between sections correct and complete?
- Is the effort estimate realistic (apply ×2 multiplier mentally)?
- Does this section actually do what it claims, given the constraints?

Output → document findings and any resulting plan adjustments in `.deepwork/decisions.md`.

---

## Step 5 — Handoff Update + Token Log + Clear ⚐

**1. Update `./handoff.md`:**
- `last_updated` timestamp
- `current_phase: 02-refine`
- Each section: fill `Tool/Skill/Swarm` and `Verification Criterion` columns
- All sections should be `pending` → `ready-to-execute`
- Update `## Open Issues` with anything still open
- `## Memory Refs` — add any new Ruflo tags from this session

**2. Token log:** Write Phase 02 entry in `.deepwork/cost-log.md`.

**3. Memory persist:** All decisions and discussion outcomes → `.deepwork/decisions.md` + Ruflo memory.

**4. Update cost-summary.md** with Phase 02 aggregate.

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
  → /clear eingeben (leert den Kontext für einen sauberen Start)
  → dann /deepwork-03-execute (Umsetzung startet)
═══════════════════════════════════════════
```

---

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WAS JETZT?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Nach /clear:  /deepwork-03-execute  (eine Section nach der anderen)
Alternative:  /deepwork-alt-autopilot  (alle Sections automatisch, ohne manuelle /clear)

Wenn du Pause machst und später wiederkommst:
  Tippe einfach /deepwork-03-execute — der Skill liest handoff.md
  und weiß genau welche Section als nächstes dran ist.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
