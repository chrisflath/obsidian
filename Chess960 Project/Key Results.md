# Key Results

## Main Finding

Players perform significantly worse in Chess960 openings (moves 1-12), and this gap reflects the loss of preparation capital — not position difficulty.

## Result 1: Format Gap

`mean(log(CPL+1))` is **+0.18** higher in Chess960 (p < 0.001).

After [[Start-Position Fixed Effects]]: gap = +0.10 (41% reduction, 59% survives).

## Result 2: Prep Capital Interaction (theta3)

From [[Two-Rating Decomposition]]:
- theta3 = **+0.050**** — standard rating is less predictive in Chess960
- **Opening-specific**: theta3 vanishes in middlegame and endgame
- Consistent across rating sources (API, PGN median, PGN first-observed)

## Result 3: Gelbach Channels

From [[Gelbach Decomposition]]:
- **Bishops** are the largest single contributor (15.4% of gap)
- Knights *help* when displaced (-6.2%)
- **64.3% residual** = pure template-absence effect
- Clock state explains only 1.1%

## Result 4: Player Heterogeneity

From [[Random Slopes & BLUPs]]:
- Players with high prep rent (R_std >> R_960) have the largest format gaps (r = +0.229***)
- 960 specialists and diverse-repertoire players show smaller gaps

## Result 5: Complexity Is Not a Confound

From [[Complexity Analysis]]:
- Chess960 positions are slightly *less* complex (lower complexity_1v2)
- Format effect persists (+9.1 cp) after full complexity controls
- `share_good_top5` is the strongest complexity predictor

## Result 6: Robustness

From [[Robustness Checks]]:
- 7 alternative DVs all show the same pattern
- Quarterly stability: no attenuation 2020-2024
- Experience cohorts: gap = ~0.14 across all cohorts, no convergence
- FE vs RE: equivalent specifications

## Result 7: Error Composition & Reference-Point Clarity

From [[Error Composition]] and [[Reference-Point Clarity]]:
- **Catastrophe rate is format-invariant** (1.7% both formats, p=0.60)
- Gap comes from mid-range errors: mistakes (41%) + blunders (58%)
- Gap concentrated in **forgiving positions** (sg≥0.5): +8.5 CPL; demanding: −2.5 CPL
- **S-curve**: format gap peaks near parity (|eval|≈25cp), vanishes at |eval|≈200cp, reverses at extremes
- Piecewise spline: is_960 × sp_50 = −0.444***, replicates with depth-free proxy (legal_z²= −0.035***)
- Interpretation: templates modulate reference-point clarity → satisficing vs optimizing tradeoff

## Result 8: Anti-Calibration

From [[Time Mechanism]]:
- Within-player corr(share_good, log_time): Standard r=−0.035 (correct), Chess960 r=+0.046 (**inverted**)
- Paired t = −11.8, p < .0001
- 960 players over-think easy positions, under-think hard ones
- Time over-allocation largest when winning (1.21x)

## Result 9: Eval-Sign Classification

From [[Eval-Sign Classification]]:
- **Mistakes with eval flip** (player crosses from not-losing to losing) = **36.6%** of CPL gap — single largest contributor
- **No-flip errors** (optimization loss, staying ahead but suboptimal) = ~50% of gap — the satisficing signature
- **Blunders format-invariant** regardless of flip type (~1.7-1.8%)
- Flip share of errors: 33.7% (std) → 36.7% (960) — 960 errors are proportionally more game-changing

## Result 10: Game Volatility & Error Cascade

From [[Game Volatility]]:
- **Time to first inaccuracy**: median move 3 (960) vs move 5 (standard); 95.4% vs 84.1% of games affected
- **Move 1 signal**: 22% of 960 games have first inaccuracy on move 1 (vs 7.4% standard)
- **Eval sign changes**: 0.56/game (960) vs 0.37 (standard) with ±50cp buffer; ≥1 meaningful flip in 40.9% vs 28.6%
- **Not position sharpness**: complexity_1v2 identical (33.5 vs 33.7); "sharpness" is player-generated cascade, not position-generated

## Result 11: Error Contagion

From [[Error Contagion]]:
- **Contagion**: opponent error raises your error rate by +23.2pp (std) vs +15.8pp (960) — ceiling effect from 960's higher baseline
- **Transition matrix**: Good→Good rate = 81.2% (std) vs 70.8% (960); after opponent errors, capitalization nearly identical (~52%)
- **ELO gradient**: 2100+ players show strongest contagion (3.7x multiplier in std) and largest capitalization gap (-5.3pp in 960)
- Templates are a **consistency tool** for routine positions, not an exploitation tool for crises

## Result 12: Cross-Platform Replication (Chess.com Elite)

From [[Freestyle Friday Data]] and [[Gelbach Decomposition]]:

Using Freestyle Friday (960 blitz 3+1) vs Titled Tuesday (standard blitz 3+1), N=5,182 games, 252 paired players:

- **Format gap 1.87x larger** in elite blitz (+0.291 log-scale vs +0.155 Lichess rapid) — time pressure amplifies template loss
- **Gelbach decomposition structure replicates**: 41.4% explained (vs 35.7%), 58.6% residual (vs 64.3%)
- **Queen** is the largest single contributor (+17.0%), overtaking bishops (+9.8%) in the elite sample
- **Template distance gradient** replicates within 960
- **Theta3 (prep capital interaction)**: not significant in chess.com elite (p=0.60) due to range restriction (R_std SD=240 vs Lichess SD=435). In-game rating interaction is significant (+0.019, p=0.034)

> [!note] Evolving
> Based on ~30% of chess.com data. Engine analysis still in progress. Piece-level estimates will continue to stabilize.

