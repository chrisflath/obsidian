# Game Volatility

## Core Question

How volatile are 960 games compared to standard? Do errors cascade into position instability?

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

### Survival Curve (% games still "clean" — no inaccuracy yet)

| By move | Standard | Chess960 | Δ |
|---------|----------|----------|---|
| 1 | 93.8% | 79.0% | -14.7pp |
| 3 | 69.6% | 40.7% | -28.8pp |
| 4 | 59.1% | 29.6% | -29.4pp |
| 6 | 42.3% | 16.1% | -26.1pp |
| 9 | 25.4% | 7.7% | -17.7pp |
| 12 | 15.9% | 4.6% | -11.3pp |

By move 4, only **30% of 960 games** are still clean vs **59% of standard games**. The first template-less stumble comes almost immediately.

### First Inaccuracy by Move Number

| Move | Standard | Chess960 | Δ |
|------|----------|----------|---|
| 1 | 7.4% | **22.0%** | +14.5pp |
| 2 | 15.4% | 22.8% | +7.4pp |
| 3 | 13.4% | 17.4% | +4.0pp |
| 4 | 12.5% | 11.6% | -0.8pp |
| 5+ | diminishing | diminishing | converging |

> [!important] Move 1 is the purest template signal
> 22.0% of 960 games have their first inaccuracy on move 1 (vs 7.4% standard). Move 1 in standard is almost always book; in 960 it's a genuine decision from scratch.

> [!note] Blunder timing is format-invariant
> First blunder incidence (16.2% vs 16.4%) and timing (median move 9 both) are essentially identical. The tactical safety net holds — it's purely optimization errors that come earlier.

## Eval Sign Changes Per Game

How many times does the advantage change hands? (N=84,694 games, moves 1-12)

| | Standard | Chess960 | t-test |
|---|---|---|---|
| Mean sign changes | 1.40 | 1.68 | t=-25.1, p<10^-137 |
| 0 sign changes | 33.9% | 26.4% | |
| ≥2 sign changes | 39.6% | 47.9% | |

### With ±50cp Buffer (meaningful flips only)

| | Standard | Chess960 | t-test |
|---|---|---|---|
| Mean sign changes | 0.37 | 0.56 | t=-34.8, p<10^-261 |
| ≥1 meaningful flip | 28.6% | 40.9% | |
| ≥2 meaningful flips | 6.5% | 12.3% | |

960 games are significantly more volatile — nearly twice as many games have ≥2 meaningful eval flips.

### Distribution of Sign Changes

| Count | Standard | Chess960 | Δ |
|-------|----------|----------|---|
| 0 | 33.9% | 26.4% | -7.5pp |
| 1 | 26.5% | 25.7% | -0.8pp |
| 2 | 19.0% | 21.3% | +2.3pp |
| 3 | 11.7% | 14.2% | +2.4pp |
| 4+ | 8.9% | 12.4% | +3.5pp |

## Are 960 Positions Objectively Sharper?

**No.** The objective complexity is virtually identical; the volatility is player-generated.

| Metric | Standard | Chess960 |
|--------|----------|----------|
| complexity_1v2 (gap best→2nd) | 33.7 | 33.5 |
| share_good (top5 within 50cp) | 0.726 | 0.697 |
| |eval| < 50 (balanced positions) | 52.6% | **38.7%** |
| |eval| > 200 (decisive) | 12.0% | **16.7%** |
| Eval std dev | 155 | 171 |

Objective complexity (complexity_1v2) is identical. But 960 *games* spend much less time in balanced territory (38.7% vs 52.6% within |eval|<50) because early errors push the eval around.

**Conditional flip rate at same starting eval** (given an error):

| Eval band | Std flip% | 960 flip% | Δ |
|-----------|-----------|-----------|---|
| +0 to +50 | 100.0% | 100.0% | 0.0pp |
| +50 to +100 | 69.0% | 73.9% | +4.9pp |
| +100 to +200 | 29.9% | 30.5% | +0.6pp |
| +200 to +400 | 17.4% | 12.6% | -4.7pp |

At the same starting eval, flip rates are barely different. 960 doesn't create sharper positions — it creates more *errors*, which cascade into position instability.

## The Error Cascade Model

1. **Seed**: First template-less error comes early (median move 3 vs move 5)
2. **Propagation**: Early error pushes eval off-balance → positions leave balanced territory
3. **Amplification**: Imbalanced positions invite further errors from both players ([[Error Contagion]])
4. **Asymmetry**: In standard, templates provide resilience in normal positions but fragility when disrupted. In 960, baseline error rate is already high but contagion adds less.
5. **Not position sharpness**: The "sharpness" is emergent from both players lacking templates, not inherent to starting positions

See also: [[Error Contagion]], [[Eval-Sign Classification]], [[Error Composition]], [[Reference-Point Clarity]]

#chess960 #mechanism #volatility #cascade
