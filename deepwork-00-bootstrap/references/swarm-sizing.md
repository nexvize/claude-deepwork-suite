# Swarm-Sizing — Entscheidungs-Guide

See `deepwork-env-setup/references/swarm-sizing.md` for the full guide.

Key rules:
- Swarm-Max: 100 Worker (from DEEPWORK-CONFIG.md)
- 5 Stufen: Direkt (0) / Schnell (2–5) / Standard (5–15) / Gründlich (15–50) / Maximum (50–100)
- ≥ 20 Worker → always show 5-Stufen-Format, let user choose
- Worktree-Isolation for all write-heavy swarms
- 80% cost-cap → warn; 100% → pause and ask
