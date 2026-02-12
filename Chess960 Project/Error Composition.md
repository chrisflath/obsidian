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

For a refined decomposition by eval-sign flip, see [[Eval-Sign Classification]].

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

960 players don't just fail to find the best move — they fail to distinguish good from adequate.

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

## Mechanism Story

1. **Reference-point clarity**: In standard chess, templates provide a salient reference ("I am on-book / plan-consistent"). In 960, the reference is ambiguous.
2. **Near parity** (|eval| < 50cp): templates help optimize among reasonable moves. Without them, satisficing → format gap peaks (+0.459 in log CPL).
3. **Diminishing sensitivity**: as positions become extreme, templates lose relevance. Pure calculation, and template interference fades.
4. **Reversal at extremes** (|eval| > 200cp): format effect vanishes. 960 players show lower CPL variance and fewer catastrophes when losing.
5. **Catastrophes are format-invariant** — downside protection preserved regardless of template availability.
6. **Time allocation** confirms: over-thinking most pronounced when winning (1.21x) — strongest loss aversion.
7. **Depth-free replication**: quadratic interaction (−0.035***) holds with num_legal_moves.

For the full S-curve and prospect theory mapping, see [[Reference-Point Clarity]].

## Related Notes

- [[Eval-Sign Classification]] — miss vs game-changing error decomposition, CPL gap by flip type
- [[Game Volatility]] — time to first error, eval sign changes, cascade model, sharpness analysis
- [[Error Contagion]] — transition matrix, contagion by ELO, capitalization rates
- [[Reference-Point Clarity]] — S-curve, prospect theory mapping, domain splits, volatility
- [[Time Mechanism]] — anti-calibration, time allocation
- [[Complexity Analysis]] — MultiPV complexity controls

## Scripts

- Analysis run inline (difficulty_rubric.py data loading + custom queries)

#chess960 #mechanism #errors #risk
