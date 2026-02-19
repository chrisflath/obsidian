# Key Results

## Main Finding

Players perform significantly worse in Chess960 openings (moves 1-12), and this gap reflects the loss of preparation capital — not position difficulty.

## Result 1: Format Gap

`mean(log(CPL+1))` is **+0.15** higher in Chess960 (p < 0.001, N=106,289 games, 438 players).

### ⚠️ SP Fixed Effects — UNINFORMATIVE (identification problem, discovered 2026-02-19)

The FWL/SP FE specification is near-perfectly collinear: all standard games map to SP=518, so `is_960` loses 99.84% of its variance after demeaning. The format coefficient is identified from only ~39 chess960 games that happened to draw SP 518. Bootstrap analysis (200 resamples) shows p<0.05 in only 10% of draws (median p=0.27). The earlier documented result (+0.1034*, 41% reduction) was a statistical fluke.

**Use the Gelbach decomposition instead** — it uses continuous position features (piece displacements, structural indicators) and is well-identified. Gelbach: 35.7% of gap explained by observable position features, 64.3% residual = pure template-absence effect.

## Result 2: Prep Capital Interaction (theta3) & General Skill (theta4)

From [[Two-Rating Decomposition]] (N=106,289 games, 438 players, verified 2026-02-19):
- theta3 = **+0.048****** — standard rating is less predictive in Chess960
- theta4 = **-0.052****** — 960 rating becomes more predictive in its own format
- **Asymmetric phase dynamics** (mixed-effects, N=80K/66K/25K by phase):
  - theta3: +0.058*** (opening) → +0.020** (middlegame) → +0.028 n.s. (endgame) — **prep capital decays**
  - theta4: stable at ~-0.05 across all phases — **general skill transfers uniformly**
- Key insight: preparation advantage is phase-specific (opening); general reasoning skill transfers across all phases
- With larger sample, middlegame theta3 is now significant (p=0.002) — prep capital effect extends beyond opening
- Endgame n.s. likely a power issue (N=25K vs 80K in opening)
- PGN median theta3 = +0.037*** (replicates)

## Result 3: Gelbach Channels

From [[Gelbach Decomposition]]:
- **Bishops** are the largest single contributor (15.4% of gap)
- Knights *help* when displaced (-6.2%)
- **64.3% residual** = pure template-absence effect
- Clock state explains only 1.1%

## Result 4: Player Heterogeneity

From [[Random Slopes & BLUPs]] (386 players, verified 2026-02-19):
- Players with high prep rent (R_std >> R_960) have the largest format gaps (r = +0.151**, was +0.229)
- 960 specialists show smaller gaps (r = -0.211***, was -0.287)
- eco_hhi strengthened (r = -0.312***, was -0.215)
- experience_ratio **lost significance** (r = -0.017 n.s., was -0.146*) — marginal in original sample
- Core pattern holds: prep rent and specialist ratio remain significant predictors

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

**Continuous difficulty measure (|eval_pv1 − eval_pv5|):**
- 1,124 unique values (vs 5 for share_good) — much finer-grained
- Per-player calibration shift (960 corr − standard corr): mean = −0.061, t = −8.9, p < .0001
- 77% of players shift toward decalibration
- **Uniform across ELO**: all tiers show ~−0.05 to −0.07 shift, 71–82% negative per tier
- Alternative continuous measures (SD of top-5, mean PV gap) produce equivalent results

**Error concentration in forgiving positions:**
- Demanding (few good moves): format gap Δ = +0.22
- Moderate: Δ = +0.41
- Forgiving (many good moves): Δ = +0.49
- Templates help most where errors concentrate — optimizing among good options, not avoiding catastrophes

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

### Anti-Calibration Replicates (chess.com elite)

With N=13,653 moves (35 paired players, partial MultiPV coverage):

| | Standard | Chess960 | Lichess reference |
|---|---|---|---|
| Mean within-player r(share_good, log_time) | **−0.057** | **+0.048** | −0.035 / +0.046 |
| Paired t | **−3.03** (p=0.005) | | −11.8 (p<.0001) |

- Sign flip replicates: standard players correctly allocate less time to easy positions; 960 players are anti-calibrated
- Effect **stronger** in elite blitz than Lichess rapid — time pressure amplifies miscalibration
- Aggregate: std r=−0.066, 960 r=+0.065 (both p<.0001)

### Chess.com Complexity Replication (N=20,127 moves, 252 players)

