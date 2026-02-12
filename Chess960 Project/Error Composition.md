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

## Reference-Point Clarity and Prospect Theory

### The Construct: Reference-Point Clarity

In standard chess, opening templates provide a salient, shared reference — "I am on-book / plan-consistent" — which makes small deviations behaviorally meaningful. In Chess960, that reference is weaker; players face higher ambiguity about what "par" looks like, so they (i) satisfice more in slack states, and (ii) behave differently when already behind.

This is not a claim that players have subjective value functions over centipawns. It is a claim that **template availability modulates reference-point clarity**, which in turn mediates perceived stakes and decision strategy.

### The S-Curve (raw bins)

Format gap by pre-move evaluation (887K moves, eval clipped ±500):

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

### Formal Test: Piecewise-Linear Spline (Player FE)

`log(CPL+1) ~ is_960 × f(|eval|) + move_z + player FE` (N=887K, player-clustered SEs)

Knots at {25, 50, 100, 200} cp. Marginal format effect β(is_960 | |eval|) with 95% CI:

| |eval| (cp) | β_format | SE | 95% CI |
|-------------|----------|-----|--------|
| 0 | +0.407 | 0.026 | [+0.356, +0.457] |
| 25 | **+0.459** | 0.029 | [+0.403, +0.515] |
| 50 | +0.430 | 0.023 | [+0.385, +0.474] |
| 75 | +0.290 | 0.018 | [+0.254, +0.326] |
| 100 | +0.149 | 0.020 | [+0.109, +0.190] |
| 150 | +0.072 | 0.016 | [+0.040, +0.103] |
| 200 | -0.006 | 0.019 | [-0.042, +0.031] |
| 300 | -0.004 | 0.017 | [-0.037, +0.029] |

Format effect peaks at |eval| ≈ 25cp, decays monotonically, crosses zero at |eval| ≈ 200cp.

Key spline interactions (player FE, clustered SEs):
- `is_960 × sp_50` = **−0.444*** (gap accelerates downward 50-100cp)
- `is_960 × sp_100` = +0.406*** (deceleration after 100cp — floor reached)

### Domain Split with Player FE

`log(CPL+1) ~ is_960 × domain + move_z + player FE` (player-clustered SEs)

**Threshold ±50cp:**

| Domain | β(is_960) | SE | p | N |
|--------|-----------|-----|---|---|
| Equal (±50cp) | **+0.459** | 0.023 | *** | 438K |
| Winning (>50) | +0.233 | 0.018 | *** | 293K |
| Losing (<-50) | +0.140 | 0.018 | *** | 156K |

| Contrast | Estimate | SE | p |
|----------|----------|-----|---|
| Δ(winning − equal) | **−0.226** | 0.021 | *** |
| Δ(losing − equal) | **−0.319** | 0.022 | *** |

**Robustness (±25cp threshold):** Same ordering. Equal +0.440***, Winning +0.392***, Losing +0.229***. Δ(losing − equal) = −0.212***.

> [!note] All domains have β > 0 in log scale
> With player FE and log(CPL+1), the losing-domain coefficient is positive but much smaller. The raw CPL gap IS negative when losing (−2.8), because log compression dampens the tails. The key finding is the **ordering**: β(equal) >> β(winning) > β(losing).

### Move Volatility: Chess-Native Risk Proxy

Prospect theory's reflection effect concerns **variance/risk**, not just mean error. Using MultiPV data (422K moves):

**A) Within-player CPL variance by domain (paired t-tests):**

| Domain | Std var | 960 var | Paired t | p | N players |
|--------|---------|---------|----------|---|-----------|
| Winning | 5,328 | 6,133 | +2.86 | .005** | 283 |
| Equal | 2,749 | **3,429** | +4.98 | <.0001*** | 296 |
| Losing | 8,329 | 7,775 | −1.44 | .150 n.s. | 237 |

960 players are MORE erratic when winning/equal (no template guidance → inconsistent satisficing), but equally or LESS erratic when losing (forced into focused calculation).

**B) Position eval spread (sd of top-5 engine lines):**

`eval_spread_z ~ is_960 × is_losing + move_z + player FE` (player-clustered SEs, N=423K):

