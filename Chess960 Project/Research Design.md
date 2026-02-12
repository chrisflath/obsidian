# Research Design

## Research Question

What is the magnitude of the template-applicability advantage in expert decision-making?

## Natural Experiment

Chess960 (Fischer Random) randomizes the starting position of pieces on the back rank (960 possible arrangements). This disables memorized opening theory — the "template" — while leaving all other aspects of the game intact.

## Identification Strategy

**Within-player comparison**: the same player in standard chess vs Chess960.
- Player random intercepts absorb all time-invariant player characteristics (talent, experience, motivation)
- The treatment `is_960` captures the format effect
- Any remaining gap after controls reflects the value of preparation capital

## Key Contrast

| | Standard | Chess960 |
|---|----------|----------|
| Opening theory | Fully applicable | Inapplicable |
| Tactical/strategic skill | Same | Same |
| Player | Same person | Same person |

## Primary Specification

```
Y_g = beta * is_960 + X_g * gamma + u_i + epsilon_g
```

Where:
- `Y_g` = `mean(log(CPL + 1))` per game (moves 1-12)
- `is_960` = binary treatment
- `X_g` = controls (ratings, position features)
- `u_i` = player random intercept
- `epsilon_g` = game-level error

**Standard errors**: player-clustered (primary), SP-clustered (robustness)

## Why This Works

1. **Same players** in both formats — no selection on ability
2. **Same time control** (rapid only) — no confound from thinking time norms
3. **Same platform** (Lichess) — identical interface, engine, rating system
4. **Opening phase only** (moves 1-12) — where templates are most relevant

## Data Sources

| Source | Format | Time control | Players | N games | Status |
|--------|--------|-------------|---------|---------|--------|
| **Lichess** (primary) | Rapid | 10+0, 15+10 | 345 paired | ~70K | Complete |
| **Freestyle Friday** (complement) | Blitz | 3+1 | ~500 titled | ~23K | Planned |

See [[Freestyle Friday Data]] for the elite blitz complement.

See also: [[Key Variables]], [[Sample & Inclusion Rules]], [[Two-Rating Decomposition]]

#chess960 #methods
