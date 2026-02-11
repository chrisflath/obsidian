# Core Results

Part of [[aoeFamiliarity Project]] | See also: [[Effect Sizes Summary]], [[Key Variables]]

## Main Regression (Match-Level, N=1,602,812)

| Predictor | Coefficient | SE | z-score | p-value | Effect Size (1 SD) |
|-----------|------------|-----|---------|---------|-------------------|
| **Solo Elo** | 0.657 | 0.004 | 164.25 | <0.001 | +14.5 pp |
| **TPE** | 0.192 | 0.005 | 38.40 | <0.001 | +4.4 pp |
| **Familiarity** | 0.102 | 0.003 | 34.00 | <0.001 | +2.3 pp |

**Model:** `win ~ selo_diff + tpe_diff + fam_diff + controls`

## Key Takeaways

- Solo Elo is **3.4x** more important than TPE
- TPE is **1.9x** more important than Familiarity
- TPE effect is **~30%** of the Solo Elo effect
- All three predictors are **independently significant** (p < 0.001)
- A 1-SD increase in team TPE difference increases win probability by **4.4 percentage points**

## Practical Significance

In a match between two teams:
- Replacing a low-TPE player (bottom 25%) with a high-TPE player (top 25%) on an otherwise equal team shifts win probability by approximately **8-10 percentage points**
- This is roughly equivalent to a **~150 Elo point advantage** in individual skill

## Results by Team Size

See [[Team Size Effects]] for the full breakdown. Key pattern:
- Solo Elo importance **decreases** with team size (0.80 to 0.63)
- TPE importance remains **stable** across team sizes
- TPE/Selo ratio **increases** from 0.52 (2v2) to 0.60 (4v4)

## Model Quality

See [[Calibration and Model Quality]] for details.
- Brier Score improvement: 0.80% over baseline (Selo + Fam only)
- Expected Calibration Error: 0.0075 (well-calibrated)