## Result 13: Expertise Gradient — Template Dependency Is Not Outgrown

Combined Lichess rapid tiers (800–2400+) with Chess.com titled players at the top:

| Tier | Platform | CPL 960 | CPL std | Gap (CPL) | Gap (log) | Paired t |
|------|----------|---------|---------|-----------|-----------|----------|
| 800-1200 | Lichess | 79.3 | 70.5 | +8.7 | +0.27 | 5.8*** |
| 1200-1500 | Lichess | 63.9 | 54.0 | +9.9 | +0.31 | 10.4*** |
| 1500-1800 | Lichess | 56.2 | 44.3 | +11.9 | +0.37 | 14.0*** |
| 1800-2100 | Lichess | 44.4 | 30.9 | +13.5 | +0.42 | 17.3*** |
| 2100-2400 | Lichess | 39.5 | 26.7 | +12.8 | +0.39 | 14.6*** |
| 2400+ | Lichess | 29.5 | 18.7 | +10.8 | +0.40 | 8.2*** |
| **Titled** | **Chess.com** | **32.4** | **14.6** | **+17.8** | **+0.67** | **12.2***** |

**Key findings:**
- Standard CPL drops monotonically from 70 to 15 as expertise rises — experts are much better at chess
- But the format gap **does not shrink** — it grows from +0.27 (amateurs) to +0.40 (Lichess 2400+) in log-scale
- Chess.com titled players: **+0.67 log-gap**, 1.7x the Lichess top tier
- Chess.com titled standard CPL (14.6) is *lower* than Lichess 2400+ (18.7), confirming greater skill — yet their 960 gap is larger
- The 1.7x ratio is partly time-control amplification (blitz vs rapid), but the pattern is clear: **the more you invest in templates, the more you lose when they're removed**

### Raw CPL Decomposition: Expertise Survives, Everybody Suffers

The graded transfer plot in raw CPL (not log-transformed) reveals a clean two-component decomposition:

**Graded transfer slopes by quintile (raw CPL):**

| Tier | Std baseline | 960 intercept | Slope (CPL/unit) | Format offset |
|------|-------------|---------------|-------------------|---------------|
| Q1: 618–1420 | 62.6 | 67.3 | 0.47 | +4.7 |
| Q2: 1427–1648 | 45.5 | 53.9 | 0.48 | +8.4 |
| Q3: 1650–1862 | 40.5 | 44.8 | 0.64 | +4.3 |
| Q4: 1864–2131 | 28.9 | 37.5 | 0.55 | +8.6 |
| Q5: 2136–3085 | 16.9 | 25.5 | 0.55 | +8.6 |
| Titled (Blitz) | 14.8 | 26.7 | 0.58 | +11.9 |

**Two components decompose differently across expertise:**

1. **Format offset** (intercept shift at td=0): **scales with expertise** — experts lose more at td=0 because they had more template capital to begin with. Grows from ~5 CPL (Q1) to ~12 CPL (Titled).
2. **Graded transfer slope**: **skill-invariant** (~0.5 CPL per unit of template distance, flat across all tiers). Displacement is equally costly for everyone in absolute terms.

> [!important] Expertise survives but everybody suffers equally from displacement
> The parallel raw CPL slopes mean that position-level disruption from piece displacement is a fixed cognitive cost — a displaced bishop is equally confusing to a 1000 and a 2200. What varies with expertise is the *baseline* template-loss penalty (the format offset): experts lose more because they had more to lose. This is a cleaner decomposition than the log version, where both effects get conflated by the nonlinear transform.

**Why the log version looks different:** The log-space slopes steepen with expertise (0.003 → 0.008) because `d/dx[log(CPL+1)] ≈ slope_raw / (mean_CPL+1)`. With equal raw slopes (~0.5) but lower baselines for experts, the same absolute cost maps to a proportionally larger log-space effect. The log version conflates two things: the uniform absolute gradient plus baseline compression.

**Plot:** `plots/publication/panel_b_quintiles_raw.pdf` (raw CPL) and `panel_b_quintiles.pdf` (log-transformed).

> [!note] Cross-platform caveat
> Lichess rapid and chess.com blitz are different time controls and rating pools. The chess.com tier is placed above Lichess because all players are titled (GMs, IMs). The 1.7x gap inflation includes both expertise and time-pressure effects. Within each platform the expertise gradient is independently significant.

## Result 14: Template Carry-Over

From [[Template Carry-Over]]:

Players carry their standard top-2 opening moves into **27%** of 960 games (r=0.231*** with repertoire concentration).

**Position similarity is the key moderator:**
- Near-standard (fd ≤ 8): 34.3% carry-over, template move **saves 6.7 CPL**
- Far-from-standard (fd > 14): 23.2% carry-over, template move gives **zero benefit** (+0.2 CPL)
- Central pawn pushes (e4, d4) transfer well (~22 CPL); position-specific moves (Nf6, d6) are terrible (40-59 CPL)

> [!important] Template carry-over is rational near standard but degrades to mere habit as displacement grows — supporting the graded transfer interpretation.

## Publication Figures

1. **Fig 1** (`fig1_hero.pdf`): Three-panel hero — (a) phase bars, (b) displacement gradient with scatter, (c) Gelbach waterfall
2. **Fig 2** (`fig2_theta3_phase.pdf`): theta3 by game phase
3. **Fig 3** (`fig3_blup_scatter.pdf`): BLUPs vs prep rent

Generated by `scripts/publication_figures.py`, output to `plots/publication/`.

See also: [[Research Open Ends]] for pending analyses and cross-project opportunities.

#chess960 #results
