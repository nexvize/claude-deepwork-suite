---
name: deepwork-01-discovery
description: "**When: MUST — Run after deepwork-00-bootstrap. Research, plan, and GO/NO-GO verdict.** Deep discovery phase for any project — software, business, content, research, or anything else. Forces a structured deep interview (as many questions as needed), 4-step tellerrand research (broad scan → deep drill → contrary findings → alternative approaches), iterative re-interview loops when research changes the picture, hard realism check with real NO-GO rights, plan hardening via stress-test, full memory/vector persistence of everything, and produces a handoff.md + token log for a clean context transition. Use ALWAYS after deepwork-00-bootstrap, or directly when: 'discovery', 'konzept', 'deep dive', 'is this realistic', 'what should we build', 'tiefenrecherche', 'plan', '/deepwork-01'. Even without explicit request — trigger whenever a project needs proper exploration before building."
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
  - Bash
  - Task
  - AskUserQuestion
  - Skill
---

# deepwork-01: Discovery

**Part 2 of the deepwork suite.** This skill forces real thinking before building. It interviews, researches, stress-tests, and produces a plan that can survive contact with reality.

**Read first:** All shared protocols live in `references/`. Read these before running the first ⚐ check:
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/native-protocols.md` — alle nativen Protokolle (Brainstorm, Spike, Verify, Debug, etc.)
- `references/tool-awareness.md` — use at every ⚐ point
- `references/memory-persistence.md` — how/when/where to persist
- `references/token-log-protocol.md` — how to log tokens
- `references/handoff-protocol.md` — handoff.md schema
- `references/interview-rounds.md` — question bank
- `references/research-substeps.md` — 4-step research guide
- `references/verdict-rubric.md` — GO/GO-WITH-CUTS/NO-GO criteria
- `references/routing.md` — section routing decisions
- `references/model-selection.md` — when to use Opus vs Sonnet, missing tools format
- `references/self-reflection.md` — internal controlling at every ⚐
- `references/research-verification.md` — source verification protocol
- `references/user-profile.md` — non-technical user assumption
- `references/decision-levels.md` — 5-Stufen-Empfehlung für alle User-Entscheidungen

---

## Step 0 — Setup ⚐

**Tool check:** Read `.deepwork/tool-inventory.md` if it exists (deepwork-00 wrote it). If not, run a quick inventory: which skills are in the system-reminder? Which MCPs are injected? Which Ruflo plugins active?

**Directory setup:**
```
.deepwork/
  journal/
  research/
  outputs/
  cost-log.md        (create if missing, headers only)
  decisions.md       (create if missing, headers only)
  tool-inventory.md  (create if missing)
```

**Foundation docs:** Read `.planning/PROJECT.md`, `REQUIREMENTS.md`, `ROADMAP.md` (from deepwork-00/gsd-new-project). If missing, write minimal versions in `.deepwork/planning/` before continuing.

**Self-reflection check ⚐** (see `references/self-reflection.md`): Am I starting from the right foundation? Is the user's actual goal clear, or am I assuming?

**User profile ⚐** (see `references/user-profile.md`): Assume non-technical user. Watch for knowledge gaps in all interview responses.

---

## Step 1 — Deep Interview: Round A ⚐

**Read:** `references/interview-rounds.md` for the full question bank.

Use `AskUserQuestion` in rounds of 2–4 questions. Ask **as many rounds as needed** — stop when each topic area is genuinely clear, not after a fixed number.

Cover in order:
1. **What & Why** — Problem, target user, pain, binary success criterion
2. **Scope & Constraints** — Budget (time/money), deadline, tech requirements, hard Don'ts
3. **Context** — User's role, existing assets, past attempts, why now
4. **Known Unknowns** — Biggest uncertainty, explicit assumptions (at least 3), risk tolerance

After each round: persist via `references/memory-persistence.md` (Tier 1 always, Tiers 2–3 if available). Write to `.deepwork/journal/<date>-01-interview-A.md`.

---

## Step 2 — Tellerrand Research (4 substeps) ⚐

**Read:** `references/research-substeps.md` for exact instructions and agent prompts for each substep.

**Recherche-Tiefe festlegen:** Bevor du startest, zeige dem User via `AskUserQuestion` die 5-Stufen-Auswahl (aus `references/decision-levels.md`, Kategorie B). Empfehle die Stufe, die zum Projekt-Kontext passt. Passe die Agent-Anzahl in 2.1–2.4 entsprechend an.

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

### 2.1 — Broad Scan
Spawn **3 parallel `Explore`-Agents** — bei Stufe 1–2 weniger, bei Stufe 4–5 mehr:
- Agent A: Existing solutions / market landscape
- Agent B: Technical libraries/frameworks (for software projects)
- Agent C: Domain context, standards, regulations

Raw outputs → `.deepwork/outputs/research-broad-scan/`  
Synthesis → `.deepwork/research/broad-scan.md`

### 2.2 — Deep Drill
Spawn **1 `general-purpose`-Agent pro vielversprechenden Lead** aus Broad Scan (2–5 Leads, parallel).

**MCP-Routing (Pflicht-Reihenfolge):**
- Library/Framework-Fragen → `mcp__context7__*` IMMER zuerst
- Web-Recherche → exa → firecrawl → WebSearch (nie direkt zu WebSearch springen)
- Code-Beispiele → GitHub MCP

Outputs → `.deepwork/outputs/research-deep-drill/`  
Synthesis → `.deepwork/research/deep-drill.md`

### 2.3 — Contrary Research
Spawn **1 `Explore`-Agent** um aktiv Failure-Modes, Regrets, "why we stopped using X" Stories, HN/Reddit-Kritik zu finden. Das ist der wichtigste und am häufigsten übersprungene Schritt.

Output → `.deepwork/research/contrary-findings.md`

### 2.4 — Tellerrand Options
Run **1 `Plan`-Agent** mit: "Given this project goal and constraints, what if we solved this completely differently? Produce minimum 3 genuine alternatives (not strawmen)."

Output section in final SUMMARY.md.

**Final synthesis:** `.deepwork/research/SUMMARY.md` (all 4 sections). Store in Ruflo embeddings for semantic recall (wenn Ruflo verfügbar — sonst nur Filesystem).

**Research Verification ⚐** (see `references/research-verification.md`):
Before any finding from research influences the plan, verify it with ≥2 independent sources. Mark unverified findings as `[unverified]` in SUMMARY.md. Do not build plan decisions on single-source claims.

**Self-reflection check ⚐:** Does the research change the goal, the approach, or any core assumption? If yes → apply insight-integration (see `references/self-reflection.md` — "Insight check").

**Persist** research summary via `references/memory-persistence.md`.

**Obsidian sync (if vault configured):** Copy `research/SUMMARY.md` to `<vault>/Projects/<slug>/Deepwork/Research-Summary.md`. See `references/tool-awareness.md` for vault setup instructions.

**Missing tools check ⚐:** At this point, review which research tools were unavailable. Log any in `.deepwork/tool-inventory.md` under `## Missing Tools`. Format: see `references/model-selection.md`.

