# Model Selection — Sonnet vs Opus

Quality is the primary criterion. The model choice should serve the work, not the budget — but token cost matters when it's high.

---

## Default: Opus for the Deepwork Suite

The deepwork suite runs complex, multi-step reasoning, plans, and creative problem-solving. Use **Claude Opus** (`claude-opus-4-7`) as the base model for all deepwork skills unless a specific reason to downgrade exists.

**Why Opus by default:** Discovery, verdict, planning, and hardening require genuine reasoning quality. A cheap but wrong plan costs more than the model savings.

---

## When to Use Sonnet

Use **Claude Sonnet** (`claude-sonnet-4-6`) for:

| Task | Reason |
|------|--------|
| Pure file reads / codebase scanning | No reasoning needed — just retrieval |
| Formatting / template filling | Mechanical task |
| Copying data between files | No judgment needed |
| Logging and summary formatting | Mechanical writing |
| WebSearch query construction | Prompt construction only |
| Parallel Explore agents for broad scanning | Speed > depth at this stage |
| Raw output storage / documentation writes | Structure-filling, not reasoning |

**Rule of thumb:** If the task requires judgment, tradeoff reasoning, or creative synthesis → Opus. If it's pattern-matching, formatting, or retrieval → Sonnet.

---

## Never Downgrade For

- Realism Verdict (6-dimension scoring)
- Plan Hardening (kreuzverhoer / counter-proposal)
- Deep Interview synthesis and re-interview
- Any step where the user is asked to make a commitment or decision
- Risk assessment and assumption integrity checks
- Research synthesis (SUMMARY.md writing)

---

## Missing Tools Notification

At each ⚐ point, check: "Is there a tool that would do this better that I don't currently have access to?"

If yes, pause and tell the user:
```
⚠️ Missing Tool: <tool name>
Purpose: <what it would do here>
How to get it: <install command / URL / setup steps>
Impact of missing: <what we lose by not having it>
Proceeding with: <fallback approach>
```

---

## Current Model IDs (as of 2026-05)

| Model | ID | Use for |
|-------|----|--------|
| Opus | `claude-opus-4-7` | All deepwork reasoning, planning, verdicts |
| Sonnet | `claude-sonnet-4-6` | Scanning, formatting, retrieval tasks |
| Haiku | `claude-haiku-4-5` | Avoid in deepwork — insufficient reasoning depth |
