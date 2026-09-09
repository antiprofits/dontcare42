## SEARCHDNA Module Spec

### What it is
A Demand Intelligence platform. Not a keyword tool.

### Atomic Unit
A Demand Signal — any observable evidence that a human is expressing intent, curiosity, pain, desire, comparison, or purchase interest.

### Core Metrics
- Demand Intensity — how much does the market care?
- Demand Velocity — how fast is demand growing or declining?
- Demand Gap — how much demand exists relative to available content/solutions?
- Demand Capture — how much of that demand does a brand currently own?

### GEO Position
GEO is a feature inside SEARCHDNA (Phase 2), not a peer module. It measures AI Visibility as one slice of Demand Capture.

### Data Schema
```typescript
type DemandSignal = {
  source: 'google_trends' | 'youtube' | 'talordata_serp'
  query: string
  topicId?: string
  signalType: 'search_intent' | 'consumption' | 'capture'
  intensity: number
  velocity?: number
  timestamp: Date
  metadata: Record<string, unknown>
}
```

## Probe Roadmap

Phase 1 — Demand Discovery (free):

- TalorData Trends endpoint (1k free responses)
- YouTube consumption signals (reuse CIE-1 ingest layer)

Phase 2 — Demand Intelligence (paid):

- TalorData SERP endpoint (same API key, same integration)
- Absolute search volume, PAA signals, related queries

Phase 3 — Market Layer:

- Reddit, TikTok, Amazon, Reviews, Support tickets

## Nav

Flat nav item at /searchdna for now. Intelligence nav group (SEARCHDNA + GEO) added once both modules exist.

## Build Order

1. lib/searchdna/types.ts — DemandSignal schema
2. lib/searchdna/probes/trends.ts — TalorData Trends probe
3. lib/searchdna/probes/youtube.ts — consumption probe (wraps CIE-1)
4. lib/searchdna/cluster.ts — topic clustering engine
5. Wire to SearchDnaPage.tsx

## API

TalorData (talordata.com) — multi-engine SERP API. 1k free responses. Covers Trends + SERP in one integration. Replaces SerpAPI. Key stored via secureStore('talordata-key').
