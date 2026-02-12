# Reference-Point Clarity

## Core Construct

In standard chess, opening templates provide a salient, shared reference — "I am on-book / plan-consistent" — which makes small deviations behaviorally meaningful. In Chess960, that reference is weaker; players face higher ambiguity about what "par" looks like, so they:
1. **Satisfice** more in slack states (forgiving positions near parity)
2. **Behave differently** when already behind (loss domain)

This is not a claim that players have subjective value functions over centipawns. It is a claim that **template availability modulates reference-point clarity**, which in turn mediates perceived stakes and the satisficing–optimizing tradeoff.

## The S-Curve: Format Gap by Position Evaluation

The format gap (960 CPL − standard CPL) follows a prospect-theory-like value function when plotted against pre-move evaluation. N=887K moves, eval clipped ±500cp.

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

Three regimes:
1. **Near parity** (|eval| < 50cp): Gap peaks at +13.8 CPL. Templates optimize among reasonable moves.
2. **Moderate advantage** (50–200cp): Gap diminishes. Positions become more "self-explaining."
3. **Decisive** (|eval| > 200cp): Gap **reverses** to −11 CPL. Pure calculation dominates; template interference actually hurts.

## Formal Specification: Piecewise-Linear Spline

`log(CPL+1) ~ is_960 × f(|eval|) + move_z + player FE` (player-clustered SEs, N=887K)

Knots at {25, 50, 100, 200} cp. Marginal format effect:

| |eval| (cp) | β_format | 95% CI |
|-------------|----------|--------|
| 0 | +0.407 | [+0.356, +0.457] |
| **25** | **+0.459** | [+0.403, +0.515] |
| 50 | +0.430 | [+0.385, +0.474] |
| 75 | +0.290 | [+0.254, +0.326] |
| 100 | +0.149 | [+0.109, +0.190] |
| 150 | +0.072 | [+0.040, +0.103] |
| **200** | **−0.006** | [−0.042, +0.031] |
| 300 | −0.004 | [−0.037, +0.029] |

Peak at |eval| ≈ 25cp. Zero-crossing at |eval| ≈ 200cp. Flat thereafter.

Key spline interactions:
- `is_960 × sp_50` = **−0.444*** (gap accelerates downward between 50–100cp)
- `is_960 × sp_100` = +0.406*** (deceleration — floor reached)

## Domain Split with Player FE

`log(CPL+1) ~ is_960 × domain + move_z + player FE` (player-clustered SEs)

### Threshold ±50cp

| Domain | β(is_960) | SE | p | N |
|--------|-----------|-----|---|---|
| Equal (±50cp) | **+0.459** | 0.023 | *** | 438K |
| Winning (>50) | +0.233 | 0.018 | *** | 293K |
| Losing (<−50) | +0.140 | 0.018 | *** | 156K |

| Contrast | Estimate | p |
|----------|----------|---|
| Δ(winning − equal) | **−0.226** | *** |
| Δ(losing − equal) | **−0.319** | *** |

### Robustness: Threshold ±25cp

Same ordering. Equal +0.440***, Winning +0.392***, Losing +0.229***. Δ(losing − equal) = −0.212***.

> [!note] All domains have β > 0 in log scale
> With player FE and log(CPL+1), the losing-domain coefficient is positive but much smaller. The raw CPL gap IS negative when losing (−2.8 CPL) — the log compression dampens the tails. The key finding is the **ordering**: β(equal) >> β(winning) > β(losing).

## Move Volatility: Chess-Native Risk Proxy

Prospect theory's reflection effect concerns **variance**, not just means. Using MultiPV data (423K moves):

### Within-Player CPL Variance (paired t-tests)

| Domain | Std var | 960 var | t | p |
|--------|---------|---------|---|---|
| Winning | 5,328 | 6,133 | +2.86 | .005** |
| Equal | 2,749 | **3,429** | +4.98 | <.0001*** |
| Losing | 8,329 | 7,775 | −1.44 | .15 n.s. |

960 players are MORE erratic when winning/equal (no template → inconsistent satisficing), but equally or LESS erratic when losing (focused calculation).

