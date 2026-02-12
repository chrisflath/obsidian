# Error Composition

## Core Question

Does the Chess960 format gap come from catastrophic blunders or from missed optimization? Do players in unfamiliar territory shift to "don't lose" mode?

## Key Finding: Loss Aversion → Satisficing

Templates don't protect against catastrophes — basic tactical vision handles that. Templates help **optimize**: choosing the best move among several reasonable options.

**Error category distribution (moves 1-12, rapid, paired):**

| Category | Standard | Chess960 | 960/Std | Δ ppts |
|----------|----------|----------|---------|--------|
| Perfect (CPL=0) | 14.5% | 12.8% | 0.88x | -1.7 |
| Minor (1-20) | 43.6% | 32.5% | 0.75x | -11.1 |
| Inaccuracy (21-50) | 19.1% | 21.8% | 1.14x | +2.6 |
| Mistake (51-100) | 12.5% | 18.6% | 1.48x | +6.1 |
| Blunder (101-300) | 8.5% | 12.7% | 1.49x | +4.2 |
| Catastrophe (>300) | 1.7% | 1.7% | **0.97x** | 0.0 |

N: standard=618K, chess960=289K moves.

> [!important] Catastrophe rate is FLAT
> The is_960 coefficient on catastrophe rate = -0.0004 (p=0.60). Players avoid worst-case outcomes equally well in both formats. The gap comes entirely from the middle of the error distribution.

## CPL Gap Decomposition by Error Band

Where does the +10.8 CPL format gap come from?

| Category | Std contrib | 960 contrib | Δ | % of gap |
|----------|-------------|-------------|---|----------|
| Perfect (0) | 0.00 | 0.00 | 0.0 | 0% |
| Minor (1-20) | 3.50 | 3.05 | -0.45 | -4.1% |
| Inaccuracy (21-50) | 6.44 | 7.39 | +0.96 | +8.8% |
| Mistake (51-100) | 8.91 | 13.34 | **+4.43** | **+40.9%** |
| Blunder (101-300) | 13.49 | 19.75 | **+6.26** | **+57.8%** |
| Catastrophe (>300) | 7.69 | 7.32 | -0.37 | -3.4% |

~99% of the gap comes from mistakes (41%) and blunders (58%). Catastrophes contribute *negatively*.

## Forgiving vs Demanding Positions

The format gap exists only in **forgiving** positions (many good moves). In demanding positions, 960 players do *better*.

| Position type | Format gap | Catastrophe Δ | Story |
|---------------|------------|---------------|-------|
| Forgiving (sg≥0.5) | **+8.5 CPL** | -0.8 CPL | Templates help optimize |
| Demanding (sg<0.5) | **-2.5 CPL** | -7.1 CPL | 960 players MORE careful |

### Format × Complexity Interactions (clustered SEs)

| DV | is_960 | is_960 × share_good | Interpretation |
|----|--------|---------------------|----------------|
| Catastrophe | -0.0004 (p=.60) | +0.0046*** | Flat main effect |
| Blunder | +0.0411*** | +0.0014 (p=.54) | Uniform increase |
| Mistake | +0.0658*** | **+0.0221***  | Concentrated in forgiving |
| Inaccuracy | +0.0352*** | **+0.0115*** | Concentrated in forgiving |

## The Discrimination Story

In forgiving positions (sg≥0.5), what happens?

| Outcome | Standard | Chess960 | Δ |
|---------|----------|----------|---|
| Found best move (CPL=0) | 14.6% | 12.1% | -2.5pp*** |
| Settled for good (1-50) | 64.4% | 57.8% | -6.6pp*** |
| Mistake+ (>50) | 21.1% | 30.2% | **+9.1pp*** |

960 players don't just fail to find the best move — they fail to distinguish good from adequate. The regression confirms: is_960 → "settled for good enough" = -0.082*** (they settle LESS but mistake MORE).

## Within-960 Template Distance Gradient

Error composition shifts monotonically with template distance:

| Metric | Near | Medium | Far |
|--------|------|--------|-----|
| Mean CPL | 47.8 | 49.3 | 52.0 |
| Perfect rate | 13.3% | 13.2% | 12.5% |
| Blunder rate | 11.3% | 12.1% | 13.4% |
| Catastrophe rate | 1.5% | 1.5% | 1.6% |

Blunders increase with distance; catastrophes stay flat.

## Conditional Severity by Complexity

Given CPL > 0 (an error occurred), how severe is it?

| Position type | Standard | Chess960 | Δ |
|---------------|----------|----------|---|
| Low sg (<0.25) | mean=95.6 | mean=89.9 | **-5.7** (960 better) |
| Mid sg (0.25-0.75) | mean=68.8 | mean=70.9 | +2.1 |
| High sg (>0.75) | mean=37.1 | mean=45.7 | **+8.6** (960 worse) |

The severity reversal confirms: when positions are unambiguous (one best move), 960 players are *more careful*. When positions are forgiving, they lack template guidance.

## Within-Player Paired Tests (all p < .0001)

| Metric | Standard | Chess960 | Δ | t |
|--------|----------|----------|---|---|
| Blunder rate | 10.7% | 15.5% | +4.8pp | 18.8 |
| Mistake rate | 12.9% | 18.6% | +5.6pp | 23.8 |
| Inaccuracy rate | 19.6% | 21.5% | +1.9pp | 8.2 |
| Perfect rate | 14.2% | 12.3% | -1.9pp | -7.1 |

## Error Efficiency

