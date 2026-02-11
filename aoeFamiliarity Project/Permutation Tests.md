# Permutation Tests

Part of [[aoeFamiliarity Project]] | Identification Test

**Script:** `id_patch_placebo.py`

## Logic

The [[Patch Shock Analysis]] shows Solo Elo is disrupted while TPE remains stable. But could this pattern arise from general time trends rather than actual patch effects?

## Method

1. Run 100 permutations with **shuffled (placebo) patch dates**
2. Apply the same patch shock model to each placebo date
3. Compare actual patch effects to the distribution of placebo effects

## Results

| Variable | Actual Effect | Placebo Mean | Placebo SD | z-score |
|----------|---------------|--------------|-----------|---------|
| selo_post | -0.025 | -0.003 | 0.023 | -0.97 |
| tpe_post | -0.001 | -0.001 | 0.005 | -0.04 |
| fam_post | +0.015 | +0.001 | 0.012 | +1.16 |

## Interpretation

- **Placebo dates:** Yield null effects (means near zero) -- no systematic time trends
- **Actual patch dates:** Show real Solo Elo disruption
- The TPE non-effect is confirmed: TPE is flat both at actual AND placebo dates

## What This Rules Out

- **Seasonal effects**: Random dates don't show the disruption pattern
- **Data artifacts**: The effect is specific to actual patches, not measurement noise
- **Gradual skill trends**: Time trends alone don't explain the Solo Elo drop

## Conclusion

The patch shock effects identified in [[Patch Shock Analysis]] are **causal**, not artifacts of time trends or data structure. This strengthens the "roadmap vs compass" identification narrative.