**Result 5 replication — Complexity is not a confound:**
- Format gap +17.6 CPL after full complexity controls (raw: +18.4)
- `share_good_top5` is strongest predictor (−5.2/SD), same as Lichess
- `complexity_1v2` not significant (p=0.27) — weaker than Lichess where it was marginal
- R² = 0.070

**Result 7-style selective blindness — DIFFERENT pattern in elite blitz:**
- Lichess: gap concentrated in forgiving positions (+8.5), demanding positions reversed (−2.5)
- Chess.com: gap present in BOTH — forgiving +16.3, demanding +23.0
- Interpretation: time pressure removes the compensatory vigilance that Lichess rapid players deploy in demanding positions

**S-curve — partially replicates:**
- Gap peaks near parity (0-50cp): +14-16 CPL, decays toward extremes (+8.8 at 200-500cp)
- Same shape but doesn't reverse at extremes — time pressure prevents "pure calculation" advantage

**Suppressor — does NOT replicate:**
- Complexity acts as mild confound (−4.4%) in chess.com vs suppressor (+8.8%) in Lichess
- Chess.com 960 positions have higher complexity_1v2 (27.8 vs 19.6), opposite of Lichess
- Different direction but small magnitude — complexity is not a major channel in either sample

### Difficulty Rubric (cross-platform, N=968K moves)

Combined Lichess rapid (5 rating tiers: 800-2400+) with Chess.com titled players. X-axis: # good moves within 25cp of best (1 to 5+). Faceted by format/template distance × game phase.

**Key findings from 2×3 grid (opening + middlegame × standard + 960-near + 960-far):**

1. **Opening dose-response**: Lines shift upward Standard → Near-960 → Far-960. Titled players collapse from ~15-20 CPL (standard) to ~40-60 CPL (far-960)
2. **Middlegame convergence**: All three columns look nearly identical — same slopes, same tier ordering, same CPL levels. Starting position is irrelevant by move 13
3. **Titled players overlap Lichess 2100+ in middlegame** regardless of starting position — confirming skill comparability and that the opening divergence is real template loss, not a sample artifact
4. **Satisficing signal**: Uptick at n_good=5+ in some 960 cells — when many moves look good, players stop optimizing

