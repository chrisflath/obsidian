# Skill Tier Effects

Part of [[aoeFamiliarity Project]] | Heterogeneity Analysis

**Scripts:** `het_skill_tiers.py`, `het_skill_variance.py`

## U-Shape Finding (Within-Tier Standardization)

| Elo Tier | N | Selo Coef | TPE Coef | TPE/Selo |
|----------|---|-----------|----------|----------|
| Q1 (Low, <1200) | 400K | 0.312 | 0.208 | 0.67 |
| Q2 (1200-1400) | 400K | 0.130 | 0.170 | 1.31 |
| Q3 (1400-1600) | 400K | 0.124 | 0.164 | 1.32 |
| Q4 (High, >1600) | 400K | 0.267 | 0.236 | 0.88 |

The Solo Elo coefficient shows a **U-shape**: high at extremes, low in the middle. TPE is relatively stable across tiers but slightly higher at the extremes.

## Mechanism: Within-Tier Variance (S7d)

| Tier | Within-Tier Selo SD |
|------|---------------------|
| Q1 | 0.63 |
| Q2 | 0.17 |
| Q3 | 0.17 |
| Q4 | 0.63 |

**Correlation:** Selo SD <-> Selo coefficient = r = 0.98 (p = 0.019)

**Interpretation:** At mid-Elo (Q2, Q3), players are mechanically similar (4x lower skill variance). When individual skills converge, coordination becomes the **dominant differentiator** -- hence TPE/Selo ratio peaks above 1.0 at mid-Elo.

At the extremes (Q1, Q4), there is wider skill variation, so individual skill differences explain more of the outcome.

## Alternative View: Global Standardization (S7b)

With global (rather than within-tier) standardization, the pattern inverts to an inverted-V shape. Both perspectives are valid but reveal different aspects:
- **Within-tier:** "Given players of similar skill, does coordination matter more?"
- **Global:** "Across the full skill distribution, where does skill matter most?"

## Connection to [[TPE-Familiarity Complementarity]]

The triple interaction analysis (S7c) shows that TPE x Familiarity complementarity is **strongest at Q4 (High-Elo)**: 0.040 vs 0.021 at Q1. At high skill levels where margins are tightest, teammate-specific learning has the highest ROI.
