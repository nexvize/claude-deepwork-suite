# Documentation Standard — Swarm/Agent Output Handling

When a Swarm, Agent, or MCP-tool produces output, it must be stored in a way that's immediately useful after a `/clear` — not just "saved", but synthesized, indexed, and linked.

---

## The Two-Layer Rule

Every significant output gets stored **twice**:

### Layer 1 — Raw Output
Exact output, unmodified, in:
```
.deepwork/outputs/<section-id>/<agent-type>-<YYYY-MM-DD-HHmm>.md
```

Examples:
- `.deepwork/outputs/02-tellerrand-research/Explore-2026-05-16-1432.md`
- `.deepwork/outputs/05-implement-parser/gsd-executor-2026-05-16-1601.md`
- `.deepwork/outputs/05-implement-parser/ruflo-swarm-worker1-2026-05-16-1605.md`

Why: the raw output may contain details that only become relevant later. Don't lose them.

### Layer 2 — Synthesis
3–5 key takeaways in the journal entry:
```
.deepwork/journal/<YYYY-MM-DD>-<phase>-<section>.md
```

Synthesis format:
```markdown
### <YYYY-MM-DD HH:MM> — <Agent/Swarm> output: <section>
**Kind:** research | learning | decision | risk
**Agent:** <Explore | Plan | gsd-executor | ruflo-swarm | ...>
**Raw output:** .deepwork/outputs/<section>/<file>

**Key takeaways:**
1. <Most important finding>
2. <Second finding>
3. <Third finding>
4. <Impact on plan / next section>
5. <Risk or open question uncovered>

**Memory tags:** projekt:<slug>, kind:<type>, section:<id>
```

---

## Section-Level Documentation

After an entire section completes (deepwork-03-execute Step 5), write a section-completion entry:

```markdown
## Section Complete: <Section Name> — <YYYY-MM-DD>

**Status:** done
**Verification:** <what was checked and passed>
**What was built/produced:** <concrete output — files, endpoints, docs, etc.>

**Key decisions made during execution:**
- <decision 1>
- <decision 2>

**Learnings (vs plan):**
- <what was different from what was planned>

**Impact on remaining sections:**
- Section <N>: <how this changes it, if at all>

**Risks discovered:**
- <any new risk that emerged during this section>

**Raw outputs:** .deepwork/outputs/<section>/
**Memory tags:** projekt:<slug>, phase:03, section:<id>, kind:learning
```

---

## Knowledge Synthesis (for new steps)

Before starting any new section, run a knowledge-synthesis pass to avoid re-reasoning from scratch.

**Step 1: Search**
- `mcp__ruflo__embeddings_search` with the section goal as query → top 5 semantically related past outputs
- `mcp__ruflo__memory_search` with tags `kind:decision` + `kind:risk` for this project

**Step 2: Synthesize**
Write a 2–4 sentence "Brief-an-mich-selbst":
> "We're in section [X]. Relevant past decisions: [Y]. Risks to watch: [Z]. Key constraint: [W]."

This brief lives only in the working context — no need to persist it. It's the jumpstart for the section.

---

## Output Quality Bar

A well-documented section should answer these questions from files alone (no asking):

1. **What was built?** → section-completion entry
2. **How did it go vs plan?** → learnings block
3. **What changed for remaining sections?** → impact block
4. **What raw artifacts exist?** → .deepwork/outputs/ links
5. **What would I Google if I had to redo this?** → key takeaways in synthesis

If any of these are unanswerable from the files, the documentation is incomplete.

---

## Project-Level Knowledge Base

At project end (or after significant milestones), produce `.deepwork/KNOWLEDGE-BASE.md`:

```markdown
# Knowledge Base: <Project Name>

## Architecture Decisions
<Link to relevant decisions.md entries>

## Key Learnings
<Aggregate of all `kind:learning` journal entries>

## Risks & Mitigations
<Current status of all risks from handoff.md>

## What We'd Do Differently
<From the assumptions reality check>

## Technical Reference
<Links to key raw outputs that have lasting reference value>
```

This file is what enables "nachhaltig angefangen werden kann" — it's the durable institutional knowledge of the project.