**Normalized version** (CPL / player's standard opening baseline):
- Standard opening: all tiers cluster near 1.0x (by construction)
- 960 opening: tier ordering INVERTS — experts show highest ratios (1.5-2.5x), amateurs ~1.0x
- Middlegame: ratios compress back, all tiers similar (~1.5x)
- **Interpretation**: experts lose more proportionally — the more template capital invested, the larger the proportional loss when templates are removed

**Plots:** `plots/difficulty_rubric_td_phase.png` (raw CPL) and `plots/difficulty_rubric_normalized.png` (normalized)

> [!note] Evolving
> Chess.com engine analysis ~20% complete for 960 games. MultiPV complexity: 79.5K positions at depth 13.0 (matching Lichess). Anti-calibration and complexity replications are preliminary but significant.

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

### Q3-Normalized Decomposition: Inherent Skill vs Template Capital

Dividing each tier's 960 CPL by Q3's sloped 960 regression line (CPL = 46.0 + 0.56 × td) reveals **convergence toward the median player** as template distance increases:

| Tier | Ratio at td=0 | Ratio at td=20 | Norm slope |
|------|--------------|----------------|------------|
| Q1 (weakest) | 1.55 | 1.24 | −0.013 |
| Q3 (median) | 1.03 | 1.00 | −0.001 |
| Q5 (strongest) | 0.55 | 0.63 | +0.005 |
| Titled (Blitz) | 0.58 | 0.68 | +0.005 |

**Decomposition of the expertise gap:**
- **Right side (td≈20)**: spread ≈ 0.6 (1.24 − 0.63) = **inherent skill difference** — what remains after templates are fully stripped away. Experts genuinely are better at chess even without preparation.
- **Left side (td≈0)**: spread ≈ 1.0 (1.55 − 0.55) = inherent skill + template capital
- **Convergence (left → right)**: ~40% of the observable expertise gap at near-standard positions is **template capital**; ~60% is **irreducible skill**

> [!important] Independent convergence with Gelbach
> The ~60% irreducible skill / ~40% template capital split converges with the Gelbach residual (~64% unexplained = pure template absence) from a completely different identification strategy. Two orthogonal decomposition methods point to the same ratio.

**Plot:** `plots/publication/panel_b_quintiles_norm.pdf`

### Phase Facets: Template Loss Is a Transient Shock, Not a Persistent Handicap

Faceting the Q3-normalized plot by game phase (opening 1–12, middlegame 13–25, endgame 26+) reveals:

- **Opening**: Strong convergence — Q1 slopes down (−0.011/unit), Q5/Titled slope up (+0.005/unit). Lines fan inward. Template distance differentially compresses expertise.
- **Middlegame**: Lines are nearly **parallel** — convergence disappears. Skill spread is preserved; template distance no longer differentially compresses expertise. Positions have normalized by move 13.
- **Endgame**: Also parallel, wider CIs. No systematic convergence.

> [!important] Template loss is a transient shock — expertise compression does not cascade
> The non-tautological finding is NOT that templates matter in the opening (definitional), but that the expertise compression **does not propagate**. One could easily expect confusion in the opening to cascade — worse positions → harder middlegame decisions → compounding skill compression throughout the game. But it doesn't. By move 13, the expertise spread snaps back to standard-chess levels. The disruption is absorbed, not compounded. This is a claim about the *dynamics* of expertise under novelty, not a tautology about where templates apply.

**Key identification asset — the dose-response gradient:** The continuous variation in template distance (0–20 index) across 960 starting positions is the paper's strongest identification feature. Most 960 studies treat the format as binary (standard vs 960). The continuous measure provides:
1. **Within-960 graded transfer** — the slope, not just the intercept
2. **Expertise × displacement interaction** — convergence as a function of disruption dose
3. **Phase specificity** — the gradient only compresses expertise in the opening
4. **Piece-level decomposition** — which pieces drive the gradient (Gelbach channels)

This turns a natural experiment into something approaching a **dose-response design** — the strongest form of evidence for a causal channel, short of random assignment (which 960 actually provides, since starting positions are drawn uniformly).

**Plot:** `plots/publication/panel_b_quintiles_norm_phases.pdf`

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

1. **Fig 1** (`fig1_hero.pdf`): Single-panel template distance gradient — 3 skill tiers (Low <1600, Mid 1600-2000, High 2000+) with per-tier regression lines + binned diamond means (95% CI). Per-tier format offset arrows (+4/+7/+10 CPL). 11 vertical back-rank vignettes anchored at standard (d=0) and KQ swap (d=2). Raw CPL, template distance index (0-20) as x-axis. Marginal histogram showing game density across 960 starting positions. Gradient ≈ +0.5 CPL/unit distance, parallel across all tiers.
2. **Fig 2** (`fig2_theta3_phase.pdf`): Paired coefficient plot — theta3 (prep capital: R_std × 960, red circles) and theta4 (general skill: R_960 × 960, blue squares) across opening/middlegame/endgame phases. Prep advantage decays (*** → *** → n.s.); general skill transfers uniformly (*** → *** → n.s. but stable magnitude).
3. **Fig 3** (`fig3_calibration_panel.pdf`): Two-panel calibration figure — (a) per-player calibration shift violins by ELO tier (|eval_pv1−pv5| × time correlation, 960 minus standard), (b) error concentration by position quality × format (demanding/moderate/forgiving bars)

Generated by `scripts/publication_figures.py` + dev scripts, output to `plots/publication/`. Figures copied to `chess960Paper/figures/`.

## Nature Short Paper (`nature_short.tex`)

**Status:** Revised draft addressing reviewer feedback, pushed 2026-02-15.

**Key revisions:**
- Abstract: exact N=74,892 (was "over 80,000"); added "opening-phase" qualifier to expertise claim
- **Moves 1-12** as primary window throughout (was 2-12 in some places); move 1 justified as non-trivial in 960; moves 2-12 as robustness variant
- **Log transform rationale** added: log(CPL+1) stabilizes heavy-tailed distribution; figures show raw CPL for interpretability; robust to 7 alternative DVs
- **Figure 1**: single-panel hero with template distance gradient, 3 skill tiers, 11 back-rank vignettes, format offset arrows, marginal histogram. Caption fully rewritten.
- **Figure 2**: replaced BLUP scatter with theta3/theta4 paired coefficient plot by phase. Caption: θ3 decays +0.056*** → n.s.; θ4 stable at ~-0.05.
- **Figure 3**: normalized expertise rubric (unchanged)
- Moderated "reasoning alone" → "more reasoning-weighted and less template-dependent" for R960 proxy
- Removed obsolete panel references (fig:main a, fig:scatter)

See also: [[Research Open Ends]] for pending analyses and cross-project opportunities.

#chess960 #results