---

## Step 3 — Adaptive Re-Interview: Round B ⚐

Based on research findings, run targeted follow-up questions.

**When to ask:**
- Research found a tellerrand option the user didn't mention → "Alternative X would be 3× cheaper because Y — relevant?"
- Common failure mode uncovered → "Projects like this often fail at Z. Is that a concern?"
- Assumption from Round A looks shaky → ask for clarification
- Regulatory/competitive landscape changes the picture → confirm user knows

**Non-technical translation ⚐** (see `references/user-profile.md`): Before each follow-up question, check if the research finding requires explanation in plain terms.

**Max 2 re-interview rounds.** If questions keep multiplying, note as Open Issues and move on.

Persist each round → `.deepwork/journal/<date>-01-interview-B.md`.

---

## Step 4 — Plan Draft ⚐

Write `.deepwork/PLAN.md`:

```markdown
# Plan: <Project Name>

## Goal
<What success looks like. Must match the binary success criterion from the interview.>

## Chosen Approach
<Why this approach over the tellerrand alternatives. Specific reasoning.>

## Tellerrand Alternatives Not Chosen
| Alternative | Why Not |
|-------------|----------|

## Scope
### In
### Out

## Execution Sections
| # | Section | Estimated effort | Key dependencies |
|---|---------|-----------------|------------------|

## Assumptions (explicit, with status)
| # | Assumption | Status | Fallback if wrong |
|---|-----------|--------|-------------------|

## Risks
| Risk | Severity | Mitigation |
|------|----------|------------|

## Open Questions
<Things not yet resolved — for re-interview or deepwork-02 discussion>
```

**Self-reflection check ⚐:** Read the draft plan as if you were the user (non-technical). Does it solve the right problem? Is it the simplest approach that works?

**Non-technical review ⚐** (see `references/user-profile.md` checklist): Run the Non-Technical User Checklist before presenting the plan.

---

## Step 5 — Plan Hardening ⚐

**Run in parallel:**

**Stress-test:** Invoke `kreuzverhoer` — Run `Skill` tool → `kreuzverhoer` on `PLAN.md`. Challenge: Is the chosen approach actually the simplest? Are the effort estimates realistic? Are the assumptions verifiable or just wishful thinking? Is each section genuinely independent?

**Counter-proposal:** Spawn 1 `Plan`-type Agent with prompt: "Given this project goal and constraints [paste from PLAN.md], write an alternative plan that makes different architectural or approach choices."

**Reality check:** Apply effort ×2 multiplier. Does the plan still fit within constraints? Adjust scope if not.

Hardening findings → `.deepwork/decisions.md` and updated `PLAN.md`.

---

## Step 6 — Realism Verdict (HARD) ⚐

**Read:** `references/verdict-rubric.md` for the full scoring rubric.

Score all 6 dimensions. Apply verdict logic. Write `.deepwork/VERDICT.md`.

**Present verdict to user via `AskUserQuestion`.**

**NO-GO is not failure. It's the skill working.**

---

## Step 7 — Handoff + Token Log + Memory Snapshot + Clear ⚐

**1. Write `./handoff.md`** following `references/handoff-protocol.md` exactly.

**2. Token log:** Follow `references/token-log-protocol.md`. Write to `.deepwork/cost-log.md`.

**3. Memory snapshot:** Final sync of journal + decisions.md.

**4. Update cost-summary.md** with Phase 01 aggregate.

**5. Clear-trigger output:**
```
═══════════════════════════════════════════
DISCOVERY-PHASE ABGESCHLOSSEN
═══════════════════════════════════════════
Ergebnis: <GO — wir bauen | GO-WITH-CUTS — wir bauen, aber mit Einschränkungen | NO-GO — jetzt noch nicht>

Was vorliegt:
  handoff.md (Übergabe-Dokument mit dem gesamten Plan) ✓
  Kosten protokolliert (.deepwork/cost-log.md) ✓
  Notizen gespeichert (.deepwork/journal/) ✓

Wie es weitergeht:
  → /clear eingeben (leert den Kontext für einen sauberen Start)
  → dann /deepwork-02-refine (Details klären und Umsetzungsplan fertigstellen)
═══════════════════════════════════════════
```

**6. Obsidian sync:** If vault is configured, sync `PLAN.md`, `VERDICT.md`, `handoff.md`, `decisions.md` to vault.
