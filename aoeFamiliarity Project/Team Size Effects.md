# Team Size Effects

Part of [[aoeFamiliarity Project]] | Heterogeneity Analysis

**Script:** Part of downstream analysis and `id_coordination_gradient.py`

## Results by Mode

| Mode | N | Solo Elo Coef | TPE Coef | TPE/Selo |
|------|---|---------------|----------|----------|
| 2v2 | 289,488 | 0.798 | 0.416 | 0.522 |
| 3v3 | 359,398 | 0.761 | 0.410 | 0.539 |
| 4v4 | 953,926 | 0.626 | 0.373 | 0.596 |

## Key Pattern

- Solo Elo coefficient **drops 21%** from 2v2 (0.80) to 4v4 (0.63)
- TPE coefficient is **relatively stable** across team sizes
- TPE/Selo ratio **increases** from 0.52 to 0.60

## Interpretation

As team size grows:
1. Individual skill gets **diluted** -- any one player's mechanical ability matters less
2. Coordination demands **increase** -- more teammates to synchronize with
3. The **relative importance** of coordination vs individual skill shifts toward coordination

This directly supports the theoretical prediction that coordination costs scale with team size, a core finding in organizational science.

## The Coordination Gradient

The gradient from 1v1 to 4v4 serves as an identification test (see [[Coordination Gradient]]):

| Mode | TPE Effect | Interpretation |
|------|-----------|----------------|
| 1v1 | ~5-15% | Floor (no coordination needed) |
| 2v2 | 0.416 | Minimal coordination |
| 3v3 | 0.410 | Moderate coordination |
| 4v4 | 0.373 | High coordination demand |

The jump from 1v1 to team games is the key validation: TPE matters dramatically more when teammates are present.
