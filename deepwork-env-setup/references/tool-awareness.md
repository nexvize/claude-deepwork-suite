# Tool-Awareness — Decision Guide

Every significant decision point in a deepwork skill is marked ⚐. At each ⚐, run this check before proceeding inline.

---

## The Check (run at every ⚐)

Ask yourself: **"Is there a tool that would do this better than me doing it inline right now?"**

Better = higher quality output, more parallelism, less context load, more reproducibility, or the tool has domain expertise I don't.

Then pick from the hierarchy below. Document your choice in 1 sentence in `.deepwork/journal/` or `.deepwork/decisions.md`.

---

## Decision Hierarchy

### 1. Skill from the catalog?
Use the `Skill` tool to invoke an existing skill.

**Deepwork-native (immer verfügbar — keine externen Abhängigkeiten):**

| Task | Ansatz |
|------|--------|
| Brainstorming / divergent thinking | Native — `references/native-protocols.md` → Brainstorm Protocol |
| Plan stress-test / Annahmen hinterfragen | `kreuzverhoer` (Skill tool) |
| Verification before completing | Native — `references/native-protocols.md` → Verification Protocol |
| Debugging wenn Verifikation schlägt fehl | Native — `references/native-protocols.md` → Debug Protocol |
| TDD workflow | Native — `references/native-protocols.md` → TDD Protocol |
| Existierende Docs/Research einlesen | Native — `references/native-protocols.md` → Document Ingest Protocol |
| Code Review am Ende | Native — `references/native-protocols.md` → Code Review Protocol |
| Technische Frage als Spike klären | Native — `references/native-protocols.md` → Spike Protocol |
| Neue Projektdokumente anlegen | Native — PROJECT.md, REQUIREMENTS.md etc. direkt schreiben (Step 3.5) |
| Quality Gate zwischen Phasen | Native — `references/native-protocols.md` → Quality Gate Checklist |

**Optionale externe Skills (nur nutzen wenn vorhanden — nie als Pflicht):**

| Task | Skill (optional) |
|------|------------------|
| Frontend / UI work | `frontend-design` oder `ui-ux-pro-max` |
| Vertiefte Security-Analyse | `security-review` |
| Tool-Inventur / Übersicht | `find-skills`, `tool-orchestrator` |
| Config / Hooks / Settings ändern | `update-config` |
| Kosten-Tracking | `ruflo-cost-tracker` |

### 2. MCP tool?
Use when an MCP has domain-specific access or capabilities.

**WICHTIG: Prescriptives MCP-Routing — immer diese Reihenfolge einhalten, nie überspringen.**

#### Web-Recherche (Reihenfolge einhalten)
1. **Exa** (`mcp__exa__web_search_exa`) — falls in tool-inventory.md verfügbar → IMMER zuerst
2. **Firecrawl** (`mcp__firecrawl__firecrawl_search`) — falls verfügbar → zweite Wahl
3. **WebSearch** — nur wenn Exa UND Firecrawl nicht verfügbar

**Niemals direkt zu WebSearch springen wenn bessere Tools verfügbar sind.**

#### Seiten scrapen / Inhalte lesen
1. Firecrawl (`mcp__firecrawl__firecrawl_scrape`) — bevorzugt
2. Playwright (`mcp__plugin_playwright_playwright__browser_navigate` + `browser_snapshot`)
3. WebFetch — Fallback

#### Library / Framework Dokumentation
`mcp__context7__resolve-library-id` → `mcp__context7__query-docs`
**Immer context7 zuerst** — nie WebSearch für Library-Docs wenn context7 verfügbar.

#### Dateien außerhalb des Projekts
`mcp__filesystem__*` → Bash als Fallback

#### Vollständige MCP-Tabelle

| Task | MCP (bevorzugt → Fallback) |
|------|---------------------------|
| Library / Framework Docs | `mcp__context7__*` → WebSearch |
| Web-Recherche (broad) | `mcp__exa__web_search_exa` → `mcp__firecrawl__firecrawl_search` → WebSearch |
| Seite scrapen | `mcp__firecrawl__firecrawl_scrape` → Playwright → WebFetch |
| GitHub Repos / Issues / PRs | `mcp__github__*` oder `mcp__plugin_github_github__*` |
| Dateien außerhalb Projekt | `mcp__filesystem__*` → Bash |
| Figma Designs | `mcp__claude_ai_Figma__*` |
| Browser-Automation | `mcp__plugin_playwright_playwright__*` |
| Persistenz (Ruflo) | `mcp__ruflo__memory_store`, `memory_search`, `memory_retrieve` |
| Semantic Search | `mcp__ruflo__embeddings_generate`, `embeddings_search` |
| Swarm-Management | `mcp__ruflo__swarm_init`, `agent_spawn`, `task_assign` |
| Autopilot-Loop | `mcp__ruflo__autopilot_enable`, `autopilot_log` |

### 3. Specialized Agent (via `Agent` tool)?
Use when the task is closed, specialized, and benefits from a fresh context window.

| Task | Agent type |
|------|------------|
| Codebase durchsuchen / erkunden | `Explore` |
| Architektur / Planung | `Plan` |
| Multi-Step Research | `general-purpose` |
| Code review (detailliert) | `feature-dev:code-reviewer` |
| Debugging | `gsd-debugger` (falls verfügbar) |

### 4. Swarm?
Use when multiple independent work streams exist.

### 5. Loop / Background Worker?
Use when the work is recurring, cache-sensitive, or long-running.

### 6. Parallel Task calls (inline)?
Use for 2–4 independent reads/searches that don't need a full agent.

### 7. Inline (direct tool call)?
Only when: Single, focused, non-parallelizable action.

---

## Web-Research-Safety-Regel

Bei Browser-/Web-Research nur lesende, sichere Aktionen ohne User-Bestätigung durchführen.

**Immer pausieren + User benachrichtigen bei:** Logins, Form-Submits, Downloads, Auto-Klicks, Uploads, Zahlungs- oder Account-Aktionen, Schreibzugriffe auf externe Dienste.
