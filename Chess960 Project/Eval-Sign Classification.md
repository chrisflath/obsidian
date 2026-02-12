# Eval-Sign Classification

## Core Question

When players err, do they leave value on the table (missed optimization) or hand over the advantage entirely (game-changing error)?

Chess.com-style classification refined with eval context: **no eval flip** (staying ahead but suboptimal) vs **eval flip** (crossing from ≥0 to <0 from the player's perspective). N = 1,006,481 moves (moves 1–12, rapid, paired players).

## Rate Breakdown

| Category | Standard | Chess960 | Δ |
|----------|----------|----------|---|
| **Good moves** | | | |
| Best (CPL = 0) | 14.1% | 12.6% | -1.5pp |
| Good (0 < CPL < 50) | 62.5% | 53.8% | -8.6pp |
| **Inaccuracy (50–100)** | **12.9%** | **18.9%** | **+6.0pp** |
| └ No eval flip | 9.0% | 13.1% | +4.1pp |
| └ Eval flip (→ losing) | 3.9% | 5.8% | +1.8pp |
| **Mistake (100–300)** | **8.7%** | **12.9%** | **+4.2pp** |
| └ No eval flip | 5.7% | 7.4% | +1.7pp |
| └ Eval flip (→ losing) | 3.1% | 5.5% | +2.5pp |
| **Blunder (300+)** | **1.8%** | **1.7%** | **-0.1pp** |
| └ No eval flip | 0.9% | 0.7% | -0.1pp |
| └ Eval flip (→ losing) | 0.9% | 1.0% | +0.1pp |

## Totals by Flip Type

| | Standard | Chess960 | Δ |
|---|---|---|---|
| All errors (CPL ≥ 50) | 23.4% | 33.5% | +10.1pp |
| └ No eval flip | 15.5% | 21.2% | +5.7pp |
| └ Eval flip | 7.9% | 12.3% | +4.4pp |
| Flip share of errors | 33.7% | 36.7% | +3.0pp |

The flip share increases in 960 (36.7% vs 33.7%) — a higher proportion of 960 errors are game-changing rather than just leaving value on the table.

## CPL Gap Decomposition by Flip Type

Total gap = +10.6 CPL

| Category | Contribution | Share |
|----------|-------------|-------|
| Mistake (eval flip) | +3.89 | **36.6%** |
| Inaccuracy (no flip) | +2.94 | **27.7%** |
| Mistake (no flip) | +2.33 | 21.9% |
| Inaccuracy (eval flip) | +1.39 | 13.1% |
| Blunder (no flip) | -0.49 | -4.6% |
| Blunder (eval flip) | +0.12 | 1.1% |
| Good + Best | +0.44 | 4.2% |

> [!important] Largest single CPL contributor = mistakes that flip the eval (36.6%)
> 100-300 CPL errors where the player was doing fine but played something that handed the advantage to the opponent. Templates provide the "right idea" to avoid crossing into losing territory.

> [!note] No-flip errors (inaccuracy + mistake) together ≈ 50%
> The satisficing signature: you don't lose the game, you just leave value on the table.

## Key Asymmetries

**Mistakes show the sharpest split.** Standard no-flip/flip ratio is 5.7%/3.1% (≈2:1), but 960 is 7.4%/5.5% (≈4:3). The eval-flipping mistake rate nearly doubles — without familiar patterns, players don't just play slightly worse, they misjudge enough to hand over the advantage.

**Blunders are rock-steady** regardless of flip type: ~1.7-1.8% total, split roughly evenly. The catastrophic error rate is a player-level constant, not template-dependent.

**Inaccuracies are mostly no-flip** (~70%) in both formats — a 50-100 CPL error rarely flips evaluation entirely. The format gap here (+4.1pp no-flip) is the pure optimization loss.

## Flip Rate by Position Complexity

Controlling for objective difficulty (share_good bins):

| share_good bin | Std flip | 960 flip | Δ | Std err% | 960 err% | Δ err |
|---------------|----------|----------|---|----------|----------|-------|
| 0–0.25 (hard) | 38.0% | 39.6% | +1.5pp | 37.2% | 38.7% | +1.5pp |
| 0.25–0.5 | 34.2% | 37.1% | +3.0pp | 38.8% | 41.4% | +2.6pp |
| 0.5–0.75 | 32.8% | 37.1% | +4.3pp | 36.2% | 42.6% | +6.4pp |
| 0.75–1.0 (easy) | 35.2% | 40.1% | +4.9pp | 20.2% | 28.8% | +8.6pp |

Both the flip rate gap AND the error rate gap are largest in **easy positions** — exactly where templates matter most. Without templates, players navigate normal positions as if they were sharp. See [[Game Volatility]] for why this isn't objective position sharpness.

See also: [[Error Composition]], [[Game Volatility]], [[Error Contagion]], [[Reference-Point Clarity]]

#chess960 #mechanism #errors #classification
