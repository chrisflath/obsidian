# Robustness Checks

From reviewer revision request. Script: `analysis/revision_analyses.py`.

## Item 2: Alternative DVs

Seven variants of the dependent variable, all showing consistent format effects:

1. Median CPL
2. Raw CPL (no log transform)
3. Blunder rate (CPL > 300)
4. Mistake rate (CPL > 100)
5. Inaccuracy rate (CPL > 50)
6. Best-move rate
7. Trimmed mean CPL (5th-95th)

## Item 4: Quarterly Stability

Format gap is stable across 2020-2024. No attenuation over time, including through the Chess960 popularization wave (post-COVID).

## Item 5: Barthelemy S(n) Complexity

Alternative position complexity measures:
- Barthelemy S(n) complexity
- Asymmetry A
- Both used as alternative covariates to `file_distance`
- Results consistent

## Item 6: FE vs RE Equivalence

Hausman-like comparison confirms that the random effects specification produces equivalent estimates to fixed effects. The RE assumption (random effects uncorrelated with regressors) holds because treatment is format-level, not player-level.

## Item 7: Experience Cohort Analysis

Players binned by total games played (1-300):
- Format gap is approximately **0.14 across all cohorts**
- No convergence with experience
- Players do not "learn away" the format gap

## Other Robustness

- **Move window**: moves 2-12 (excluding move 1) confirms results
- **Rating source**: PGN median, PGN first-observed, API rating — all consistent
- **SP-clustered SEs**: similar inference to player-clustered

See also: [[Key Results]], [[Research Design]]

#chess960 #robustness