| Coefficient | Estimate | SE | p |
|-------------|----------|-----|---|
| is_960 | +0.031 | 0.007 | *** |
| is_losing | +0.267 | 0.012 | *** |
| **is_960 × losing** | **−0.141** | 0.014 | *** |

When losing, 960 positions have **lower** eval spread — consistent with 960 players navigating to positions with fewer wild tactical swings (risk-averse continuation choices, or simply that 960 losing positions are structurally less volatile).

**C) Time by domain:**

| Domain | Std time | 960 time | 960/Std |
|--------|----------|----------|---------|
| Losing | 9.4s | 10.5s | 1.12x |
| Equal | 9.4s | 10.4s | 1.11x |
| Winning | 8.5s | 10.2s | **1.21x** |

Over-thinking most pronounced when winning — the domain with the most to protect.

### Depth-Free Validity Check

> [!warning] Potential circularity
> If eval_before is derived from the same engine pipeline as CPL, the S-curve could be mechanical. Need a depth-free state proxy.

**num_legal_moves (fully depth-free):**

`log(CPL+1) ~ is_960 × legal_z + is_960 × legal_z² + move_z + player FE` (N=423K, clustered SEs):

| Coefficient | Estimate | SE | p |
|-------------|----------|-----|---|
| is_960 × legal_z | **−0.133** | 0.013 | *** |
| is_960 × legal_z² | **−0.035** | 0.004 | *** |

The **quadratic interaction replicates** with a completely depth-free proxy. Both linear and quadratic terms significant, confirming diminishing sensitivity is not an artifact of engine-depth circularity.

**share_good (engine-derived but independent of CPL computation):**

| Position type | Format gap |
|--------------|-----------|
| Hard (sg < 0.25) | **−2.8** |
| Moderate (0.25-0.5) | +4.6 |
| Easy (0.5-0.75) | +3.3 |
| Very easy (sg > 0.75) | **+8.3** |

Reproduces the same pattern: gap is negative in demanding positions, peaks in forgiving ones.

## Prospect Theory Mapping

| PT Concept | Operationalization | Evidence |
|------------|-------------------|----------|
| **Reference-point clarity** | Templates define "par" | Format gap peaks near equality, vanishes at extremes |
| **Loss aversion** | Downside protection > optimization pursuit | Catastrophe rate flat (p=.60), optimization sacrificed |
| **Diminishing sensitivity** | Gap shrinks with |eval| | Spline: β peaks at 25cp, zero by 200cp. Quadratic: −0.052*** |
| **Reflection** | Different behavior below reference | β(losing) << β(equal); CPL variance lower when losing |
| **Satisficing near reference** | Uncertainty → "good enough" play | Gap concentrated in forgiving positions (+8.5 CPL vs −2.5 CPL) |
| **Anti-calibration** | Misperceived stakes | Over-thinking easy positions ([[Time Mechanism]]) |

> [!note] What we are NOT claiming
> We do not claim to observe subjective value functions or to estimate λ. The claim is behavioral: template availability modulates reference-point clarity, which mediates perceived stakes and the satisficing–optimizing tradeoff. The S-curve, domain asymmetry, and variance patterns are consistent with this framing and provide a parsimonious account of multiple findings.

## Error Classification with Eval-Sign Flip

Refined chess.com-style classification that distinguishes **missed optimization** (no eval flip — you stayed ahead but left value on the table) from **game-changing errors** (eval flip — you handed over the advantage). N = 1,006,481 moves (moves 1–12, rapid, paired players).

### Rate Breakdown

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

**Totals:**

| | Standard | Chess960 | Δ |
|---|---|---|---|
| All errors (CPL ≥ 50) | 23.4% | 33.5% | +10.1pp |
| └ No eval flip | 15.5% | 21.2% | +5.7pp |
| └ Eval flip | 7.9% | 12.3% | +4.4pp |
| Flip share of errors | 33.7% | 36.7% | |

### CPL Gap Decomposition by Flip Type

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

> [!important] Largest single contributor = mistakes that flip the eval (36.6%)
> These are 100-300 CPL errors where the player was doing fine but played something that handed the advantage to the opponent. Templates provide the "right idea" to avoid crossing into losing territory.

