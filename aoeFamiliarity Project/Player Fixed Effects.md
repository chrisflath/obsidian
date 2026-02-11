# Player Fixed Effects

Part of [[aoeFamiliarity Project]] | Identification Test

**Script:** `id_robustness.py` (S6 specification)

## Logic

Can we isolate the effect of a **teammate's** coordination skill on MY outcomes, after absorbing all of MY individual unobservables?

## Model

```
teammate_1v1_outcome ~ my_player_FE + teammate_TPE + controls
```

By including player fixed effects for the focal player, we absorb all time-invariant individual characteristics (skill, experience, play style, etc.).

## Result

**Teammate TPE coefficient = 0.078*** (highly significant)**

## Interpretation

After absorbing everything about ME (via fixed effects):
- My teammate's TPE still predicts whether **I** win
- This can only work through a **team synergy mechanism** -- teammate coordination skill genuinely helps the team
- It rules out the interpretation that TPE simply captures unmeasured individual ability

## Why This Is Powerful

1. Player FE absorb any individual-level confounder (measured or unmeasured)
2. The remaining TPE effect must operate through the **team channel**
3. This is the closest the design comes to a "within-person" causal estimate

## Effect Size Context

- Teammate FE estimate: 0.078
- Full sample estimate: 0.192
- Ratio: 0.41

The FE estimate is smaller than the full sample, which is expected: some of the full-sample TPE effect includes individual skill correlation that the FE model absorbs. The surviving 0.078 represents a conservative lower bound on the true team coordination effect.