| Format | Error rate | CPL per error | Mean CPL |
|--------|-----------|---------------|----------|
| Standard | 85.5% | 46.8 | 40.0 |
| Chess960 | 87.2% | 58.3 | 50.9 |

960 errors are **more costly** (+24.6% CPL/error). The error rate barely changes (+1.7pp), but each error is larger.

## Prospect Theory: The S-Curve

The format gap follows a **prospect-theory value function** when plotted against position evaluation (distance from reference point).

> [!important] Reference point = balanced position (eval ≈ 0)
> Templates define "normal." Near the reference point, templates guide optimization. Far from it, pure calculation dominates and templates become irrelevant — or even harmful.

### The Value Function (format gap by eval)

```
Eval range       Gap      Visual
(-500, -200]    -10.8     █████|          ← 960 BETTER
(-200, -100]     -3.2         █|
(-100, -50]      +4.2          |██
(-50, -25]       +9.1          |████
(-25, 0]        +12.1          |██████    ← PEAK
(0, 25]         +11.4          |█████
(25, 50]        +13.8          |██████    ← PEAK
(50, 100]       +10.2          |█████
(100, 200]       +0.0          |          ← VANISHES
(200, 500]      -11.0     █████|          ← 960 BETTER
```

### Formal Test: Quadratic Interaction (S-curve)

`log(CPL+1) ~ is_960 × eval_z + is_960 × eval_z² + elo_z + move_z` (N=887K, clustered SEs)

| Coefficient | Estimate | SE | p |
|-------------|----------|-----|---|
| is_960 | +0.433 | 0.018 | *** |
| is_960 × eval_z | **-0.024** | 0.004 | *** |
| is_960 × eval_z² | **-0.052** | 0.003 | *** |

Both the linear and quadratic interactions are negative and highly significant:
- **Linear** (−0.024): format gap shrinks as position becomes more extreme
- **Quadratic** (−0.052): gap narrows *faster* at extremes (concavity) — the S-curve

### Domain Split

| Domain | Format gap | Catastrophe Δ | Perfect Δ |
|--------|-----------|---------------|-----------|
| Winning (eval > 50) | +3.7 | -0.47pp | +0.14pp |
| Equal (±50) | **+13.6** | +0.07pp | **-1.77pp** |
| Losing (eval < -50) | **-2.8** | **-1.13pp** | **+1.35pp** |

When losing, 960 players: fewer catastrophes, MORE perfect moves, LOWER CPL. Without templates, they're in pure calculation mode — no template interference.

### Variance by Domain

| Domain | Std CPL var | 960 CPL var | Ratio |
|--------|------------|------------|-------|
| Winning | 7,212 | 6,288 | 0.87 |
| Equal | 2,494 | **3,211** | **1.29** |
| Losing | 10,389 | 8,674 | 0.84 |

At the reference point (equal), 960 has **higher** variance — consistent with ambiguity about the right move. At extremes, 960 has **lower** variance — more consistent play when templates aren't relevant.

### Time by Domain

| Domain | Std time | 960 time | 960/Std |
|--------|----------|----------|---------|
| Losing | 9.4s | 10.5s | 1.12x |
| Equal | 9.4s | 10.4s | 1.11x |
| Winning | 8.5s | 10.2s | **1.21x** |

960 players over-think most when WINNING — consistent with loss aversion: they have something to protect and don't trust their move choice without template guidance.

## Prospect Theory Mapping

| PT Concept | Chess Analog | Evidence |
|------------|-------------|----------|
| **Reference point** | Balanced position (eval ≈ 0) | Format gap peaks at reference, vanishes at extremes |
| **Loss aversion** (λ > 1) | Catastrophe avoidance > optimization pursuit | Catastrophe rate flat, perfect rate falls; gap is −1.77pp vs +0.07pp |
| **Diminishing sensitivity** | Gap shrinks with |eval| | is_960 × eval_z² = −0.052*** |
| **Reflection effect** | 960 better when losing | Gap reverses to −2.8 in loss domain |
| **Certainty effect** | Templates provide pseudo-certainty | Without templates → uncertainty → satisficing |
| **Anti-calibration** | Overweighted uncertainty at reference | Over-thinking easy positions ([[Time Mechanism]]) |

## Mechanism Story: Loss Aversion Under Uncertainty

1. **Templates define the reference point** — "I know what to do here" = equilibrium. Without templates, every position feels like it could be a loss.
2. Near the reference (balanced positions), templates help **optimize** among reasonable moves. Without them, loss aversion triggers satisficing → format gap peaks (+13.8 CPL).
3. **Diminishing sensitivity**: as positions become more extreme, templates lose relevance. What matters is pure calculation — and 960 players have no template interference.
4. **Reversal at extremes**: heavily winning/losing positions produce a *negative* format gap (−11 CPL). Templates may actually hurt here (overconfidence in "known" positions, pattern-matching that doesn't apply).
5. **Catastrophes are format-invariant** — asymmetric sensitivity means downside protection is preserved even without templates. The cost is entirely in missed optimization.
6. Links to **anti-calibration** ([[Time Mechanism]]): positions *feel* uncertain without templates → over-thinking easy positions. Time over-allocation is largest when winning (1.21x) — the domain with the most to protect.

## Scripts

- Analysis run inline (difficulty_rubric.py data loading + custom queries)

See also: [[Time Mechanism]], [[Complexity Analysis]], [[Key Results]]

#chess960 #mechanism #errors #risk #prospect-theory
