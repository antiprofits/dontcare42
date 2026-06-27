---
name: searchdna-probe
description: "Demand signal extractor for SEARCHDNA. Probes a query or topic and emits a DemandSignal JSON record (intensity, velocity, source) to the current directory. Run before lib/searchdna/cluster.ts to seed topic clustering with fresh signals. Triggers on: demand signal, demand intensity, demand velocity, probe topic, search demand, what is the demand for."
user-invokable: false
---

# SearchDNA Probe: Demand Signal Extractor

## Purpose

Probes one query/topic against the active Phase 1/2 sources (TalorData Trends, YouTube consumption, TalorData SERP) and writes the result as a `DemandSignal` record, matching the schema in `PROJECT.md`. This is the seed step before clustering — `lib/searchdna/cluster.ts` consumes these records.

## Quick Reference

| Mode | Sources hit | Use when |
|---|---|---|
| full | Trends + YouTube + SERP (if key has SERP access) | building a real cluster |
| `--quick` | Trends only | fast sanity check on a single query |

## Process

1. Collect the query/topic and optional `topicId` from the user. If missing, ask for one example query (e.g. "best ergonomic keyboard").
2. Run the available probes in order: `lib/searchdna/probes/trends.ts`, then `lib/searchdna/probes/youtube.ts` (skip on `--quick`), then the TalorData SERP probe if Phase 2 key access exists.
3. Compute `intensity` from the raw signal volume and `velocity` from the delta against the prior window, when history exists.
4. Construct the output strictly against the `DemandSignal` type — do not invent fields outside `source`, `query`, `topicId`, `signalType`, `intensity`, `velocity`, `timestamp`, `metadata`.
5. Append the record to the day's signal log (one JSON object per line) rather than overwriting, so clustering can replay history.
6. Confirm with a one-line summary: query, intensity, velocity, source(s) hit.

## Limitations

- TalorData free tier caps at 1k responses — `--quick` mode exists to conserve quota during iteration.
- Sparse/niche queries may return zero signal from Trends; fall back to YouTube consumption alone and note it in `metadata`.
- Velocity is `undefined` on first probe of a topic — there is no prior window to diff against.
