# Autopilot Contract Template

The contract is the pre-flight agreement between you and Claude. Everything in it means Claude doesn't need to ask during execution. Gaps in the contract = forced pauses during the run.

Copy this template, fill it out during the mega-interview, and save it as `.deepwork/AUTOPILOT-CONTRACT.md`.

---

```markdown
# Autopilot Contract: <Project Name>
Created: <ISO-8601>
Signed: <YES — filled after user confirms>

---

## Project Essence
<3–5 sentences: what, for whom, why. Must be concrete enough to make implementation decisions from.>

## Success Criterion
<Single binary statement. True or false.>

## Scope Hard Limits
### Always In
- <item — these MUST be completed>
### Always Out
- <item — if discovered necessary, PAUSE instead of doing it>
### Cut if needed (priority order, first cut first)
1. <lowest priority item — sacrifice this first if time/budget tight>
2. <next>
3. <next>

---

## Research Depth
Tellerrand openness: <1=stay focused on the obvious path | 3=explore some alternatives | 5=be genuinely open to radical pivots>
Research thoroughness: <1=quick scan | 3=standard | 5=deep drill everything>

---

## Decision Defaults

### Approach Decisions
When a technical choice arises between options, prefer:
- <e.g., "TypeScript over JavaScript">
- <e.g., "REST over GraphQL unless there's a clear reason">
- <e.g., "SQLite for local, PostgreSQL for hosted">
- <e.g., "existing library over custom implementation">

### Uncertainty Handling
When genuinely uncertain about an approach and no default applies:
- <try the simpler option first / take the option with lower blast radius / pause>

### Scope Creep Handling
When a useful-but-out-of-scope feature is discovered:
- <document it in open-issues and continue / pause and ask>

### Quality vs Speed
When quality and speed trade off:
- <always prioritize quality / prefer quality but cut scope to fit deadline>

---

## Assumption Fallbacks
<!-- For each major assumption from discovery, specify the fallback -->
| Assumption | Fallback if False |
|-----------|------------------|
| <assumption 1> | <what to do: continue with cut / pause / try alternative X> |
| <assumption 2> | <fallback> |
| <assumption 3> | <fallback> |

---

## Risk Responses
<!-- For each significant risk from discovery -->
| Risk | Severity | If It Materializes |
|------|----------|-------------------|
| <risk 1> | High | <continue / cut scope / pause> |
| <risk 2> | Mid | <mitigation action / continue> |
| <risk 3> | Killer | ALWAYS PAUSE |

---

## Resource Caps
cost_cap_usd: <X.XX or "none">
token_cap_input: <N or "none">
time_cap_hours: <N or "none">
cost_warning_at_pct: 80
sections_per_run: <"all" or N>
max_parallel_agents: <N, default 4>

---

## Tool Policy
### Always use (if available)
- <e.g., "TDD for all code sections">
- <e.g., "ruflo-swarm for parallel sections">

### Prefer
- <e.g., "gsd-executor for implementation tasks">
- <e.g., "context7 for library docs">

### Avoid
- <e.g., "don't use playwright (not installed)">
- <e.g., "don't make external API calls to X">

### Require approval before
- <e.g., "any git push">
- <e.g., "any external service call">
- <e.g., "any infrastructure change">

---

## Escalation Rules (PAUSE triggers)
<!-- When any of these happen, pause and send PushNotification -->

Always pause for:
1. Realismus Verdikt = NO-GO
2. Killer-severity risk materializes
3. Cost cap reached (100%)
4. Verification fails 3 times consecutively
5. Decision is required that has no default in this contract

Also pause for (user-specific):
- <custom trigger 1>
- <custom trigger 2>

Don't pause for:
- Tellerrand research findings within configured depth
- Plan adjustments when contract defaults apply
- Section completion (no clear between sections in autopilot mode)
- Low/Mid risks with mitigations

---

## Communication
push_notification_on_pause: <yes/no>
final_report: always
intermediate_updates: <never / after each section / after each phase>

---

## Autopilot Auto-Permissions
<!-- These flags allow the autopilot to act without pausing. Default: all true.
     The autopilot is the hands-off mode — these defaults exist so it can actually run hands-off.
     All auto-actions are still logged to .deepwork/journal/ for traceability.
     Override any flag to false if you want to be asked for that specific action. -->

allow_auto_migration: true
<!-- true = old .deepwork/ structure gets migrated automatically without pause -->

allow_auto_vault_bootstrap: true
<!-- true = Obsidian vault folder (D:\Claude\ObsidianVault\) created automatically if missing -->

allow_auto_mcp_install: true
<!-- true = missing required MCPs (context7, filesystem, exa, firecrawl) installed automatically -->

allow_auto_hooks_setup: true
<!-- true = default hook set activated without individual confirmation -->

allow_large_swarms: true
<!-- true = swarms with 20+ workers start without pre-confirmation (still subject to cost cap) -->

prefer_parallel_sections: true
<!-- true = independent sections run in parallel via swarm instead of sequentially -->

skip_pre_permission_blocks: true
<!-- true = pre-permission plain-language blocks go to journal only, not to chat UI -->

---

## Always-Pause Triggers (NOT overridable — these always cause a pause)
<!-- These 8 triggers cannot be disabled — they protect against irreversible or high-risk actions.
     You CAN add more triggers below, but you CANNOT remove any of the 8 default ones. -->

1. Verdikt = NO-GO (project viability check failed — user must decide)
2. Killer-severity risk materializes during execution
3. Cost cap 100% reached
4. Verification fails 3 consecutive times on same section
5. Web-Safety-Pause: any login, form submit, data upload, auto-click, payment, or write action on external service
6. External write actions (git push, API write, infrastructure change) — unless explicitly removed from require_approval_before list
7. Out-of-contract decision required with no applicable default
8. Self-reflection reveals major course correction needed (≥2 remaining sections invalidated)

Also always pause for (user-defined additions):
- <add your own triggers here>

---

## Additional Notes
<anything else that would affect decisions during the run>
```
