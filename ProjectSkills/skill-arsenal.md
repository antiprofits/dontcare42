# Skill Arsenal — Global Inventory

All skills ever added to this repository, in any status.
Update this file every time a skill is installed, parked, or removed.

---

## Active Skills — In Repo (`.claude/skills/`)

### Meta / Governance

| Skill | Source | Hash prefix | Scope | Added |
|-------|--------|-------------|-------|-------|
| `task-observer` | `rebelytics/one-skill-to-rule-them-all` | `60bfdcd9` | global | 2026-07-18 |

> Note: `task-observer` keeps its `references/` folder (3 `.md` files) — these are text files the skill loads on demand, not binary assets.

### LLM Routing & Token Efficiency (OmniRoute)

| Skill | Source | Hash prefix | Scope | Added |
|-------|--------|-------------|-------|-------|
| `omni-compression` | `diegosouzapw/OmniRoute` | `4f76b5aa` | global | 2026-07-18 |
| `omni-context-rtk` | `diegosouzapw/OmniRoute` | `b73f3756` | global | 2026-07-18 |
| `omni-resilience` | `diegosouzapw/OmniRoute` | `a83680aa` | global | 2026-07-18 |
| `omni-inference` | `diegosouzapw/OmniRoute` | `e2d73cb2` | global | 2026-07-18 |

> OmniRoute itself (self-hosted provider gateway, 264+ LLMs, ~1.6B free tokens/month) is noted
> as a future integration for SEARCHDNA probe LLM calls — see `AGENTS.md` → Provider Boundaries.

### LLM & AI Development

| Skill | Source | Hash prefix | Scope | Added |
|-------|--------|-------------|-------|-------|
| `llm-application-dev` | `moizibnyousaf/ai-agent-skills` | `40d1e099` | global | 2026-06-27 |

### Video Production (HeyGen Hyperframes Suite)

| Skill | Source | Hash prefix | Scope | Added |
|-------|--------|-------------|-------|-------|
| `hyperframes` | `heygen-com/hyperframes` | `2c53ce65` | global | 2026-06-27 |
| `hyperframes-core` | `heygen-com/hyperframes` | `7610a4f0` | global | 2026-06-27 |
| `hyperframes-cli` | `heygen-com/hyperframes` | `f1c3aa4d` | global | 2026-06-27 |
| `hyperframes-animation` | `heygen-com/hyperframes` | `7605eed3` | global | 2026-06-27 |
| `hyperframes-creative` | `heygen-com/hyperframes` | `50a92937` | global | 2026-06-27 |
| `hyperframes-keyframes` | `heygen-com/hyperframes` | —          | global | 2026-06-27 |
| `hyperframes-registry` | `heygen-com/hyperframes` | `a65dd053` | global | 2026-06-27 |
| `embedded-captions` | `heygen-com/hyperframes` | `a2b6c054` | global | 2026-06-27 |
| `captions-overlay` | `heygen-com/hyperframes` | —          | global | 2026-06-27 |
| `faceless-explainer` | `heygen-com/hyperframes` | `51731155` | global | 2026-06-27 |
| `general-video` | `heygen-com/hyperframes` | `49315015` | global | 2026-06-27 |
| `motion-graphics` | `heygen-com/hyperframes` | `608c9298` | global | 2026-06-27 |
| `motion-doctrine` | `heygen-com/hyperframes` | —          | global | 2026-06-27 |
| `music-to-video` | `heygen-com/hyperframes` | `e892ec28` | global | 2026-06-27 |
| `oversized-cursor` | `heygen-com/hyperframes` | —          | global | 2026-06-27 |
| `pr-to-video` | `heygen-com/hyperframes` | `60d3ec8a` | global | 2026-06-27 |
| `product-launch-video` | `heygen-com/hyperframes` | `1b1a4713` | global | 2026-06-27 |
| `remotion-to-hyperframes` | `heygen-com/hyperframes` | `3f5441e7` | global | 2026-06-27 |
| `seam-craft` | `heygen-com/hyperframes` | —          | global | 2026-06-27 |
| `slideshow` | `heygen-com/hyperframes` | `74020216` | global | 2026-06-27 |
| `talking-head-recut` | `heygen-com/hyperframes` | `01ef81d3` | global | 2026-06-27 |
| `cut-the-curve` | `heygen-com/hyperframes` | —          | global | 2026-06-27 |
| `changelog-video` | `heygen-com/hyperframes` | —          | global | 2026-06-27 |
| `figma` | `heygen-com/hyperframes` | —          | global | 2026-06-27 |
| `media-use` | `heygen-com/hyperframes` | `df639864` | global | 2026-06-27 |

---

## Active Skills — User Level (`~/.claude/skills/`)

These are installed globally at the user level, not committed to this repo.

| Skill | Source | Scope | Added |
|-------|--------|-------|-------|
| `find-skills` | `vercel-labs/skills` | user-global | 2026-06-27 |

---

## Parked Skills

Identified as useful; not installed. Install when the trigger condition is met.

| Skill | Source | Trigger condition | Identified |
|-------|--------|------------------|-----------|
| `tailwind-design-system` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-06-27 |

---

## Registered MCP Servers

MCP servers registered for this project. Governed by `AGENTS.md` → Local MCP Servers.
These are not skills and are not committed to the repository; they are registered in the
Claude Code project config.

| Server | Package | Version | Registration scope | Added |
|--------|---------|---------|-------------------|-------|
| `uni-code` | `@yuxianglin/uni-code` | 0.3.1 (pinned) | project (`/home/user/dontcare42`) | 2026-07-19 |

---

## Deprecated Skills

Skills that were active and have been removed.

| Skill | Source | Reason | Removed |
|-------|--------|--------|---------|
| — | — | — | — |

---

## Skill Counts

| Category | Count |
|----------|-------|
| Active (in repo) | 31 |
| Active (user-level) | 1 |
| Parked | 1 |
| Deprecated | 0 |
| MCP servers (registered) | 1 |
| **Total tracked** | **34** |
