# Nomad Anomaly

Part of [[aoeFamiliarity Project]] | See also: [[1v1 Falsification Test]], [[Map Type Effects]]

## The Problem

In the [[1v1 Falsification Test]], the TPE coefficient on Nomad maps is anomalously high:

| Map Class | 1v1 TPE Coefficient | as % of Team Elo |
|-----------|--------------------|--------------------|
| Open | 0.252 | 14.8% |
| Closed | 0.305 | 18.0% |
| **Nomad** | **0.737** | **45.7%** |

A 45.7% spillover to 1v1 is too high to be a simple "floor" -- it suggests confounding.

## Root Cause Analysis

The upstream TPE estimation (Stage 1 of [[Three-Stage Pipeline]]) was estimated **without map fixed effects**. This means:

1. Players who **specialize on Nomad** develop Nomad-specific skills
2. These skills inflate their gamma coefficient in the upstream model
3. When tested on 1v1 Nomad, these map-specific skills predict 1v1 wins
4. This is **confounding**, not true coordination spillover

## Mechanism

```
Nomad specialization -> Higher gamma (upstream) -> Higher TPE
                    -> Better 1v1 Nomad performance

The correlation is through map-specific skill, not coordination
```

## Recommendations

1. Use **Open map floor (14.8%)** as the primary identification benchmark
2. Consider adding categorical map dummies to the upstream model in a future re-estimation
3. Acknowledge Nomad as a limitation in the manuscript
4. The Nomad anomaly actually *strengthens* the Open map result by contrast

## Current Status

Documented in `NOMAD_ANOMALY_ANALYSIS.md`. Listed as technical debt for potential future TPE re-estimation with map fixed effects.
