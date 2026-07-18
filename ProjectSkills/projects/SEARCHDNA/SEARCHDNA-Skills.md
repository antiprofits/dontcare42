# SEARCHDNA — Skill Registry

All skills relevant to the SEARCHDNA Demand Intelligence module.
See `ProjectSkills/dependency-map.md` for the full pipeline graph.

---

## Active Skills

### llm-application-dev

| Field | Value |
|-------|-------|
| **Source** | `moizibnyousaf/ai-agent-skills` |
| **Status** | `active` |
| **Scope** | global (primary use: SEARCHDNA) |
| **Install path** | `.claude/skills/llm-application-dev/SKILL.md` |
| **Lock hash** | `40d1e099` |
| **Added** | 2026-06-27 |

**Purpose:** Guides LLM integration patterns — prompt engineering, RAG, typed I/O contracts —
used in the SEARCHDNA probe layer for signal classification and demand scoring.

**Pipeline position:**
```
Demand Probe (trends.ts / youtube.ts)
    ↓
[llm-application-dev]  ← classifies raw signals into DemandSignal.signalType
    ↓
Normalisation (types.ts)
```

**Customisations:** None yet. As probe LLM calls are implemented, add project-specific
prompt constraints here (e.g., always output `signalType` as one of the union values in `types.ts`).

---

## Parked Skills

### tailwind-design-system

| Field | Value |
|-------|-------|
| **Source** | `wshobson/agents` |
| **Status** | `parked` |
| **Install trigger** | `SearchDnaPage.tsx` UI work begins (Phase 3) |
| **Identified** | 2026-06-27 |

**Purpose:** Provides Tailwind CSS design system patterns for the `SearchDnaPage.tsx` UI component.
Not relevant until the frontend build phase.

---

## Global Skills Available to SEARCHDNA

These are installed globally and available but not SEARCHDNA-specific.

| Skill | Relevance to SEARCHDNA |
|-------|----------------------|
| `find-skills` (user-level) | Discover new skills when a capability gap is identified |
| `hyperframes` suite | Not currently scoped — available if a video/report export surface is added |

---

## Planned Skills (Not Yet Identified)

| Capability needed | Phase | Notes |
|------------------|-------|-------|
| TypeScript data probe scaffolding | Phase 1 | May use a generic TS skill or custom probe template |
| Vector embedding / semantic search | Phase 2+ | If signal clustering uses embeddings instead of heuristic clustering |
| PDF extraction | Phase 3+ | Stirling-PDF REST API integration for ingesting industry report PDFs |
| Chart / data visualisation | Phase 3 | For SearchDnaPage.tsx demand metric displays |

---

## Skill Dependency Graph (SEARCHDNA)

```
TalorData API  +  YouTube API
        ↓
   Demand Probe
        ↓  ← llm-application-dev (signal classification)
   Normalisation  (lib/searchdna/types.ts — source of truth)
        ↓
   Signal Clustering  (lib/searchdna/cluster.ts)
        ↓
   Demand Gap Detection
        ↓
   Opportunity Ranking
        ↓
   SearchDnaPage.tsx  ← tailwind-design-system [PARKED]
```

---

## Definition of Done for SEARCHDNA Skills

A skill is correctly integrated in SEARCHDNA when:

- [ ] Listed in this file with full identity fields
- [ ] Listed in `ProjectSkills/skill-arsenal.md`
- [ ] `skills-lock.json` reflects the install
- [ ] `ProjectSkills/dependency-map.md` updated if skill fits a pipeline step
- [ ] `ProjectSkills/changelog.md` entry added
- [ ] Skill output validated against `lib/searchdna/types.ts` schema
