# AGENTS.md — Repository Constitution

Every AI agent working in this repository must read this file before touching any code.
It is the single source of truth for architecture, standards, and scope.

---

## Project Overview

This repository is the monorepo for a **Demand Intelligence platform**.
The first module is **SEARCHDNA** — a system that surfaces demand signals
(search intent, content consumption, purchase interest) across multiple data sources,
normalises them into a unified schema, and exposes metrics that answer four questions:

- How much does the market care? → **Demand Intensity**
- How fast is demand moving? → **Demand Velocity**
- How much demand is unserved? → **Demand Gap**
- How much demand does a brand own? → **Demand Capture**

Additional projects (Vault, NotchOS, Vantage) will follow the same conventions.
Each project lives under `ProjectSkills/projects/<name>/` for skill and dependency tracking.

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────┐
│                    SearchDnaPage.tsx                │  ← UI layer (Phase 4)
├─────────────────────────────────────────────────────┤
│              lib/searchdna/cluster.ts               │  ← Topic clustering engine
├──────────────────────────┬──────────────────────────┤
│  lib/searchdna/probes/   │  lib/searchdna/probes/   │
│       trends.ts          │      youtube.ts           │  ← Data probes (Phase 1)
├──────────────────────────┴──────────────────────────┤
│              lib/searchdna/types.ts                 │  ← Shared schema (source of truth)
└─────────────────────────────────────────────────────┘
          ↓                          ↓
   TalorData API              YouTube Data API
   (Trends + SERP)          (reuses CIE-1 ingest)
```

The Python AI engine (if introduced) follows a narrow-contract pattern:
typed input → typed output, no durable state, Pydantic models throughout.
See `ProjectSkills/projects/SEARCHDNA/SEARCHDNA-Skills.md` for the LLM pipeline.

---

## Directory Map

```
/
├── AGENTS.md                          # This file — read first
├── CLAUDE.md                          # Claude-specific operational rules
├── PROJECT.md                         # Product spec and build order
├── skills-lock.json                   # Installed skill manifest (auto-managed)
│
├── .claude/
│   └── skills/                        # Agent skills (SKILL.md only — no binaries)
│
├── ProjectSkills/
│   ├── README.md                      # Skill system overview
│   ├── skill-arsenal.md               # Global skill inventory
│   ├── dependency-map.md              # Skill and pipeline dependency graphs
│   ├── changelog.md                   # Skill version history
│   ├── templates/
│   │   ├── Global-Skill.md            # Template for global skills
│   │   └── Project-Skill.md           # Template for project-scoped skills
│   └── projects/
│       ├── SEARCHDNA/
│       │   └── SEARCHDNA-Skills.md
│       ├── Vault/
│       │   └── Vault-Skills.md
│       ├── NotchOS/
│       │   └── NotchOS-Skills.md
│       └── Vantage/
│           └── Vantage-Skills.md
│
└── lib/
    └── searchdna/                     # SEARCHDNA source (Phase 1+ work)
        ├── types.ts
        ├── cluster.ts
        └── probes/
            ├── trends.ts
            └── youtube.ts
```

---

## Source-of-Truth Files

| File | What it governs |
|------|----------------|
| `lib/searchdna/types.ts` | Canonical `DemandSignal` schema — never duplicated elsewhere |
| `skills-lock.json` | Installed skills, sources, and hashes — do not edit by hand |
| `ProjectSkills/skill-arsenal.md` | Global skill registry — update whenever a skill is added or removed |
| `PROJECT.md` | Product spec, data schema, roadmap, and build order |
| `AGENTS.md` | Architecture and engineering standards (this file) |

---

## Build Order

Follow this sequence strictly. Do not skip phases.

```
Phase 1 — Demand Discovery (free tier)
  1. lib/searchdna/types.ts          DemandSignal schema
  2. lib/searchdna/probes/trends.ts  TalorData Trends probe
  3. lib/searchdna/probes/youtube.ts Consumption probe (wraps CIE-1 ingest)

Phase 2 — Demand Intelligence (paid tier)
  4. lib/searchdna/probes/serp.ts    TalorData SERP probe (same API key)
  5. lib/searchdna/cluster.ts        Topic clustering engine

Phase 3 — UI
  6. SearchDnaPage.tsx               Flat nav at /searchdna