> [!note] No-flip errors (inaccuracy + mistake) together ≈ 50%
> The satisficing signature: you don't lose the game, you just leave value on the table.

### Are 960 Positions Objectively Sharper?

**No.** The positions themselves are equally complex; the "sharpness" is player-generated.

| Metric | Standard | Chess960 |
|--------|----------|----------|
| complexity_1v2 (gap best→2nd) | 33.7 | 33.5 |
| share_good (top5 within 50cp) | 0.726 | 0.697 |
| |eval| < 50 (balanced positions) | 52.6% | 38.7% |
| |eval| < 100 | 73.5% | 62.0% |
| |eval| > 200 (decisive) | 12.0% | 16.7% |
| Eval std dev | 155 | 171 |

960 positions are objectively NOT sharper (complexity_1v2 virtually identical), but 960 *games* spend less time in balanced territory because early errors push the eval around.

**Conditional flip rate at same eval** (given an error occurred):

| Eval band | Std flip% | 960 flip% | Δ |
|-----------|-----------|-----------|---|
| +0 to +50 | 100.0% | 100.0% | 0.0pp |
| +50 to +100 | 69.0% | 73.9% | +4.9pp |
| +100 to +200 | 29.9% | 30.5% | +0.6pp |
| +200 to +400 | 17.4% | 12.6% | -4.7pp |

At the same starting eval, flip rates are barely different. 960 doesn't create sharper positions — it creates more *errors*, and those errors cascade.

**Flip rate by position complexity** (controlling for objective difficulty):

| share_good bin | Std flip | 960 flip | Δ | Std err% | 960 err% | Δ err |
|---------------|----------|----------|---|----------|----------|-------|
| 0–0.25 (hard) | 38.0% | 39.6% | +1.5pp | 37.2% | 38.7% | +1.5pp |
| 0.25–0.5 | 34.2% | 37.1% | +3.0pp | 38.8% | 41.4% | +2.6pp |
| 0.5–0.75 | 32.8% | 37.1% | +4.3pp | 36.2% | 42.6% | +6.4pp |
| 0.75–1.0 (easy) | 35.2% | 40.1% | +4.9pp | 20.2% | 28.8% | +8.6pp |

The gap is largest in **easy** positions — exactly where templates matter most. Without templates, players navigate normal positions as if they were sharp.

### Eval Sign Changes Per Game

How volatile are games? Number of times eval crosses zero during moves 1-12 (N=84,694 games):

| | Standard | Chess960 | t-test |
|---|---|---|---|
| Mean sign changes | 1.40 | 1.68 | t=-25.1, p<10^-137 |
| 0 sign changes | 33.9% | 26.4% | |
| ≥2 sign changes | 39.6% | 47.9% | |

**With ±50cp buffer** (meaningful flips only):

| | Standard | Chess960 | t-test |
|---|---|---|---|
| Mean sign changes | 0.37 | 0.56 | t=-34.8, p<10^-261 |
| ≥1 meaningful flip | 28.6% | 40.9% | |
| ≥2 meaningful flips | 6.5% | 12.3% | |

960 games are significantly more volatile — nearly twice as many games have ≥2 meaningful eval flips. This is the cascade effect: early template-less errors create imbalanced positions that invite further errors.

## Time to First Error

How quickly does the first meaningful error appear? (N=81,774 games with ≥10 analyzed moves, moves 1–12, rapid, paired)

| Metric | Standard | Chess960 | Δ | t-test |
|--------|----------|----------|---|--------|
| **First inaccuracy (CPL≥50)** | | | | |
| % games with ≥1 | 84.1% | 95.4% | +11.3pp | |
| Mean move | 5.18 | **3.46** | -1.72 | t=81.9, p≈0 |
| Median move | 5 | **3** | -2 | |
| **First mistake (CPL≥100)** | | | | |
| % games with ≥1 | 58.9% | 76.2% | +17.3pp | |
| Mean move | 7.03 | **5.91** | -1.11 | t=39.6, p≈0 |
| **First blunder (CPL≥300)** | | | | |
| % games with ≥1 | 16.2% | 16.4% | **+0.2pp** | |
| Mean move | 8.58 | 8.39 | -0.20 | t=3.8, p=0.0001 |
| **First eval flip (CPL≥50 + sign change)** | | | | |
| % games with ≥1 | 56.1% | 72.9% | +16.7pp | |
| Mean move | 5.65 | **4.07** | -1.58 | t=56.2, p≈0 |

