# Two-Rating Decomposition

## Motivation

Standard chess rating confounds general skill with preparation capital. Players with extensive opening preparation have inflated standard ratings relative to their "raw" ability. Chess960 rating reflects skill without prep.

By including **both** ratings, we can separate these components.

## Model

```
Y_g = beta * is_960
    + theta1 * R_std_z
    + theta2 * R_960_z
    + theta3 * (R_std_z x is_960)
    + theta4 * (R_960_z x is_960)
    + u_i + epsilon
```

## Predictions

| Coefficient | Meaning | Prediction | Finding |
|-------------|---------|------------|---------|
| theta1 | R_std effect in standard | < 0 (better players err less) | -0.208*** |
| theta3 | R_std x 960 interaction | > 0 (std rating less predictive in 960) | **+0.050***** |
| theta2 | R_960 effect in standard | < 0 | +0.022 (n.s.) |
| theta4 | R_960 x 960 interaction | <= 0 (960 rating more predictive in 960) | **-0.035***** |

## Key Result: theta3

**theta3 = +0.050**** means: a 1 SD increase in standard rating predicts 0.05 *less* improvement in Chess960 than in standard. The prep component of standard rating loses predictive power when prep is disabled.

## Phase Gradient

theta3 is **opening-specific** — it vanishes in later phases:

| Phase | theta3 | p-value |
|-------|--------|---------|
| Opening (1-12) | +0.050 | *** |
| Middlegame (13-25) | +0.005 | n.s. |
| Endgame (26+) | -0.007 | n.s. |

This is a strong specificity test: prep capital should only matter where templates apply.

## Robustness

| Rating source | theta3 |
|---------------|--------|
| API rating (primary) | +0.050*** |
| PGN median | +0.101*** |
| PGN first-observed | +0.029*** |

## Chess.com Elite Replication (N=5,182 games, 252 players)

Adapted for chess.com Freestyle Friday (960 blitz 3+1) vs Titled Tuesday (standard blitz 3+1).

### Theta3 Range Restriction

Chess.com R_std SD=240 vs Lichess SD=435 (1.8x less variance). The elite sample is too homogeneous in standard skill for between-player theta3 detection.

| Model | theta3 | p |
|-------|--------|---|
| API ratings (R_std from `/stats`) | -0.004 | 0.60 (NULL) |
| In-game ratings (WhiteElo/BlackElo) | +0.019 | 0.034* |
| Prep rent (R_std - R_960) | +0.006 | 0.12 (directional) |

> [!important] Partial replication
> theta3 is null with API ratings due to range restriction. Using in-game ratings (which vary game-to-game) recovers a significant positive interaction (+0.019*, p=0.034). The prep rent correlation is directionally correct but underpowered.

### Phase Gradient (chess.com)

| Phase | theta4 (R_960 × 960) | p |
|-------|----------------------|---|
| Opening (1-12) | n.s. | — |
| Middlegame (13-25) | -0.030 | ** |
| Endgame (26+) | -0.060 | ** |

The chess.com phase gradient is inverted vs Lichess — theta4 (960 rating advantage in 960) strengthens in later phases. This may reflect elite 960 specialists having middlegame/endgame edges, while the opening is equalized by Freestyle Friday experience.

### Format Gap

| | Chess.com | Lichess |
|--|-----------|---------|
| β (format gap) | +0.290*** | +0.176*** |
| Ratio | 1.65x larger | baseline |

See also: [[Research Design]], [[Key Results]], [[Random Slopes & BLUPs]], [[Skill Decomposition — Cross-Project Bridge]], [[Gelbach Decomposition]]

**Script**: `analysis/two_rating_decomposition.py` (adapted inline for chess.com)

#chess960 #methods #identification
