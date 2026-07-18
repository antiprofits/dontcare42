# Dependency Map

Visual dependency graphs for skill pipelines and data pipelines.
Update this file when a skill is added that participates in a pipeline,
or when a new pipeline is defined.

---

## SEARCHDNA — Demand Intelligence Pipeline

The core data pipeline. Each step depends on the output of the previous.

```
TalorData API  +  YouTube API
        ↓
   Demand Probe
   (lib/searchdna/probes/trends.ts + youtube.ts)
   Skill: llm-application-dev (signal classification)
        ↓
   Normalisation
   (DemandSignal schema — lib/searchdna/types.ts)
        ↓
   Signal Clustering
   (lib/searchdna/cluster.ts)
        ↓
   Demand Gap Detection
   (gap = demand volume − captured volume)
        ↓
   Opportunity Ranking
   (composite score: Intensity × Velocity × Gap)
        ↓
   SearchDnaPage.tsx
   Skill: tailwind-design-system [PARKED — Phase 3]
```

**Skill dependencies per step:**

| Pipeline step | Active skill | Status |
|--------------|-------------|--------|
| Signal classification / probe LLM calls | `llm-application-dev` | active |
| UI layer | `tailwind-design-system` | parked |

---

## SEARCHDNA — Phase 2 SERP Extension

Extends Phase 1 with paid TalorData SERP data.

```
TalorData SERP endpoint
        ↓
   SERP Probe
   (lib/searchdna/probes/serp.ts)
        ↓
   (joins Phase 1 pipeline at Normalisation)
```

---

## Video Production Pipeline (Hyperframes Suite)

The hyperframes skills form a layered composition system.
These are not currently scoped to any active project — available globally.

```
User brief / assets
        ↓
   hyperframes           ← entry point — always read first
        ↓
   ┌────────────────────────────────────────────┐
   │  hyperframes-core   (composition contract) │
   │  hyperframes-cli    (dev loop / rendering) │
   │  hyperframes-creative (design direction)   │
   │  hyperframes-animation (motion rules)      │
   │  hyperframes-keyframes (seek-safe timelines│
   │  hyperframes-registry (blocks / components)│
   └────────────────────────────────────────────┘
        ↓
   media-use             ← resolve BGM / SFX / images
        ↓
   Specialised workflow (pick one):
   ├── general-video
   ├── faceless-explainer
   ├── motion-graphics
   ├── slideshow
   ├── talking-head-recut
   ├── music-to-video
   ├── pr-to-video
   ├── product-launch-video
   ├── changelog-video
   └── remotion-to-hyperframes
        ↓
   Caption layer (optional):
   ├── embedded-captions
   └── captions-overlay
        ↓
   Motion techniques (optional):
   ├── cut-the-curve      (velocity-matched seams)
   ├── seam-craft
   ├── motion-doctrine
   └── oversized-cursor
        ↓
   figma                  ← import Figma assets into composition
```

**Skill dependency rule:** always invoke `hyperframes` before any other
video skill — it routes to the correct specialised workflow.

---

## Skill Dependency Risk Register

If a skill changes, the following downstream skills or pipeline steps are affected:

| Skill changed | Downstream impact |
|--------------|------------------|
| `llm-application-dev` | SEARCHDNA probe LLM calls — re-validate signal classification |
| `hyperframes-core` | All hyperframes composition outputs — re-test rendering |
| `hyperframes` (entry) | All video workflow routing — update workflow triggers |
| `lib/searchdna/types.ts` | All probes, cluster, UI — full type-check required |
