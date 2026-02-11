# Calibration and Model Quality

Part of [[aoeFamiliarity Project]] | Sensitivity Analysis (S5)

## Brier Score Comparison

| Metric | Baseline (Selo + Fam) | Full (Selo + TPE + Fam) | Improvement |
|--------|----------------------|------------------------|-------------|
| Brier Score | 0.2285 | 0.2266 | 0.80% |
| Skill Score | 0.086 | 0.093 | Better |
| ECE | 0.0097 | 0.0075 | Well-calibrated |

## Interpretation

- **Brier Score** (lower is better): Adding TPE improves prediction by 0.80% -- modest but consistent
- **Expected Calibration Error (ECE)**: 0.0075 means predicted probabilities closely match observed frequencies -- the model is well-calibrated
- **Skill Score**: Improvement over climatological baseline (50/50 prediction)

## Why the Improvement Seems Small

A 0.80% improvement in Brier Score is actually meaningful in this context:
1. Win prediction is inherently noisy (many random factors in each game)
2. Solo Elo already captures the majority of predictable variation
3. TPE adds **systematic** predictive power in the tails (mismatched teams)
4. The improvement is concentrated in games where TPE differences are largest

## Connection to Effect Sizes

The modest Brier improvement does not contradict the substantial [[Effect Sizes Summary]]. A 4.4 pp win probability shift per 1 SD TPE is large in practice, but Brier Score averages over all matches, including the many where TPE differences are small.

## Calibration Plot

The model's predicted win probabilities closely track actual win rates across all deciles, confirming that the logistic regression is appropriately specified.
