# Time Mechanism

## Core Question

Do Chess960 players fail to allocate thinking time appropriately because they lack templates to assess position difficulty?

## Caveat (Updated)

> [!warning] Standard clock coverage improved
> After clock backfill: time_spent coverage 85% std / 93% 960. clock_time_remaining: 99% std / 100% 960. Cross-format comparisons now well-powered.

## Key Finding: Anti-Calibration

Without templates, 960 players cannot tell which positions need more thought. They over-think easy positions and under-think hard ones.

**Within-player correlation(share_good, log_time):**

| Format | Mean r | Median r | N players | Direction |
|--------|--------|----------|-----------|-----------|
| Standard | -0.035 | -0.033 | 307 | Correct (harder → more time) |
| Chess960 | +0.046 | +0.039 | 302 | **Inverted** (easier → more time) |

Paired t-test: t = -11.8, p < .0001. The calibration difference is highly significant.

## Time Descriptives (moves 1-12, rapid, paired players)

| Metric | Standard | Chess960 | Diff |
|--------|----------|----------|------|
| Mean time/move (s) | 8.73 | 9.92 | +1.19 |
| Median time/move (s) | 4.00 | 5.00 | +1.00 |
| Mean log(time) | 1.44 | 1.71 | +0.27 |

960 players spend ~14% more time per move overall.

## Time-Complexity Calibration

DV = log(time_spent), player-clustered SEs. 357K moves.

| Predictor | Standard | Chess960 |
|-----------|----------|----------|
| share_good_z | +0.014 (n.s.) | +0.071*** |
| elo_z | -0.073* | -0.016 |
| move_z | +0.168*** | +0.118*** |
| R² | 0.030 | 0.014 |

**Formal interaction:** format × share_good → time = **+0.078*** (p < .001)**

Interpretation: In 960, players spend *more* time on *easy* positions (positive share_good → more time). The sign is inverted — they should spend more time on hard positions.

## Residual Time (after partialling out complexity)

| Format | Mean residual |
|--------|---------------|
| Standard | -0.149 |
| Chess960 | +0.135 |

960 players spend more time than position complexity warrants.

## Time Efficiency

DV = log(CPL+1), player-clustered SEs.

| Predictor | Standard | Chess960 |
|-----------|----------|----------|
| log_time | +0.131*** | +0.116*** |
| share_good_z | -0.060*** | -0.027*** |
| elo_z | -0.376*** | -0.347*** |
| move_z | +0.274*** | +0.115*** |

Time "buys" similar error reduction per unit in both formats, but the **deployment** is miscalibrated in 960.

## Earlier Results (Move-Level)

| Variable | Coefficient | p | Interpretation |
|----------|------------|---|----------------|
| format × relative_time | -0.084 | *** | 960 players LESS time-sensitive |
| format × clock_remaining | -0.002 | n.s. | No clock pressure interaction |

### Within-960 Quartiles

| Quartile | Mean CPL |
|----------|----------|
| Q1 (fast) | 2.85 |
| Q2 | 3.03 |
| Q3 | 3.16 |
| Q4 (slow) | 3.32 |

### Phase Split

| Phase | format × time | p |
|-------|--------------|---|
| Early opening (2-6) | -0.096 | *** |
| Late opening (7-12) | -0.025 | * |

## Extended Gelbach Decomposition (with complexity)

Move-level: 392K moves, 326 paired players. Player FE. **No post-treatment variables (time excluded).**

```
Format gap β_base = 0.437 → 100%

                          δ×γ      % gap   Running
─────────────────────────────────────────────────────
  Queen displacement    +0.042     +9.7%     90.3%
  Bishop displacement   +0.042     +9.5%     80.8%
  Rook displacement     +0.017     +3.8%     77.0%
  King displacement     +0.011     +2.6%     74.4%
  Knight displacement   -0.018     -4.1%     78.5%
  K-Q same color        +0.020     +4.5%     74.0%
  Lopsidedness          -0.009     -2.1%     76.0%
  Move number           -0.001     -0.3%     76.4%
  Position complexity   +0.005     +1.1%     75.3%
  Gap 1v2               -0.001     -0.1%     75.4%
  Legal moves           -0.043     -9.8%     84.9%
─────────────────────────────────────────────────────
  Residual (templates)  +0.372     85.2%

Grouped:
  Piece displacement:   +21.5%
  Structural:            +2.5%
  Move number:           -0.3%
  Position complexity:   -8.8%  ← SUPPRESSOR
  Residual:             +85.2%
```

> [!important] Complexity is a suppressor
> Position complexity explains -8.8% of the format gap — 960 positions are objectively slightly *easier*. The raw gap understates the template effect.

## Graded Transfer Slope Decomposition

Within-960 Gelbach: does complexity explain the template distance gradient?

```
Base slope (td → log CPL):  0.01229
Full slope (td | controls): 0.01244  (101.2% retained)

                  δ (td→ctrl)  γ (ctrl→cpl)  Contribution  % of slope
───────────────────────────────────────────────────────────────────────
share_good         -0.0083       -0.0458       +0.0004       +3.1%
complexity_1v2     +0.0004       -0.0526       -0.0000       -0.2%
num_legal_moves    -0.0063       +0.0750       -0.0005       -3.9%
move_number        -0.0004       +0.0809       -0.0000       -0.3%
───────────────────────────────────────────────────────────────────────
Total explained                                -0.0001       -1.2%
Residual (template)                            +0.0124      101.2%
```

## Graded Transfer by Move Number

| Move | N | td slope | p |
|------|---|----------|---|
| 1 | 20,012 | +0.0187 | <.001*** |
| 2 | 19,869 | +0.0042 | .200 |
| 3 | 19,713 | +0.0131 | <.001*** |
| 4-6 | ~58K | +0.0096–0.0105 | <.01** |
| 7-10 | ~75K | +0.0127–0.0162 | <.001*** |

Move 1 has the strongest gradient. No fade-out through move 10.

## Template Distance Index

Weighted piece displacement + structural feature, scaled 0-20:

```python
PIECE_WEIGHTS = {
    'delta_queen':   0.01031,   # Queen (1.00)
    'delta_bishops': 0.00671,   # Bishops (0.65)
    'delta_rooks':   0.00374,   # Rooks (0.36)
    'delta_king':    0.00178,   # King (0.17)
    'delta_knights': -0.00079,  # Knights (~0, negative)
}
KQ_WEIGHT = 0.01492  # K-Q same color (p=0.001)
```

- R² = 0.0055 (game-level), 88% more variance than file_distance
- Zero monotonicity violations across 10 bins
- Adding kq_same_color resolved non-monotonicity at td ~17.5

## Mechanism Story

1. Templates provide efficient **difficulty assessment** — players know which positions are tricky
2. Without templates (960), players cannot assess difficulty → **anti-calibrated time allocation**
3. They over-think easy positions and under-think hard ones
4. The binding constraint is **template knowledge** (85% residual), not computational difficulty (-8.8% suppressor)
5. Evidence is opening-specific and scales monotonically with template distance
6. Consequence: not catastrophic blunders but **missed optimization** — see [[Error Composition]]

## Scripts

- `analysis/difficulty_rubric.py` — Progressive model building, complexity models, move-level rubric, stratified analyses, time mechanism tightening
- `scripts/panel_b_dev.py` — Panel B development (template distance gradient figure)

See also: [[Complexity Analysis]], [[Key Results]], [[Analysis Pipeline]]

#chess960 #mechanism #time #complexity
