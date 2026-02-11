# Random Slopes & BLUPs

## Purpose

Allow each player to have their own format gap (random slope on `is_960`), then correlate these player-level gaps with observable player characteristics.

## Model

```
Y_g = beta * is_960 + u_i + v_i * is_960 + epsilon
```

Where `v_i` is the player-specific deviation from the average format gap.

## Random Effects

- **N**: 297 players (with >= 5 games in each format)
- **Slope variance**: 0.0102
- **Correlation (intercept, slope)**: -0.610

The negative correlation means players who make fewer errors overall (low intercept) tend to have *larger* format gaps (more positive slope) — better players lose more from losing their prep.

## Second-Stage Correlations

BLUPs `b_Fi` (player's estimated format gap) correlated with:

| Predictor | r | p | Interpretation |
|-----------|---|---|----------------|
| `prep_rent` (R_std - R_960) | +0.229 | *** | High prep rent = larger format gap |
| `specialist_ratio` (R_960/R_std) | -0.287 | *** | 960 specialists have smaller gaps |
| `eco_hhi` | -0.215 | *** | Diverse opening repertoire = smaller gap |
| `experience_ratio` | -0.146 | * | More 960 experience = smaller gap |

## Key Insight

Players whose standard rating exceeds their 960 rating (high `prep_rent`) show the largest performance drops in Chess960. This is direct evidence that the format gap reflects preparation capital.

## Visualization

Figure 3 (`fig3_blup_scatter.pdf`) plots `b_Fi` against `prep_rent` with regression line.

See also: [[Two-Rating Decomposition]], [[Key Results]]

**Script**: `analysis/two_rating_decomposition.py`

#chess960 #methods #player-level
