# Research Sub-Steps — Tellerrand Research Guide

The 4-step research process for deepwork-01. Each step has a different goal. Don't collapse them — each one catches things the others miss.

---

## Overview

```
Step 2.1 — Broad Scan      → What's out there? Map the landscape.
Step 2.2 — Deep Drill      → What do the details actually say?
Step 2.3 — Contrary Search → Where does this go wrong?
Step 2.4 — Tellerrand      → What if we did this completely differently?
```

Spawn parallel subagents for 2.1 and run 2.2–2.4 based on what 2.1 uncovers.

---

## Step 2.1 — Broad Scan

**Goal:** Map the entire landscape. Don't drill yet — just find what exists.

**Parallel agents to spawn:**

**Agent A — Market/Existing Solutions:**
- What tools/products/services already exist for this problem?
- Tools: `WebSearch`, Exa (`mcp__exa__*`), Firecrawl (`mcp__firecrawl__*`)
- Queries: `"<problem domain> tools"`, `"<problem> alternatives"`, `"<problem> comparison"`

**Agent B — Technical Landscape (for software projects):**
- What libraries, frameworks, APIs exist that could help?
- Tools: `mcp__context7__resolve-library-id` + `query-docs`, `mcp__github__search_code`, `WebSearch`

**Agent C — Domain/Industry Context:**
- Regulatory requirements? Standards? Best practices?
- Tools: `WebSearch`, Exa, Firecrawl

**Output:** `.deepwork/research/broad-scan.md`

---

## Step 2.2 — Deep Drill

**Goal:** Get the actual details on the 3–5 most promising leads from the broad scan.

**What "deep" means:**
- For a tool: read the actual docs, not just the landing page. Check GitHub issues for common problems.
- For a library: read the API reference, look at real usage examples, check performance benchmarks.
- For a competitor: find their pricing, limitations, user reviews, known complaints.

**Agents:** 1 per lead (run in parallel). Use:
- `mcp__context7__query-docs` for library docs
- `mcp__github__get_file_contents` for source/examples
- WebFetch + Firecrawl for crawling relevant pages
- Exa for semantic search into specific domains

**Output:** `.deepwork/research/deep-drill.md`

---

## Step 2.3 — Contrary Search

**Goal:** Find the failure modes, criticisms, and "why not" arguments. This is the most important and most often skipped step.

**What to search for:**
- `"why X is bad"`, `"X alternatives"`, `"X problems"`, `"stopped using X"`
- `"why we chose Y over X"`, `"X vs Y lessons learned"`
- HackerNews, Reddit r/programming, dev.to, postmortems

**Questions to answer:**
- What do practitioners regret about choosing this approach?
- What are the hidden costs (maintenance, scaling, edge cases)?
- What did teams try first and abandon?

**Agent:** 1 focused agent. Use `WebSearch`, Exa, Firecrawl.

**Output:** `.deepwork/research/contrary-findings.md`

---

## Step 2.4 — Tellerrand Options

**Goal:** Deliberately explore alternatives to the current direction.

**The key question:** "What if we solved this completely differently?"

**Prompt templates:**
- "Instead of building X, what if we just used Y?"
- "Instead of a [app/service/tool], what if this was a [script/API/plugin/workflow]?"
- "What if the human did step X manually, and automation only handled Y?"
- "What's the 10× cheaper version of this?"
- "What's the version a single developer could maintain forever?"

**Minimum 3 genuine alternatives** — not strawmen, real options worth considering.

**Output section in `.deepwork/research/SUMMARY.md`:**
```markdown
## Tellerrand Options

| Alternative | Core Idea | Upsides | Why probably not (but confirm with user) |
|-------------|-----------|---------|------------------------------------------|
| <name> | <1 sentence> | <benefits> | <why we might skip it — but ask> |
```

---

## Research Synthesis

After all 4 steps, write `.deepwork/research/SUMMARY.md`:

```markdown
# Research Summary — <Project Name> — <date>

## TL;DR
<3–5 sentences. What the research tells us about whether and how to proceed.>

## State of the Art
## Technical Findings
## Domain Context
## Contrary Findings
## Tellerrand Options
## Key Implications for the Plan
## Assumptions Affected by Research
## Open Questions Research Couldn't Answer
```

Store SUMMARY.md in Ruflo embeddings for semantic recall.
