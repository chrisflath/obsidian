# Error Contagion

## Core Question

Does an opponent's error raise your error probability? Is this contagion effect different between formats? How does skill moderate it?

Data: consecutive half-moves by different players, moves 1–12, rapid, paired. ~1.35M standard transitions, ~579K chess960 transitions.

## Contagion Effect

| | Standard | Chess960 |
|---|---|---|
| Error rate after opp clean move | 18.8% | 29.2% |
| Error rate after opp error (CPL≥50) | 42.0% | 45.0% |
| **Contagion (Δ)** | **+23.2pp** | **+15.8pp** |
| Mean CPL after opp clean | 32.0 | 43.2 |
| Mean CPL after opp error | 73.3 | 71.0 |
| **CPL contagion (Δ)** | **+41.2** | **+27.8** |

Both t-tests p≈0. Contagion is **stronger in standard** (+23.2pp vs +15.8pp), but this is a ceiling effect: 960 baseline is already 29.2% (vs 18.8%), leaving less room for contagion. In relative terms: standard = 2.2x multiplier, 960 = 1.5x multiplier.

> [!important] Templates provide baseline resilience but create fragility when disrupted
> Standard players operate at a low error floor thanks to templates, but when the opponent's error pushes them off-book, the jump is larger. 960 players already operate without that floor, so marginal impact of opponent errors is smaller.

### By Trigger Severity

| Trigger | Std err% after | 960 err% after | Std Δ from base | 960 Δ from base |
|---------|---------------|---------------|-------|-------|
| Inaccuracy (50–100) | 37.8% | 42.6% | +19.0pp | +13.4pp |
| Mistake (100–300) | 48.2% | 49.0% | +29.4pp | +19.9pp |
| Blunder (300+) | 42.3% | 41.2% | +23.5pp | +12.1pp |

After opponent blunders, 960 players actually err slightly less (41.2% vs 42.3%) — the vigilance effect.

## Contagion by ELO Tier

| ELO | Std base | Std after err | Std contagion | 960 base | 960 after err | 960 contagion |
|-----|---------|--------------|--------------|---------|--------------|--------------|
| < 1500 | 28.3% | 46.8% | +18.5pp | 37.6% | 49.3% | +11.7pp |
| 1500–1800 | 22.4% | 41.9% | +19.6pp | 33.3% | 46.4% | +13.0pp |
| 1800–2100 | 16.6% | 36.6% | +20.0pp | 27.4% | 42.5% | +15.1pp |
| 2100+ | 8.7% | 32.4% | **+23.7pp** | 19.6% | 39.3% | **+19.6pp** |

> [!note] Stronger players are MORE susceptible to contagion
> 2100+ go from 8.7% to 32.4% (3.7x multiplier) in standard. Weaker players go from 28.3% to 46.8% (1.7x). Strong players have more to lose from template disruption, so the relative shock is larger. In 960, the same gradient exists but is compressed because baselines are higher.

### Capitalization by ELO (% best/good after opp mistake/blunder)

| ELO | Std capitalize | 960 capitalize | Δ |
|-----|---------------|---------------|---|
| < 1500 | 49.3% | 49.2% | -0.2pp |
| 1500–1800 | 52.9% | 50.9% | -2.1pp |
| 1800–2100 | 58.1% | 53.8% | -4.3pp |
| 2100+ | 61.7% | 56.5% | **-5.3pp** |

Weaker players capitalize at the same rate regardless of format (templates aren't helping them exploit errors). Stronger players lose 5.3pp of capitalization in 960 — they have the tactical skill to punish errors in standard but lack template context to recognize opportunities as efficiently in 960. This is the prep-capital story: the higher the skill, the more you lean on templates for both consistency and exploitation.

## Full Transition Matrix

### Standard (opponent move → your response)

| Opp ↓ / You → | Best | Good | Inacc | Mistake | Blunder | N |
|---|--:|--:|--:|--:|--:|--:|
| Best | 23.6% | 62.3% | 8.5% | 4.7% | 0.8% | 191,994 |
| Good | 13.2% | 66.9% | 12.3% | 6.5% | 1.1% | 847,090 |
| Inaccuracy | 10.4% | 51.8% | 22.3% | 13.6% | 1.9% | 171,933 |
| Mistake | 9.1% | 42.7% | 15.7% | 27.7% | 4.8% | 113,823 |
| Blunder | 8.2% | 49.5% | 5.9% | 13.3% | 23.1% | 22,260 |

### Chess960

| Opp ↓ / You → | Best | Good | Inacc | Mistake | Blunder | N |
|---|--:|--:|--:|--:|--:|--:|
| Best | 19.1% | 56.5% | 15.0% | 8.3% | 1.1% | 72,442 |
| Good | 12.0% | 57.6% | 18.9% | 10.3% | 1.1% | 311,512 |
| Inaccuracy | 10.3% | 47.2% | 25.1% | 16.1% | 1.4% | 110,256 |
| Mistake | 10.3% | 40.7% | 17.3% | 28.3% | 3.5% | 74,900 |
| Blunder | 9.1% | 49.6% | 5.8% | 14.7% | 20.7% | 9,654 |

### Δ (960 − Standard)

| Opp ↓ / You → | Best | Good | Inacc | Mistake | Blunder |
|---|--:|--:|--:|--:|--:|
| Best | -4.4 | -5.8 | **+6.5** | **+3.6** | +0.2 |
| Good | -1.2 | **-9.3** | **+6.5** | **+3.8** | +0.1 |
| Inaccuracy | -0.1 | -4.6 | +2.7 | +2.6 | -0.5 |
| Mistake | +1.2 | -2.0 | +1.5 | +0.5 | -1.2 |
| Blunder | +1.0 | +0.0 | -0.0 | +1.4 | **-2.4** |

### Key Findings

1. **Top two rows** (after opp Best/Good): massive shift from Good → Inaccuracy/Mistake (+6.5pp each). Templates keep you clean in routine play.
2. **Bottom two rows** (after opp Mistake/Blunder): differences are small and mixed. Once things go sideways, templates don't help.
3. **Blunder→Blunder is -2.4pp**: 960 players are *more composed* after opponent disasters.
4. **Capitalization rate after opp error**: nearly identical (52.8% std vs 51.8% 960). Templates don't help you *punish* errors.
5. **Good→Good rate**: 81.2% std vs 70.8% 960 (-10.4pp). The entire format gap lives in routine positions.

> [!important] The format gap lives in normal play, not in crisis management
> After opponent plays Best/Good, standard players respond with Best/Good 81.2% of the time vs 70.8% in 960. After opponent mistakes/blunders, capitalization rates are virtually identical (~52%). Templates are a consistency tool for routine positions, not an exploitation tool for crises.

See also: [[Error Composition]], [[Game Volatility]], [[Eval-Sign Classification]], [[Key Results]]

#chess960 #mechanism #contagion #errors
