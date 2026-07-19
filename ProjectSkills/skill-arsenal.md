# Skill Arsenal — Global Inventory

All skills ever added to this repository, in any status.
Update this file every time a skill is installed, parked, or removed.

> **Hash / checksum authority:** Computed SHA-256 hashes for all installed skills are in
> `skills-lock.json`. That file is auto-managed — do not edit it by hand and do not
> duplicate hashes here. The `Hash prefix` column has been removed from this table to
> prevent drift; `skills-lock.json` is the canonical source for all hash values.

---

## Active Skills — In Repo (`.claude/skills/`)

Skills in `.claude/skills/` are **repository-scoped**: available only within this
repository. Do not label them "global" — that label applies only to user-level installs
(`~/.claude/skills/`).

**Status key:**

| Status | Meaning |
|--------|---------|
| `Active` | All referenced files committed; skill is in use |
| `Complete` | SKILL.md is self-contained; no unreferenced local files |
| `Reference Only` | Requires external infrastructure to activate (e.g. OmniRoute deployment) |
| `Incomplete` | SKILL.md references companion files (scripts/, references/, assets/) not committed per trimming rule |

### Meta / Governance

| Skill | Source | Status | Scope | Added |
|-------|--------|--------|-------|-------|
| `task-observer` | `rebelytics/one-skill-to-rule-them-all` | `Active` | repository-scoped | 2026-07-18 |

> Note: `task-observer` keeps its `references/` folder (3 `.md` files: `environments.md`,
> `skill-authoring.md`, `weekly-review.md`) — text files the skill loads on demand, not binary assets.

### LLM Routing & Token Efficiency (OmniRoute)

| Skill | Source | Status | Scope | Added |
|-------|--------|--------|-------|-------|
| `omni-compression` | `diegosouzapw/OmniRoute` | `Reference Only` | repository-scoped | 2026-07-18 |
| `omni-context-rtk` | `diegosouzapw/OmniRoute` | `Reference Only` | repository-scoped | 2026-07-18 |
| `omni-resilience` | `diegosouzapw/OmniRoute` | `Reference Only` | repository-scoped | 2026-07-18 |
| `omni-inference` | `diegosouzapw/OmniRoute` | `Reference Only` | repository-scoped | 2026-07-18 |

> OmniRoute skills are reference documentation only — they do not activate routing or
> compression without a running OmniRoute deployment. See `AGENTS.md` → OmniRoute Integration Status.

### LLM & AI Development

| Skill | Source | Status | Scope | Added |
|-------|--------|--------|-------|-------|
| `llm-application-dev` | `moizibnyousaf/ai-agent-skills` | `Complete` | repository-scoped | 2026-06-27 |

> Source authority note: `llm-application-dev/SKILL.md` frontmatter incorrectly states
> `source: wshobson/agents`. The lockfile (`skills-lock.json`) and this registry are
> authoritative: source is `moizibnyousaf/ai-agent-skills`.

### Video Production (HeyGen Hyperframes Suite)

All hyperframes suite skills are `Incomplete`: SKILL.md files reference companion directories
(`references/`, `scripts/`, `assets/`, `sub-agents/`, `examples/`) that are not committed
per the SKILL.md-only trimming rule. The doctrine content within each SKILL.md is readable;
the referenced helper files are not present in this repository.

Exceptions: `captions-overlay` and `oversized-cursor` are self-contained (no local file
references) and are classified `Complete`.

| Skill | Source | Status | Scope | Added |
|-------|--------|--------|-------|-------|
| `hyperframes` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `hyperframes-core` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `hyperframes-cli` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `hyperframes-animation` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `hyperframes-creative` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `hyperframes-keyframes` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `hyperframes-registry` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `embedded-captions` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `captions-overlay` | `heygen-com/hyperframes` | `Complete` | repository-scoped | 2026-06-27 |
| `faceless-explainer` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `general-video` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `motion-graphics` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `motion-doctrine` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `music-to-video` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `oversized-cursor` | `heygen-com/hyperframes` | `Complete` | repository-scoped | 2026-06-27 |
| `pr-to-video` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `product-launch-video` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `remotion-to-hyperframes` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `seam-craft` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `slideshow` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `talking-head-recut` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `cut-the-curve` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `changelog-video` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `figma` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |
| `media-use` | `heygen-com/hyperframes` | `Incomplete` | repository-scoped | 2026-06-27 |

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

## Provenance and Licensing

| Source | License | Verification status | Notes |
|--------|---------|---------------------|-------|
| `rebelytics/one-skill-to-rule-them-all` | CC BY 4.0 | Confirmed in upstream README | — |
| `heygen-com/hyperframes` | Not documented in SKILL.md | Unverified — check upstream repo before redistribution | Applies to all 25 hyperframes suite skills |
| `diegosouzapw/OmniRoute` | Not documented in SKILL.md | Unverified | Applies to omni-compression, omni-context-rtk, omni-resilience, omni-inference |
| `moizibnyousaf/ai-agent-skills` | Not documented in SKILL.md | Unverified | SKILL.md frontmatter incorrectly states `wshobson/agents`; lockfile and this registry are authoritative |
| `vercel-labs/skills` | Not documented in SKILL.md | Unverified | find-skills (user-level only, not committed) |

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
