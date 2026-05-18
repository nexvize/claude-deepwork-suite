# Self-Reflection & Internal Controlling

Every significant step in a deepwork session must be verified — not just completed. This file defines when and how to check that work is still on track, errors haven't crept in, and the direction is still correct.

---

## When to Run a Self-Reflection Check

At every ⚐ checkpoint, before moving to the next step, run the check. Also trigger immediately when:
- A new insight, finding, or piece of information arrives that could change the direction
- Something takes significantly longer or is significantly harder than expected
- A result looks different from what was planned
- An assumption is confirmed false

---

## The Controlling Triangle

```
Goal (what the user actually needs)
  ↕ aligned?
Plan (what we decided to build/do)
  ↕ aligned?
Execution (what we're actually doing right now)
```

If any level is misaligned → stop and correct before continuing.

---

## The Self-Reflection Check (run at every ⚐)

**1. Goal check:** Is what I'm doing right now still serving the user's actual goal?
**2. Plan check:** Is the current plan still the best way to reach the goal?
**3. Execution check:** Am I executing the plan correctly, or have I drifted?
**4. Insight check (only when new information arrives):** Does this change the Goal, Plan, or Execution level?

---

## Response to Check Results

- **All clear → continue.** Document briefly in `decisions.md`.
- **Minor drift → correct inline.** Fix + note in decisions.md.
- **Plan needs adjustment → adjust.** Update PLAN.md + handoff.md + decisions.md.
- **New insight invalidates section → restart section.** Reset to `ready-to-execute`.
- **New insight invalidates approach → present to user.** Options: adjust plan / restart discovery / continue with risk accepted.

---

## Error Patterns to Watch For

| Error | How it appears | Catch it by |
|-------|---------------|-------------|
| Scope creep | Section grows beyond its spec | Re-read section spec before starting |
| Goal drift | Solving a different problem than stated | Re-read success criterion at each ⚐ |
| Assumption blindness | Building on an assumption that was falsified | Check assumptions table in handoff.md |
| Research recency | Using outdated information as if current | Check source dates |
| Tool bias | Using a familiar tool instead of the right tool | Run routing check at every ⚐ |
| Completion theater | Marking done without verifying | Binary criterion must be explicitly checked |
| User assumption mismatch | Building what was said, not what was meant | Re-read user-profile.md |
