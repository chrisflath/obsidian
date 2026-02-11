# Complexity Analysis

## Motivation

Need to disentangle "Chess960 positions are harder to play" from "Chess960 removes templates." Position complexity is a potential confound.

> [!warning] Do NOT use |eval_before| as complexity
> |eval_before| measures who's winning (position imbalance), not how hard the decision is.

## Method: MultiPV

Run Stockfish with `MultiPV=5` to get the top 5 moves and their evaluations.

### Measures

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| `complexity_1v2` | \|eval(best) - eval(2nd best)\| | **Primary**. Small gap = hard decision |
| `complexity_1v3` | \|eval(best) - eval(3rd best)\| | Broader measure |
| `share_good_top5` | Fraction of top 5 within 50cp of best | How many "reasonable" moves exist |
| `num_legal_moves` | Count of legal moves | Positional breadth |

### Interpretation
- **Small gap** (e.g., 5 cp): hard decision, multiple good options
- **Large gap** (e.g., 100 cp): easy decision, one clearly best move

## Sampling Strategy (Tiered)

| Phase | Move range | Strategy | Plies per game |
|-------|-----------|----------|----------------|
| Phase 1 | Moves 1-10 | Complete coverage | 20 |
| Phase 2 | Moves 11-20 | 4 random samples | 4 |
| Phase 3 | Moves 21-40 | 3 random samples | 3 |

Deterministic hash seeding by `(game_id, ply)` for reproducibility. Ply-uniform sampling (equal white/black).

## Descriptives by Format (N=65,586)

| Metric | Chess960 | Standard |
|--------|----------|----------|
| CPL (mean) | 51.6 | 40.6 |
| complexity_1v2 | 40.3 | 44.5 |
| num_legal_moves | 28.6 | 30.7 |
| share_good_top5 | 0.68 | 0.69 |

Chess960 positions are actually *slightly less* complex by these measures, ruling out difficulty as the explanation.

## Regression Results

| Variable | Coef | SE | p |
|----------|------|-----|---|
| Intercept | 41.45 | 0.50 | *** |
| is_960 | **+9.11** | 0.74 | *** |
| complexity_z | -1.59 | 0.26 | *** |
| num_moves_z | +6.94 | 0.32 | *** |
| share_good_z | **-12.79** | 0.35 | *** |
| elo_z | -10.60 | 0.29 | *** |
| share_good_z x num_moves_z | -0.09 | 0.30 | n.s. |

R-squared = 0.082

### Key Takeaways
1. Format effect **persists** (+9.1 cp) after controlling for all complexity measures
2. `share_good_top5` is the strongest predictor (-12.8 cp/SD)
3. Complexity effects are **additive**, not multiplicative (interaction is null)

## Progress

~236K of ~1.5M positions analyzed. Running with `--workers 5 --threads 2`.

## Running

```bash
uv run python -m analysis.complexity_analyzer \
  --batch 500 --multipv 5 --time-limit 0.5 \
  --threads 2 --workers 5
```

Table: `position_complexity` (see [[Database Schema]])

See also: [[Key Variables]], [[Key Results]]

**Script**: `analysis/complexity_analyzer.py`

#chess960 #methods #complexity
