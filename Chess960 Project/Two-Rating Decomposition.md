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

See also: [[Research Design]], [[Key Results]], [[Random Slopes & BLUPs]], [[Skill Decomposition — Cross-Project Bridge]]

**Script**: `analysis/two_rating_decomposition.py`

#chess960 #methods #identification
