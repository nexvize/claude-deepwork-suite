# Routing Guide — Section Type → Tool/Skill/Swarm

Use this table when deciding how to execute a section in deepwork-03. Match the section's primary character to the right tool. Document your choice in decisions.md.

---

## Quick Decision Table

| Section Character | Primary Tool | Notes |
|------------------|-------------|-------|
| Code with clear spec + test-ability | `superpowers:test-driven-development` | Always prefer TDD for code |
| Complex feature spanning multiple files | `superpowers:subagent-driven-development` | Fresh context per subagent |
| Multiple independent parallel tasks | `ruflo-swarm:swarm` or parallel `Agent` calls | Use swarm for write-heavy isolation |
| Single well-defined implementation task | `gsd-executor` Agent | Clean, fresh context |
| Frontend / UI component | `frontend-design` or `ui-ux-pro-max` Skill | Domain expertise |
| Bug / unexpected behavior | `gsd-debug` Skill + `superpowers:systematic-debugging` | |
| Code review / quality check | `gsd-code-review` or `coderabbit:code-review` | |
| Security audit | `security-review` Skill | |
| Research / documentation | Explore Agent (parallel) | 2–3 agents at once |
| Database / infrastructure | MCP-first (supabase, filesystem, github) | |
| Browser / UI testing | `mcp__plugin_playwright_playwright__*` | |
| Risky refactor (broad file changes) | `superpowers:using-git-worktrees` + swarm | Isolation is worth it |
| Simple single-file edit | Inline (Read + Edit) | No agent overhead needed |
| Configuration / settings | `update-config` Skill | |
| Diagram / slides | Figma MCP or Gamma MCP | |

---

## Decision Logic

```
Does this section require tests to be meaningful?
  YES → superpowers:test-driven-development (start here)
  NO ↓

Is this section 3+ independent parallel work streams?
  YES → ruflo-swarm (if write-heavy/risky) or parallel Agent calls
  NO ↓

Is this a specialized closed task (debug, review, security, UI)?
  YES → matching specialist Skill or Agent
  NO ↓

Is this a complex feature that benefits from fresh context?
  YES → gsd-executor Agent or superpowers:subagent-driven-development
  NO ↓

Is this a risky broad refactor?
  YES → git worktrees + swarm
  NO ↓

→ Inline with direct tools (Read, Edit, Write, Bash)
```

---

## Swarm vs Parallel Agents

| Use Swarm | Use Parallel Agents |
|-----------|-------------------|
| Multiple write-heavy tasks that could conflict | 2–4 independent reads/searches |
| Need worktree isolation | Single output per agent |
| Broad refactors or rewrites | Clearly scoped sub-tasks |
| Full audit or review of many files | Targeted lookups |
| Risk of merge conflicts | No file conflicts possible |

---

## Verification Tool Routing

After execution, verification must match what was built:

| What was built | Verification approach |
|---------------|----------------------|
| Code with tests | Run tests. Check pass/fail. |
| API endpoint | Call it with expected inputs, check outputs |
| UI component | Browser screenshot + manual check (playwright if available) |
| Data pipeline | Run with sample data, verify output format |
| Documentation | Read cold — does it make sense without context? |
| Configuration | Apply it, check no regressions |
| Refactor | All existing tests still pass, behavior unchanged |

Always use `superpowers:verification-before-completion` if available — it adds a structured final check.

---

## Example Section → Tool Mappings

| Section Name | Tool Choice | Reason |
|-------------|-------------|--------|
| "Set up project structure + config files" | Inline (Write) | Trivial file creation |
| "Implement parser module" | TDD (`superpowers:test-driven-development`) | Complex logic, benefits from tests-first |
| "Build 3 independent API endpoints" | Swarm (3 workers, 1 per endpoint) | Parallel, write-heavy, isolatable |
| "Set up CI/CD pipeline" | `gsd-executor` Agent | Defined spec, isolated task |
| "Full security audit" | `security-review` Skill | Specialist skill |
| "Implement dark mode + i18n + animations" | `ruflo-swarm` (3 workers) | 3 independent UI tracks |
| "Debug failing integration test" | `gsd-debug` Skill | Debugging specialist |
| "Write all user-facing docs" | `general-purpose` Agent | Documentation generation |
