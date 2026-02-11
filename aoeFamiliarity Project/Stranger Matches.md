# Stranger Matches

Part of [[aoeFamiliarity Project]] | Identification Test

**Script:** `id_stranger_matches.py`

## Logic

If TPE captures an **intrinsic** coordination trait (rather than learned synergy with specific teammates), it should predict wins even when players are matched with **complete strangers**.

## Method

Stratify the sample by familiarity levels and run the downstream regression within each stratum.

## Results

| Familiarity Level | N | TPE Coef | Fam Coef | TPE vs Full |
|------------------|---|----------|----------|-------------|
| Full Sample | 1,602,812 | 0.192 | 0.102 | baseline |
| Bottom 25% | 400,705 | 0.160 | 0.033 | 0.834 |
| **Bottom 10% (Strangers)** | **160,317** | **0.131** | **0.026** | **0.682** |

## Interpretation

Even among **strangers** (bottom 10% familiarity -- effectively zero prior shared experience):
- TPE still significantly predicts win probability (coef = 0.131)
- This is 68% of the full-sample effect
- Familiarity coefficient drops dramatically (0.026 vs 0.102), as expected

## What This Rules Out

- **"Learned synergy" hypothesis**: If TPE only worked because of teammate-specific practice, it would be zero for strangers
- **"Selection bias" hypothesis**: Strangers are quasi-randomly matched, ruling out systematic partner selection

## What This Supports

TPE captures a **portable, intrinsic coordination ability** -- some people are simply better at coordinating with *anyone*, not just practiced teammates. This is consistent with the "compass" metaphor: the skill works regardless of the specific team context.

The remaining ~32% gap (0.131 vs 0.192) likely reflects the genuine amplification of coordination through familiarity -- see [[TPE-Familiarity Complementarity]].
