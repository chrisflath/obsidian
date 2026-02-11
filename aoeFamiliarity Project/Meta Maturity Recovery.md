# Meta Maturity Recovery

Part of [[aoeFamiliarity Project]] | Identification Test

**Script:** `id_patch_recovery.py`

## Logic

After a patch disrupts the meta, Solo Elo predictive power should **recover** as players re-learn the new meta. TPE, being transferable, should show **no recovery pattern** (it was never disrupted).

## Model

```
win ~ selo + tpe + fam + log_days + selo*log_days + tpe*log_days + fam*log_days
```

Where `log_days` = log(days since last major patch).

## Results

| Predictor | Interaction with log(days) | p-value |
|-----------|---------------------------|---------|
| **Solo Elo** | +0.0068 | <0.001 |
| **TPE** | +0.0002 | 0.913 |

## Interpretation

- **Solo Elo x log(days): +0.0068***  -- Solo Elo predictive power **recovers** as the meta stabilizes (positive interaction). Players gradually re-learn optimal strategies.
- **TPE x log(days): +0.0002 (NS)** -- TPE remains **flat** regardless of meta age. It was never disrupted, so there's nothing to recover.

## Connection to Patch Shocks

This completes the [[Patch Shock Analysis]] narrative:
1. **Immediately post-patch:** Solo Elo drops, TPE stable
2. **Over time:** Solo Elo recovers, TPE still stable
3. **Pattern:** Solo Elo follows a disruption-recovery cycle; TPE shows no cycle

This differential temporal dynamic is strong evidence that the two constructs measure fundamentally different things.

## "Learning Curve" Interpretation

The recovery curve (log-linear in days) suggests diminishing returns to re-learning: initial adjustment is fast, then gradually slows. This is consistent with a standard learning curve model.