Phase 4 — Market Layer
  7. Reddit, TikTok, Amazon, Reviews, Support ticket probes
```

---

## Coding Standards

### TypeScript Rules

- Strict mode always (`"strict": true`). No `any`, no `@ts-ignore` without a comment explaining why.
- Deserialise at the boundary. Raw API responses become typed objects immediately on ingestion.
- Serialise late. Internal code passes typed objects, never plain dicts.
- Subclass shared models from `lib/searchdna/types.ts`. Never re-declare the `DemandSignal` shape.
- Interfaces for external contracts, types for internal unions.
- No barrel re-exports unless the module is a public package boundary.

### Shared Typing Strategy

All probe outputs conform to `DemandSignal` (see `PROJECT.md`).
The clustering engine consumes `DemandSignal[]` and emits `DemandCluster[]` (defined in `types.ts`).
The UI layer reads only from the cluster output — it never calls probes directly.

### Naming Conventions

| Layer | Convention | Example |
|-------|-----------|---------|
| Files | kebab-case | `trends-probe.ts` |
| Types/Interfaces | PascalCase | `DemandSignal` |
| Functions | camelCase | `fetchTrendSignals` |
| Constants | SCREAMING_SNAKE | `TALORDATA_BASE_URL` |
| env vars | `STIRLING_*` prefix for engine vars | `STIRLING_TALORDATA_KEY` |

---

## LLM Architecture

LLM components (if introduced) must follow the narrow-contract pattern:

```
Input (typed Pydantic / Zod schema)
  → LLM call (reasoning for complex outputs only, not deterministic glue)
  → Output (typed schema — impossible to instantiate incorrectly)
