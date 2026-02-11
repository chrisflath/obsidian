# 1v1 Falsification Test

Part of [[aoeFamiliarity Project]] | Identification Test

**Script:** `id_solo_falsification.py`

## Logic

If TPE truly captures **coordination** skill, it should have minimal predictive power in **solo (1v1) games** where no coordination is needed. Any 1v1 effect represents individual skill "spillover" -- the floor of TPE that reflects unmeasured individual ability rather than team coordination.

## Model

```
1v1_win ~ selo_diff + tpe_diff + controls
```

## Results by Map Class

| Map Class | N (1v1) | TPE Coefficient | as % of Team Elo |
|-----------|---------|-----------------|-----------------|
| **Open** | 782K | 0.252*** | 14.8% |
| Closed | 132K | 0.305*** | 18.0% |
| **Nomad** | 29K | 0.737*** | 45.7% |

## Interpretation

- **Open maps (Arabia):** Clean 14.8% floor -- this is the baseline individual skill spillover
- **Closed maps:** Slightly higher (18%), plausibly because strategic planning (a component of TPE) also helps in solo defensive play
- **Nomad:** Anomalously high 45.7% -- see [[Nomad Anomaly]]

## Recommended Use

Use the **Open map floor (14.8%)** as the primary identification benchmark.

**Coordination component** = Team TPE effect minus 1v1 floor = roughly **10-12 percentage points** of pure coordination.

## Additional Context

TPE adds only **~2% R-squared** in 1v1 models, compared to the substantial contribution in team games. Most 1v1 variation is explained by Solo Elo (Team Elo), confirming that TPE's value is overwhelmingly team-specific.