**Survival curve** (% games still "clean" — no inaccuracy yet):

| By move | Standard | Chess960 | Δ |
|---------|----------|----------|---|
| 1 | 93.8% | 79.0% | -14.7pp |
| 3 | 69.6% | 40.7% | -28.8pp |
| 6 | 42.3% | 16.1% | -26.1pp |
| 9 | 25.4% | 7.7% | -17.7pp |
| 12 | 15.9% | 4.6% | -11.3pp |

> [!important] Move 1 is the purest template signal
> 22.0% of 960 games have their first inaccuracy on move 1 (vs 7.4% standard). Move 1 in standard is almost always book; in 960 it's a genuine decision from scratch.

> [!note] Blunder timing is nearly identical
> First blunder incidence (16.2% vs 16.4%) and timing (median move 9 both) are format-invariant. The tactical safety net holds — it's purely optimization errors that come earlier and more often. This is the cascade seed: the first template-less stumble on move 2–3 pushes the eval off balance, and downstream errors compound.

## Error Contagion & Transition Matrix

Does an opponent's error raise your error probability? (Consecutive half-moves, different players, moves 1–12)

### Contagion Effect

| | Standard | Chess960 |
|---|---|---|
| Error rate after opp clean move | 18.8% | 29.2% |
| Error rate after opp error (CPL≥50) | 42.0% | 45.0% |
| **Contagion (Δ)** | **+23.2pp** | **+15.8pp** |
| Mean CPL after opp clean | 32.0 | 43.2 |
| Mean CPL after opp error | 73.3 | 71.0 |
| **CPL contagion (Δ)** | **+41.2** | **+27.8** |

Both t-tests p≈0. Contagion is **stronger in standard** (+23.2pp vs +15.8pp), but this is a ceiling effect: 960 players already err at 29.2% baseline (vs 18.8%), leaving less room for contagion. In relative terms: standard = 2.2x multiplier, 960 = 1.5x multiplier.

**By trigger severity:**

| Trigger | Std err% after | 960 err% after | Std Δ | 960 Δ |
|---------|---------------|---------------|-------|-------|
| Inaccuracy (50–100) | 37.8% | 42.6% | +19.0pp | +13.4pp |
| Mistake (100–300) | 48.2% | 49.0% | +29.4pp | +19.9pp |
| Blunder (300+) | 42.3% | 41.2% | +23.5pp | +12.1pp |

> [!note] Templates provide baseline resilience but create fragility when disrupted
> Standard players operate at a low error floor thanks to templates, but when the opponent's error pushes them off-book, the jump is larger. 960 players already operate without that floor, so marginal impact of opponent errors is smaller.

### Full Transition Matrix

**Standard** (opponent move → your response):

| Opp ↓ / You → | Best | Good | Inacc | Mistake | Blunder | N |
|---|--:|--:|--:|--:|--:|--:|
| Best | 23.6% | 62.3% | 8.5% | 4.7% | 0.8% | 191,994 |
| Good | 13.2% | 66.9% | 12.3% | 6.5% | 1.1% | 847,090 |
| Inaccuracy | 10.4% | 51.8% | 22.3% | 13.6% | 1.9% | 171,933 |
| Mistake | 9.1% | 42.7% | 15.7% | 27.7% | 4.8% | 113,823 |
| Blunder | 8.2% | 49.5% | 5.9% | 13.3% | 23.1% | 22,260 |

**Chess960:**