```

- Use LLMs for signal classification, gap scoring, and cluster labelling.
- Do not use LLMs for data fetching, parsing, or schema validation.
- Each LLM step is a pure function: same input → deterministic schema shape, even if content varies.
- Store prompt templates in `lib/searchdna/prompts/` as `.ts` files, not inline strings.

---

## Adapter Architecture

Each data source is an adapter implementing the `ProbeAdapter` interface (defined in `types.ts`):

```typescript
interface ProbeAdapter {
  fetch(query: string): Promise<DemandSignal[]>
}
```

Adapters are stateless. Credentials are injected via `secureStore`. Never hardcode keys.

---

## Provider Boundaries

| Capability | Provider | Key storage |
|-----------|----------|-------------|
| Trends + SERP | TalorData (`talordata.com`) | `secureStore('talordata-key')` |
| Video consumption | YouTube Data API | `secureStore('youtube-key')` |
| PDF ingestion (future) | Stirling-PDF (self-hosted) | internal service URL |
| LLM inference | Anthropic Claude | `secureStore('anthropic-key')` |

Never call a provider not listed here without updating this table first.

### OmniRoute Integration Status

**Status: Evaluating — not part of the required development path.**

OmniRoute may provide provider routing, resilience, usage telemetry, and prompt compression
when an agent client is explicitly configured to send requests through a persistent OmniRoute
deployment. The installed OmniRoute Agent Skills (`omni-compression`, `omni-context-rtk`,
`omni-resilience`, `omni-inference`) are **reference documentation only**. They do not
activate routing or compression by themselves.

Do not assume OmniRoute is available from environment variables alone. Client base-URL,
authentication, streaming, tool-call, and provider compatibility must be validated for the
exact execution environment.

Before enabling OmniRoute for any production development session:

1. Deploy to a persistent private endpoint and test in an isolated session.
2. Confirm tool-call and streaming compatibility against an unproxied baseline.
3. Measure actual token savings — run the same tool-heavy task both ways and compare
   input tokens, output quality, missing diagnostic details, and latency.
4. Verify that compression preserves errors, diffs, test failures, and other actionable output.
5. Deliberately trigger a provider failure and confirm fallback does not break tool calls or streaming.
6. Review credential storage, logging, retention, and exposure of repository content that
   passes through the hosted gateway.
7. Confirm the exact routing, compression, and cost headers (`X-OmniRoute-*`).
8. Record the approved endpoint and client-specific configuration separately from this file.

Until all eight steps are validated and recorded, agents must not treat OmniRoute as a
required dependency or claim that its Agent Skills provide active compression.

---

## Validation Commands

Run these before every PR. Adapt as the project gains a build system.

```bash
task check          # Full quality gate (lint + type-check + tests)
task lint           # ESLint
task type-check     # tsc --noEmit
task test           # Unit tests
task format         # Prettier
```

Until a Taskfile exists, use equivalent `npx` or `pnpm` commands.

---

## Testing Philosophy

- Unit-test every probe adapter with a mocked HTTP response.
- Unit-test the clustering engine with synthetic `DemandSignal[]` fixtures.
- Do not test framework internals — only the behaviour this codebase owns.
- Fixtures live in `lib/searchdna/__fixtures__/`.
- Tests live beside the file they test: `trends.test.ts` next to `trends.ts`.

---

## Security Rules

- No secrets in source code or committed files. Use `secureStore`.
- No `console.log` of request payloads in production paths.
- All user-facing inputs validated at the boundary before entering the system.
- Dependencies pinned to exact versions in `package.json`. Review diffs on upgrades.
- Run `task security` (or equivalent) before merging any dependency change.

---

## Performance Expectations

- Individual probe calls must complete within 5 s under normal load.
- The clustering engine must handle 10,000 signals without blocking the event loop (use workers or streaming aggregation).
- The UI must not crash on PDFs or data sets up to 100 MB.
- No synchronous file I/O in any probe or clustering path.

---

## Error-Handling Conventions

- Probes catch and wrap provider errors into a typed `ProbeError` with `source`, `query`, and `cause`.
- The clustering engine never throws — it returns `{ clusters, errors }` so partial results are usable.
- UI errors surface via a `<DemandErrorBoundary>` component, never a raw JS crash.
- All unhandled promise rejections must be caught at the probe call site.

---

## Documentation Requirements

- Public interfaces in `types.ts` get a one-line JSDoc comment explaining purpose, not shape.
- Probe adapters get a comment explaining the data source and any known limitations.
- Everything else: no comments unless the WHY is non-obvious.
- No multi-paragraph docstrings. No "added for X" notes — those belong in the PR description.

---

## Communication and Reporting Format

When an agent reports work:

```
What changed: <one sentence>
Why: <one sentence if non-obvious>
Next: <one sentence or "nothing — done">
Blockers: <one sentence or omit>
```

Do not narrate tool calls. Do not explain what code does. Report results and decisions only.

---

## Definition of Done

A task is done when ALL of the following are true:

- [ ] Types defined in `types.ts` (if the task introduces new data shapes)
- [ ] Implementation matches the build order in `PROJECT.md`
- [ ] `task check` passes (or equivalent lint + type-check)
- [ ] At least one unit test covers the happy path
- [ ] `ProjectSkills/skill-arsenal.md` updated if a skill was added or removed
- [ ] PR description explains the why, not the what
- [ ] No secrets, no `any`, no `@ts-ignore` without comment

---

## Scope Boundaries

**In scope for SEARCHDNA Phase 1:**
TalorData Trends probe, YouTube consumption probe, `DemandSignal` schema.

**Out of scope until explicitly unlocked:**
- SERP probe (Phase 2)
- Clustering engine (Phase 2)
- UI (Phase 3)
- Reddit / TikTok / Amazon probes (Phase 4)
- GEO visibility scoring (Phase 2, inside SEARCHDNA)
- Any other project (Vault, NotchOS, Vantage)

Do not implement out-of-scope items speculatively.

---

## Project Roadmap References

| Phase | Reference |
|-------|-----------|
| SEARCHDNA build order | `PROJECT.md` → Build Order |
| GEO positioning | `PROJECT.md` → GEO Position |
| Probe data schema | `PROJECT.md` → Data Schema |
| Skill inventory | `ProjectSkills/skill-arsenal.md` |
| Skill dependencies | `ProjectSkills/dependency-map.md` |

---

## Files Every Agent Must Read Before Changing Code

1. `AGENTS.md` — this file
2. `PROJECT.md` — product spec and build order
3. `lib/searchdna/types.ts` — canonical schema (once it exists)
4. `ProjectSkills/projects/SEARCHDNA/SEARCHDNA-Skills.md` — active skills for this project
5. The `SKILL.md` of any skill being invoked
