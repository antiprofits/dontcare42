# Skill Changelog

Chronological record of skill additions, removals, and status changes.

---

## 2026-07-18

### Added
- `omni-compression` (diegosouzapw/OmniRoute) — RTK + Caveman token compression for LLM probe calls
- `omni-context-rtk` (diegosouzapw/OmniRoute) — context window compression via RTK filters
- `omni-resilience` (diegosouzapw/OmniRoute) — circuit breaker/cooldown patterns for ProbeAdapter error handling
- `omni-inference` (diegosouzapw/OmniRoute) — unified LLM inference routing reference
- `task-observer` v2.0.0 (rebelytics/one-skill-to-rule-them-all) — meta-skill that monitors
  sessions and logs skill improvement observations; feeds into ProjectSkills governance layer.
  Installed manually (curl) with `references/` folder retained (on-demand text files, not assets).

---

## 2026-06-27

### Added
- `find-skills` (vercel-labs/skills) — user-level global install; skill discovery utility
- `llm-application-dev` (moizibnyousaf/ai-agent-skills) — LLM probe patterns for SEARCHDNA
- `hyperframes` suite × 26 skills (heygen-com/hyperframes) — video production capability

### Parked
- `tailwind-design-system` (wshobson/agents) — pending SearchDnaPage.tsx UI work (Phase 3)

### Governance
- Created `AGENTS.md`, `CLAUDE.md`, and full `ProjectSkills/` registry structure
- Established skill trimming rule: only `SKILL.md` committed, no binary assets
