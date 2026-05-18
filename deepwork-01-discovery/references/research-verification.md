# Research Verification Protocol

All research findings must be verified before being used to make decisions. A single source is an unverified claim.

---

## The Verification Requirement

**Never use a single source as the basis for a plan decision.**

Before any finding influences the plan, ask:
- Can I find at least one other independent source that says the same thing?
- Do the sources agree on the specifics, or just the general direction?
- Are the sources current (within the last 12–18 months for technology)?
- Are the sources actually independent (not citing each other)?

---

## Confidence Levels

| Sources | Confidence | How to treat it |
|---------|-----------|------------------|
| 1 source | ⚠️ Low | Label as `[unverified]`. Do not build plan on it without a spike. |
| 2 independent sources agreeing | ✓ Medium | Acceptable as plan input. Note the sources. |
| 3+ independent sources agreeing | ✓✓ High | Treat as established fact. |
| Sources disagree | ❓ Conflicted | Note the conflict. Ask user which to trust, or design plan to handle both cases. |
| No sources found | ❌ Unknown | Treat as assumption. Mark explicitly as `unverified assumption` in PLAN.md. |

---

## Verification Process for Key Findings

### Step 1: Identify the claim
"Library X supports feature Y" / "Approach Z has performance problem W" / "API A has rate limit B"

### Step 2: Find independent verification
- Use a different search tool (if used WebSearch, try Exa or context7)
- Use a different query formulation
- Check official documentation (primary source)
- Check community discussion (secondary source — stack overflow, reddit, HN)
- Check code examples that use the library in production

### Step 3: Assess agreement
- Do sources agree? → Confidence up
- Do sources contradict? → Flag the conflict; dig deeper
- Can't find a second source? → Mark as `[unverified]`

### Step 4: Date-check
- For technology: anything older than 18 months should be re-verified against current docs

---

## Source Quality Ranking

1. **Official documentation**
2. **Empirical test** (you ran the code and saw the result)
3. **Official GitHub issues/releases**
4. **Peer-reviewed publications / standards bodies**
5. **High-quality technical blog posts**
6. **Stack Overflow accepted answers** (check date — outdated answers persist)
7. **Reddit / HN discussions**
8. **AI-generated summaries** (including Claude's own knowledge — always verify independently)

⚠️ Claude's own training knowledge is **not** an independent source.
