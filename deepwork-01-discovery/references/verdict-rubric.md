# Verdict Rubric — GO / GO-WITH-CUTS / NO-GO

The verdict is the hardest part of deepwork-01. It requires honest judgment, not optimism.

---

## Verdicts

| Verdict | Meaning |
|---------|----------|
| **GO** | Plan is sound. Risks are known and manageable. Move to deepwork-02. |
| **GO-WITH-CUTS** | Viable, but scope must be reduced or a pivot must happen before deepwork-02. Specify exactly what changes. |
| **NO-GO** | Not viable as-is. Specify the blocker and what would need to change before re-trying. Skill blocks progression. |

---

## Scoring Rubric

Evaluate each dimension. **Killers trump everything** — one Killer = immediate NO-GO.

### 1. Feasibility (technical / practical)
- **Killer:** Core technical assumption is demonstrably false
- **High risk:** Core approach hasn't been done before and we don't know if it's possible
- **Mid risk:** Technically feasible but requires skills/tools we don't currently have
- **Low risk:** Clear path exists, similar things have been built before

### 2. Effort vs. Value
- **Killer:** Estimated effort (after ×2 realism multiplier) is clearly disproportionate to the stated value
- **High risk:** Tight budget/deadline but plan scope is large
- **Mid risk:** Doable within constraints but requires cutting some nice-to-haves
- **Low risk:** Effort fits clearly within available time and resources

### 3. Market / Demand (for user-facing products)
- **Killer:** Target users demonstrably don't have the problem we're solving
- **High risk:** No evidence of demand beyond the builder's intuition
- **Mid risk:** Indirect evidence of demand, no direct validation
- **Low risk:** Clear evidence of demand

### 4. Assumption Integrity
- **Killer:** A core assumption is known to be false
- **High risk:** 2+ core assumptions are unverified with no plan to verify
- **Mid risk:** Some unverified assumptions with clear verification paths
- **Low risk:** Assumptions are mostly verified or have low-risk fallbacks

### 5. Risk Profile
- **Killer:** One or more Killer-severity risks with no mitigation
- **High risk:** Multiple High-severity risks, some with weak mitigation
- **Mid risk:** Mostly Mid/Low risks, all with clear mitigation paths
- **Low risk:** Risks are known, small, and well-mitigated

### 6. Clarity
- **Killer:** Success criterion is undefined
- **High risk:** Goals are vague; multiple interpretations possible
- **Mid risk:** Core goal clear but some ambiguity in scope
- **Low risk:** Binary success criterion exists and is measurable

---

## Verdict Logic

```
Any Killer dimension → NO-GO
3+ High dimensions → NO-GO (or GO-WITH-CUTS if cuts eliminate the Highs)
2 High dimensions → GO-WITH-CUTS with explicit scope changes
1 High dimension → GO with that risk documented and monitored
Mostly Mid/Low → GO
```

---

## GO-WITH-CUTS Requirements

1. **Exactly what is cut from scope** (be specific)
2. **Why this cut is sufficient** (does it eliminate the High-risk dimension?)
3. **What the new success criterion is** after the cut

---

## NO-GO Requirements

1. **The exact blocker** (which Killer/High dimension, why it can't be mitigated)
2. **What would need to change** before retrying
3. **A suggested next step** (spike? Pivot? Different problem to solve?)

A NO-GO is not a failure — it's the skill doing its job. Better to catch it here than after 3 months of building.

---

## Verdict File: `.deepwork/VERDICT.md`

```markdown
# Verdict: <GO | GO-WITH-CUTS | NO-GO>

## Date
## Scoring Summary
| Dimension | Score | Notes |
|-----------|-------|-------|
| Feasibility | Low/Mid/High/Killer | |
| Effort vs Value | ... | |
| Market/Demand | ... | |
| Assumption Integrity | ... | |
| Risk Profile | ... | |
| Clarity | ... | |

## Reasoning
## For GO-WITH-CUTS: Required Changes
## For NO-GO: Blockers and Next Steps
## Signed off by user
```
