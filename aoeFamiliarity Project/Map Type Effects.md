# Map Type Effects

Part of [[aoeFamiliarity Project]] | Heterogeneity Analysis

**Script:** `het_map_types.py`

## Map Classification

| Class | Example Maps | Strategic Character |
|-------|-------------|---------------------|
| **Open** | Arabia, Steppe, Runestones | Individual mechanical execution dominates |
| **Closed** | Arena, Black Forest, Hideout | Coordinated timing attacks, defensive play |
| **Nomad** | Nomad, Land Nomad | Early adaptation, no starting TC, high uncertainty |

## Results

| Map Class | N | Solo Elo | TPE | TPE/Selo | vs Open |
|-----------|---|----------|-----|----------|---------|
| **Open** | 3.1M | 0.857 | 0.403 | 0.470 | baseline |
| **Nomad** | 1.6M | 0.591 | 0.371 | 0.628 | +33.8% |
| **Closed** | 2.9M | 0.538 | 0.366 | 0.680 | +44.7% |

## Interpretation

**Ranking by TPE importance:** Closed (0.680) > Nomad (0.628) > Open (0.470)

- **Open maps** favor individual mechanical execution (fast aggression, micro skills)
- **Closed maps** require coordinated timing attacks and strategic planning -- TPE matters **45% more** than on open maps
- **Nomad** requires early coordination (finding each other, establishing base together) but eventually strategic play

This gradient validates that TPE captures genuine coordination value: it matters most when the task structure demands synchronization.

## Connection to Organizational Theory

This mirrors findings in organizational science: coordination costs are higher for complex, interdependent tasks. Open maps approximate "pooled interdependence" (individuals contribute separately) while closed maps approximate "reciprocal interdependence" (requires mutual adjustment).

## Caveat: Nomad Anomaly

See [[Nomad Anomaly]] for a discussion of the elevated 1v1 TPE spillover on Nomad maps, which suggests map-specific skill confounding in the upstream estimation.