| Opp ↓ / You → | Best | Good | Inacc | Mistake | Blunder | N |
|---|--:|--:|--:|--:|--:|--:|
| Best | 19.1% | 56.5% | 15.0% | 8.3% | 1.1% | 72,442 |
| Good | 12.0% | 57.6% | 18.9% | 10.3% | 1.1% | 311,512 |
| Inaccuracy | 10.3% | 47.2% | 25.1% | 16.1% | 1.4% | 110,256 |
| Mistake | 10.3% | 40.7% | 17.3% | 28.3% | 3.5% | 74,900 |
| Blunder | 9.1% | 49.6% | 5.8% | 14.7% | 20.7% | 9,654 |

**Δ (960 − Standard):**

| Opp ↓ / You → | Best | Good | Inacc | Mistake | Blunder |
|---|--:|--:|--:|--:|--:|
| Best | -4.4 | -5.8 | **+6.5** | **+3.6** | +0.2 |
| Good | -1.2 | **-9.3** | **+6.5** | **+3.8** | +0.1 |
| Inaccuracy | -0.1 | -4.6 | +2.7 | +2.6 | -0.5 |
| Mistake | +1.2 | -2.0 | +1.5 | +0.5 | -1.2 |
| Blunder | +1.0 | +0.0 | -0.0 | +1.4 | **-2.4** |

### Key Transition Matrix Findings

1. **Top two rows** (after opp Best/Good): massive shift from Good → Inaccuracy/Mistake (+6.5pp each). Templates keep you clean in routine play.
2. **Bottom two rows** (after opp Mistake/Blunder): differences are small and mixed. Once things go sideways, templates don't help.
3. **Blunder→Blunder is -2.4pp**: 960 players are *more composed* after opponent disasters.
4. **Capitalization rate after opp error**: nearly identical (52.8% std vs 51.8% 960). Templates don't help you *punish* errors.
5. **Good→Good rate**: 81.2% std vs 70.8% 960 (-10.4pp). The entire format gap lives in routine positions.

> [!important] The format gap lives in normal play, not in crisis management
> After opponent plays Best/Good, standard players respond with Best/Good 81.2% of the time vs 70.8% in 960. After opponent mistakes/blunders, capitalization rates are virtually identical (~52%). Templates are a consistency tool for routine positions, not an exploitation tool for crises.

### Error Cascade Model

The findings support a cascade interpretation of the 960 format gap:

1. **Seed**: First template-less error comes early (median move 3 vs move 5)
2. **Propagation**: Early error pushes eval off-balance → positions leave balanced territory (38.7% vs 52.6% within |eval|<50)
3. **Amplification**: Imbalanced positions invite further errors from both players (contagion)
4. **Asymmetry**: In standard, templates provide resilience in normal positions (81% good-after-good) but fragility when disrupted (+23pp contagion). In 960, baseline error rate is already high but contagion adds less.
5. **Not position sharpness**: Objective complexity (complexity_1v2) is identical; the "sharpness" is player-generated

## Mechanism Story

1. **Reference-point clarity**: In standard chess, templates provide a salient reference ("I am on-book / plan-consistent"). Small deviations are behaviorally meaningful. In 960, the reference is ambiguous — players face higher uncertainty about what "par" looks like.
2. **Near parity** (|eval| < 50cp): templates help optimize among reasonable moves. Without them, ambiguity triggers satisficing → format gap peaks (+0.459 in log CPL).
3. **Diminishing sensitivity**: as positions become more extreme, templates lose relevance. What matters is pure calculation, and template interference fades.
4. **Reversal at extremes** (|eval| > 200cp): format effect vanishes. In heavily losing positions, 960 players show lower CPL variance and fewer catastrophes — consistent with focused calculation unclouded by template overconfidence.
5. **Catastrophes are format-invariant** — downside protection is preserved regardless of template availability. The cost is entirely in missed optimization near parity.
6. **Time allocation** confirms: over-thinking is most pronounced when winning (1.21x) — the domain where loss aversion is strongest.
7. **Depth-free replication**: quadratic interaction (−0.035***) holds with num_legal_moves, ruling out engine-circularity artifacts.

## Scripts

- Analysis run inline (difficulty_rubric.py data loading + custom queries)

See also: [[Reference-Point Clarity]], [[Time Mechanism]], [[Complexity Analysis]], [[Key Results]], [[Freestyle Friday Data]]

#chess960 #mechanism #errors #risk #prospect-theory