### Position Eval Spread

`eval_spread_z ~ is_960 × is_losing + move_z + player FE` (N=423K, clustered SEs):

| Coefficient | Estimate | SE | p |
|-------------|----------|-----|---|
| is_960 | +0.031 | 0.007 | *** |
| is_losing | +0.267 | 0.012 | *** |
| **is_960 × losing** | **−0.141** | 0.014 | *** |

When losing, 960 positions have lower eval spread — players navigate to less volatile continuations (or 960 losing positions are structurally less volatile).

### Time by Domain

| Domain | Std time | 960 time | 960/Std |
|--------|----------|----------|---------|
| Losing | 9.4s | 10.5s | 1.12x |
| Equal | 9.4s | 10.4s | 1.11x |
| Winning | 8.5s | 10.2s | **1.21x** |

Over-thinking most pronounced when winning — the domain with the most to protect and the highest reference-point ambiguity.

## Depth-Free Validity Check

> [!warning] Potential circularity
> eval_before and CPL are both derived from the same Stockfish pipeline. The S-curve could be mechanical if deeper analysis systematically compresses eval-CPL correlation.

### num_legal_moves (fully depth-free)

`log(CPL+1) ~ is_960 × legal_z + is_960 × legal_z² + move_z + player FE` (N=423K, clustered SEs):

| Coefficient | Estimate | SE | p |
|-------------|----------|-----|---|
| is_960 × legal_z | **−0.133** | 0.013 | *** |
| is_960 × legal_z² | **−0.035** | 0.004 | *** |

The **quadratic interaction replicates** with a completely depth-free proxy.

### share_good (engine-derived, independent of CPL)

| Position type | Format gap (raw CPL) |
|--------------|---------------------|
| Hard (sg < 0.25) | **−2.8** |
| Moderate (0.25–0.5) | +4.6 |
| Easy (0.5–0.75) | +3.3 |
| Very easy (sg > 0.75) | **+8.3** |

Same pattern: gap negative in demanding positions, peaks in forgiving ones.

## Prospect Theory Mapping

| PT Concept | Operationalization | Evidence |
|------------|-------------------|----------|
| **Reference-point clarity** | Templates define "par" | Format gap peaks near equality, vanishes at extremes |
| **Loss aversion** | Downside protection > optimization | Catastrophe rate flat (p=.60); perfect rate falls −1.77pp |
| **Diminishing sensitivity** | Gap shrinks with |eval| | Spline: β peaks at 25cp, zero by 200cp |
| **Reflection** | Different behavior below reference | β(losing) << β(equal); CPL variance lower when losing |
| **Satisficing** | Uncertainty → "good enough" play | Gap concentrated in forgiving positions (+8.5 vs −2.5 CPL) |

> [!note] What we are NOT claiming
> We do not claim to observe subjective value functions or to estimate λ. The claim is behavioral: template availability modulates reference-point clarity, which mediates perceived stakes and the satisficing–optimizing tradeoff. The S-curve, domain asymmetry, and variance patterns are consistent with this framing.

## Connection to Other Mechanisms

- **Anti-calibration** ([[Time Mechanism]]): positions feel uncertain without templates → over-thinking easy positions. Time over-allocation is largest when winning (1.21x).
- **Error composition** ([[Error Composition]]): catastrophe rate is format-invariant; the gap comes from mid-range errors (satisficing) in forgiving positions.
- **Template distance** ([[Key Results]]): the S-curve exists within-format too — farther from standard → larger gap, but only near parity.
- **Complexity as suppressor** ([[Complexity Analysis]]): 960 positions are objectively slightly easier, so reference-point ambiguity overstates the raw gap.

## Scripts

- Analysis run inline via difficulty_rubric.py data loading + custom queries
- Spline and domain-split models estimated with statsmodels OLS + FWL demeaning + cluster-robust SEs

See also: [[Error Composition]], [[Time Mechanism]], [[Complexity Analysis]], [[Key Results]]

#chess960 #mechanism #prospect-theory #reference-point
