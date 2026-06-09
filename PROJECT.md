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
