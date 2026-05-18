# Memory Persistence Protocol

Everything that happens during a deepwork session must survive a `/clear`. This file defines what to persist, where, and how — so any future session can pick up exactly where things left off.

---

## The Core Guarantee

After a `/clear`, a new Claude session reads:
1. `handoff.md` (project root)
2. `.deepwork/journal/` (process log)
3. `.deepwork/decisions.md` (decision log)
4. `.deepwork/cost-log.md` (token history)

And can **immediately start working** on the next pending section without asking a single question. If it can't — something is missing from the persistence layer.

---

## What to Persist

| Kind | Examples | Tags |
|------|---------|------|
| `interview` | User's answers, revealed constraints, stated preferences | `kind:interview` |
| `research` | Findings, sources, key facts, tellerrand alternatives | `kind:research` |
| `decision` | "We chose X over Y because Z" | `kind:decision` |
| `pivot` | "Original plan changed from A to B because C" | `kind:pivot` |
| `verdict` | GO / GO-WITH-CUTS / NO-GO + reasoning | `kind:verdict` |
| `risk` | Risks identified, severity, current mitigation status | `kind:risk` |
| `learning` | What was discovered during execution (vs plan) | `kind:learning` |
| `assumption` | Assumption + its current verification status | `kind:assumption` |
| `tool-choice` | Why Swarm vs Agent vs inline for a given step | `kind:tool-choice` |

---

## Three-Tier Persistence

### Tier 1 — File System (always, no dependencies)

**`.deepwork/journal/<YYYY-MM-DD>-<phase>-<section>.md`**

Append-only narrative log. Each entry:
```markdown
### <YYYY-MM-DD HH:MM> — <phase> / <section>
**Kind:** <interview | research | decision | pivot | verdict | risk | learning | assumption | tool-choice>
**Summary:** <2–4 sentences of what happened>
**Details:** <full content, quotes from user, research findings, reasoning>
**Next:** <what this implies for the next step>
```

**`.deepwork/decisions.md`**

Concise chronological decision log (cross-reference from journal):
```markdown
### <YYYY-MM-DD HH:MM> — <decision name>
- Kind: decision | pivot | verdict
- Decision: <what was decided>
- Why: <brief reason>
- Alternatives: <what was rejected and why>
- Impact: <what sections/plans this affects>
```

### Tier 2 — Ruflo Memory + Vector (when available)

**Structured memory** via `mcp__ruflo__memory_store`:
```json
{
  "content": "<what happened>",
  "tags": ["projekt:<slug>", "phase:<N>", "section:<id>", "kind:<type>"],
  "metadata": {
    "phase": "01-discovery",
    "section": "tellerrand-research",
    "date": "<ISO-8601>"
  }
}
```

**Embeddings** for semantic search via `mcp__ruflo__embeddings_generate` → stored, then `embeddings_search` to recall by similarity.

**Knowledge graph** via `mcp__ruflo__kg_extract` for entities and relations:
- Entities: project name, technologies, actors, risks
- Relations: "requires", "replaces", "conflicts-with", "depends-on"

**Hierarchical storage** via `mcp__ruflo__agentdb_hierarchical-store` for nested context.

### Tier 3 — MCP Memory Fallback

If Ruflo is not available but MCP memory (knowledge-graph server in `.mcp.json`) is live:
- Store key facts via the memory MCP's store tool
- Use semantic recall when starting a new section

---

## When to Persist

| Moment | Persist what | Where |
|--------|-------------|-------|
| After each interview round | User answers, new constraints | Journal + Ruflo memory |
| After research synthesis | Key findings, tellerrand options | Journal + embeddings |
| After each decision | Decision + alternatives | decisions.md + Ruflo tagged `kind:decision` |
| After each plan change / pivot | Diff + reason | Journal + decisions.md tagged `kind:pivot` |
| After each verdict | Full verdict + reasoning | Journal + Ruflo tagged `kind:verdict` |
| After each swarm/agent output | Raw output + synthesis | outputs/ + journal |
| Before every `/clear` | Final sync + snapshot | All tiers |

---

## Recall Patterns

### At session start (after `/clear`)
1. Read `handoff.md` — get current state.
2. Read `.deepwork/decisions.md` — recall all key decisions.
3. `mcp__ruflo__memory_search` with tags `projekt:<slug>` + `kind:decision` + `kind:risk` — pull top 10 most relevant memories.
4. Synthesize into **Brief-an-mich-selbst** (2–3 sentences): "We're building X. Last session we completed Y. Next is section Z. Key constraints: A, B. Watch out for risk C."

### Before starting a new section
- `mcp__ruflo__embeddings_search` with section name + goal → pull semantically related past decisions and learnings.
- Check decisions.md for any decision that affects this section.

### After a pivot
- Search journal for all entries with `kind:assumption` whose assumptions are now impacted.
- Update those entries and the handoff.md `## Assumptions Reality Check`.

---

## Tagging Convention

```
projekt:<slug>          — project identifier (use kebab-case project name)
phase:<0|1|2|3|4>       — which deepwork phase
section:<id>            — section number or name
kind:<type>             — see table above
severity:<low|mid|high|killer>  — for risk entries
status:<open|resolved|realized> — for risk entries
```

Always include `projekt:` and `kind:` at minimum.
