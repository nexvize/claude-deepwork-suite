# Token Log Protocol

Paul wants to know exactly how many tokens were consumed, for what, and by which tools — per section, per phase, per project.

---

## When to Log

| Event | Log Entry |
|-------|----------|
| After EVERY section completes | Section entry in `cost-log.md` |
| After every phase (01, 02, 03 batch, 04 run) | Phase-aggregate entry |
| Before every `/clear` | Final session-level entry |
| At project end | Update `cost-summary.md` |

---

## Format: `cost-log.md`

File location: `.deepwork/cost-log.md`  
Mode: **Append-only** — never delete old entries.

```markdown
## <ISO-8601 datetime> — <Section or Phase Name>

- skill: deepwork-<NN>-<name>
- phase: <01-discovery | 02-refine | 03-execute | 04-autopilot>
- section: <section name or "phase-level">
- duration: <Xm Ys>
- input_tokens: <N>
- output_tokens: <N>
- cache_read_tokens: <N>
- cache_hit_rate: <0.00–1.00>
- est_only: false
- agents:
  - Explore(2): research substeps 2.1 + 2.2
  - Plan(1): counter-proposal for plan hardening
- mcp_calls:
  - context7: 4 calls
  - exa: 2 calls
- est_cost_usd: <X.XX>
- notes: <1–2 sentences on what was notable>
```

---

## Format: `cost-summary.md`

```markdown
# Cost Summary: <Project Name>

## By Phase
| Phase | Input Tokens | Output Tokens | Cache Read | Est. Cost USD |
|-------|-------------|---------------|------------|---------------|
| 00-bootstrap | ... | ... | ... | ... |
| 01-discovery | ... | ... | ... | ... |
| **TOTAL** | ... | ... | ... | **...** |
```

---

## Cost Estimation Model (Claude Opus 4.7 approximate)

```
est_cost = (input_tokens / 1_000_000 * 15) 
         + (output_tokens / 1_000_000 * 75)
         + (cache_read_tokens / 1_000_000 * 1.5)
```

Label as estimate. Real costs visible in Anthropic Console.
