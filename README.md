# claude-deepwork-suite

Deepwork Skills Suite for Claude Code — 4-mode AI project workflow system

## What is this?

A collection of Claude Code skills that bring structure, quality gates, and reproducibility to AI-assisted project work. Four modes for four different needs:

- **Mode 1 (Full Pipeline):** `deepwork-00-bootstrap` → `deepwork-01-discovery` → `deepwork-02-refine` → `deepwork-03-execute` → `deepwork-end-report`
- **Mode 2 (Quick-Use):** `deepwork-quick` — single protocol without pipeline
- **Mode 3 (Autopilot):** `deepwork-alt-autopilot` — autonomous multi-section run
- **Mode 4 (Transfer):** `deepwork-entry-analyze` — onboard existing projects

## Skills

| Skill | Mode | Description |
|---|---|---|
| `deepwork-env-setup` | Prereq | One-time machine setup: MCPs, plugins, vault, hooks |
| `deepwork-00-bootstrap` | 1 | Start a project: triage, routing, folder structure, foundation docs |
| `deepwork-01-discovery` | 1 | Research + plan + GO/NO-GO verdict |
| `deepwork-02-refine` | 1 | Plan → executable sections with success criteria |
| `deepwork-03-execute` | 1 | Execute one section (vertical slice), then /clear |
| `deepwork-end-report` | 1 | Final report + next steps |
| `deepwork-quick` | 2 | Single protocols without pipeline: Review, Debug, Spike, Refactor, Brainstorm |
| `deepwork-alt-autopilot` | 3 | Autonomous run without /clear, no manual input after start |
| `deepwork-entry-analyze` | 4 | Existing project: analyze, build structure, enable Mode 1 |

## Installation

Copy the `skills/` folder contents to `~/.claude/skills/` and the `commands/` folder contents to `~/.claude/commands/`.

Then run `/deepwork-env-setup` once to configure your environment.

## Configuration

All paths and limits are in `DEEPWORK-CONFIG.md`. Edit that file — nothing else needs changing.

Key settings: `DEEPWORK_VAULT_PATH`, `DEEPWORK_SWARM_MAX_WORKERS` (default: 100), `DEEPWORK_DEFAULT_COST_CAP_USD` (default: $5.00)

## License

MIT
