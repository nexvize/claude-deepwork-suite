# Documentation Standard — Swarm/Agent Output Handling

When a Swarm, Agent, or MCP-tool produces output, it must be stored in a way that's immediately useful after a `/clear`.

---

## The Two-Layer Rule

Every significant output gets stored **twice**:

### Layer 1 — Raw Output
Exact output, unmodified, in:
```
.deepwork/outputs/<section-id>/<agent-type>-<YYYY-MM-DD-HHmm>.md
```

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

After an entire section completes (deepwork-03-execute Step 5):

```markdown
## Section Complete: <Section Name> — <YYYY-MM-DD>

**Status:** done
**Verification:** <what was checked and passed>
**What was built/produced:** <concrete output>
**Key decisions made during execution:**
**Learnings (vs plan):**
**Impact on remaining sections:**
**Risks discovered:**
**Raw outputs:** .deepwork/outputs/<section>/
**Memory tags:** projekt:<slug>, phase:03, section:<id>, kind:learning
```

---

## Output Quality Bar

A well-documented section should answer these questions from files alone:
1. **What was built?**
2. **How did it go vs plan?**
3. **What changed for remaining sections?**
4. **What raw artifacts exist?**
5. **What would I Google if I had to redo this?**
