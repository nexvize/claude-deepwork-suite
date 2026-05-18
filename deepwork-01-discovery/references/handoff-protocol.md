# Handoff Protocol — Schema & Writing Guide

The `handoff.md` file is the single source of truth that bridges every phase and every `/clear`. A new Claude session must be able to read it cold and start working without asking a single question.

---

## File Location

Always written to `./handoff.md` in the **project root** — not inside `.deepwork/`. This keeps it findable without any context.

---

## Required Schema

```markdown
# Handoff: <Project Name>

## Meta
- created: <ISO-8601 datetime>
- last_updated: <ISO-8601 datetime>
- current_phase: <00-bootstrap | 01-discovery | 02-refine | 03-execute | 04-autopilot>
- current_skill: <deepwork-00 | deepwork-01 | deepwork-02 | deepwork-03 | deepwork-04>
- working_dir: <absolute path>
- verdict: <pending | GO | GO-WITH-CUTS | NO-GO>
- token_log_path: .deepwork/cost-log.md
- memory_tags: projekt:<slug>, phase:<N>

## Project Essence
<3–5 sentences: what, for whom, why now, what success looks like. Must be concrete, not vague.>

## Success Criterion
<Single binary statement. Either true or false. E.g.: "A user can run `lint-md README.md` and get structured output in under 2s.">

## Scope
### In
- <item>
### Out
- <item>

## Constraints
- <Budget, deadline, tech preferences, hard Don'ts>

## Assumptions
| # | Assumption | Status | Evidence / Fallback |
|---|-----------|--------|---------------------|
| 1 | <text> | unverified \| verified \| falsified | <notes> |

## Risks
| Risk | Severity | Mitigation | Status |
|------|----------|------------|--------|
| <text> | Low \| Mid \| High \| Killer | <text> | open \| mitigated \| realized |

## Chosen Approach
<Why this approach and not the tellerrand alternatives. 3–5 sentences.>

## Tellerrand Alternatives Considered
| Alternative | Why Not Chosen |
|-------------|----------------|
| <text> | <text> |

## Sections (Execution Plan)
Each section = one deepwork-03-execute invocation.

| # | Section Name | Status | Tool/Skill/Swarm | Verification Criterion | Outcome |
|---|-------------|--------|-----------------|----------------------|---------|
| 1 | <name> | pending \| in-progress \| done | <tool choice> | <binary check> | <filled when done> |

## Token Log Refs
- Phase 01 discovery: see .deepwork/cost-log.md entries tagged `phase:01`

## Memory Refs
- Ruflo tags: `projekt:<slug>`, search by `kind:decision`, `kind:learning`, `kind:risk`, `kind:pivot`
- Journal: .deepwork/journal/
- Decisions: .deepwork/decisions.md

## Autopilot Contract Status
- contract_file: .deepwork/AUTOPILOT-CONTRACT.md (if deepwork-04 was used)
- contract_status: not-created \| active \| expired

## Open Issues
- <discovered during execution that needs attention>

## Learnings
- <what was learned that wasn't in the plan>

## Assumptions Reality Check
| Assumption # | Original | Result | Impact on Remaining Sections |
|-------------|----------|--------|------------------------------|
| <N> | <text> | confirmed \| falsified: <detail> | <none \| sections X,Y need adjustment> |
```

---

## Writing Rules

**Be concrete, not vague.** "Set up project" is not a section name. "Create package.json + tsconfig.json + ESLint config" is.

**Success criterion must be binary.** "Works well" fails. "User can run X and get Y in under Zs" passes.

**Sections must be independently executable.** A new context (after `/clear`) picks up exactly one section and can complete it without reading anything else — except this handoff.md.

**Update in place, don't rewrite.** When a section completes, fill its `Status`, `Outcome`, and the `## Learnings` / `## Assumptions Reality Check` blocks.

**Verdikt is mandatory before sections start.** No sections should be `pending` while `verdict: pending`.

---

## Cold-Start Test

After writing or updating this file, ask: "If a new Claude session reads only this file, can it immediately start working on the next pending section without asking any questions?"

If no → the file is not complete. Add what's missing.
