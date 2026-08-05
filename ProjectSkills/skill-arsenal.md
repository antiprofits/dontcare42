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

These are installed at the user level and are **not committed to this repo**.

> **Ephemeral container note:** Skills installed to `~/.claude/skills/` in a remote container
> session are lost when the container is reclaimed. They must be re-installed on the local
> machine to persist. SHAs below are the install-time commit SHAs where recorded.
> User-level skills are not tracked in `skills-lock.json` (which covers repo-committed skills only).

| Skill | Source | Pinned SHA | License | Files | Local Mods | Added |
|-------|--------|------------|---------|-------|------------|-------|
| `find-skills` | `vercel-labs/skills` | unrecorded | Unverified | SKILL.md | none | 2026-06-27 |
| `aar-loop` | `coopersimson96/aar-loop` | `a7172d610760ba403af4cf3cb18dc0d895431b2e` | Unverified | SKILL.md, scripts/append_lesson.py | none | 2026-07-22 |
| `beautify-github-readme` | `oil-oil/beautify-github-readme` | `fa477898d7f62b3c4cf19224a6a4eb7ce4b4defc` | Unverified | SKILL.md, references/ ×7 | scripts/audit_readme.py excluded (read-only audit only; SKILL.md does not depend on it at runtime) | 2026-07-22 |
| `improve-animations` | `emilkowalski/skills` | unrecorded | Unverified | SKILL.md only | companion files excluded per SKILL.md-only trimming rule | 2026-07-22 |
| `mind-the-gap` | `emilkowalski/skills` | unrecorded | Unverified | SKILL.md only | companion files excluded per SKILL.md-only trimming rule | 2026-07-22 |
| `scroll-animations` | `emilkowalski/skills` | unrecorded | Unverified | SKILL.md only | companion files excluded per SKILL.md-only trimming rule | 2026-07-22 |

> **Excluded from install (emilkowalski/skills):** `animation-vocabulary` — excluded entirely;
> no governance entry created. Do not install.
>
> **Gap — wshobson/agents TypeScript skills:** Four TypeScript skills from `wshobson/agents`
> were approved for user-level install in a prior session. Their exact skill names were not
> captured in the governance record. Verify from local machine `~/.claude/skills/` and add
> entries here before Phase 1 (local machine reinstall) begins.

---

## Parked Skills

Identified as useful; not installed. Install when the trigger condition is met.

| Skill | Source | Trigger condition | Identified |
|-------|--------|------------------|-----------|
| `tailwind-design-system` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-06-27 |
| `design-system-patterns` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |
| `accessibility-compliance` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |
| `responsive-design` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |
| `interaction-design` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |
| `visual-design-foundations` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |
| `web-component-design` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |
| `mobile-ios-design` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |
| `mobile-android-design` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |
| `react-native-design` | `wshobson/agents` | `SearchDnaPage.tsx` UI work begins (Phase 3) | 2026-07-22 |

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
| `rebelytics/one-skill-to-rule-them-all` | CC-BY-4.0 | Confirmed in upstream README | task-observer |
| `heygen-com/hyperframes` | Apache-2.0 | Confirmed in upstream repo LICENSE file and badge | Applies to all 25 hyperframes suite skills |
| `diegosouzapw/OmniRoute` | MIT | Confirmed in upstream repo README ("100% MIT self-hosted") | omni-compression, omni-context-rtk, omni-resilience, omni-inference |
| `moizibnyousaf/ai-agent-skills` | MIT | Confirmed in upstream repo LICENSE file | llm-application-dev; SKILL.md frontmatter incorrectly states `wshobson/agents`; lockfile and this registry are authoritative |
| `wshobson/agents` | MIT | Confirmed in repo LICENSE | Source for parked `tailwind-design-system` + `ui-design` suite; `llm-application-dev` SKILL.md frontmatter claims this source but lockfile is authoritative (`moizibnyousaf/ai-agent-skills`) |
| `coopersimson96/aar-loop` | Unverified | Not checked | aar-loop (user-level); verify license before redistribution |
| `oil-oil/beautify-github-readme` | Unverified | Not checked | beautify-github-readme (user-level); verify license before redistribution |
| `emilkowalski/skills` | Unverified | Not checked | improve-animations, mind-the-gap, scroll-animations (user-level); verify license before redistribution |
| `vercel-labs/skills` | Unverified | Not checked | find-skills (user-level only, not committed) |

---

## Deprecated Skills

Skills that were active and have been removed.

| Skill | Source | Reason | Removed |
|-------|--------|--------|---------|
| — | — | — | — |

---

## Skill Counts

| Category | Count | Notes |
|----------|-------|-------|
| Active (in repo) | 31 | See `.claude/skills/` |
| Active (user-level) | 6 | find-skills, aar-loop, beautify-github-readme, improve-animations, mind-the-gap, scroll-animations |
| Active (user-level, gap) | ? | wshobson TypeScript skills — approved but names unrecorded; verify from local machine |
| Parked | 10 | wshobson/agents ui-design suite |
| Deprecated | 0 | — |
| Excluded | 1 | animation-vocabulary (emilkowalski/skills) — do not install |
| MCP servers (registered) | 1 | uni-code @0.3.1 |
| **Total tracked (confirmed)** | **48+** | Excludes unrecorded wshobson TypeScript skills |
