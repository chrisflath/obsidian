# Key Variables

## Dependent Variable

| Variable | Formula | Notes |
|----------|---------|-------|
| `mean_log_cpl` | `mean(log(CPL + 1))` per game | Log handles skew, +1 handles zeros |

## Treatment

| Variable | Definition | Notes |
|----------|------------|-------|
| `is_960` | `format == 'chess960'` | Binary treatment indicator |

## Position Controls

| Variable | Definition | Notes |
|----------|------------|-------|
| `file_distance` | Sum of piece displacement from SP 518 | Z-scored; from `chess960_position_metrics` |
| `lopsidedness` | \|starting position eval\| | Z-scored; asymmetry of position |
| `kq_same_color` | King and queen on same color square | Binary |
| `has_unprotected` | Any unprotected pawns in starting position | Binary (0/1); key contrast is std=always 0 vs 960=sometimes 1 |
| `delta_bishops` | Bishop displacement from standard squares | Piece-level decomposition |
| `delta_queen` | Queen displacement | Piece-level decomposition |
| `delta_rooks` | Rook displacement | Piece-level decomposition |
| `delta_king` | King displacement | Piece-level decomposition |
| `delta_knights` | Knight displacement | Piece-level decomposition |

## Rating Variables

| Variable | Definition | Notes |
|----------|------------|-------|
| `R_std_z` | Z-scored standard rating | From `players.standard_rating` |
| `R_960_z` | Z-scored chess960 rating | From `players.chess960_rating` |
| `prep_rent` | `R_std - R_960` | Proxy for prep capital value |
| `specialist_ratio` | `R_960 / R_std` | Higher = more 960-adapted |

## Time Variables

| Variable | Definition | Notes |
|----------|------------|-------|
| `log_time` | `log(time_spent + 0.1)` | Z-scored within time control |
| `clock_remaining` | Pre-move clock (seconds) | State variable, not post-treatment |

## Complexity Variables

From [[Complexity Analysis]] (MultiPV):

| Variable | Definition | Notes |
|----------|------------|-------|
| `complexity_1v2` | \|eval(best) - eval(2nd best)\| | **Primary measure**; small = hard |
| `share_good_top5` | Fraction of top 5 within 50cp of best | Strongest predictor |
| `num_legal_moves` | Count of legal moves | Positional breadth |

> [!warning] Do NOT use `|eval_before|` as complexity
> This measures position imbalance (who's winning), not decision difficulty.

See also: [[Research Design]], [[Database Schema]], [[Complexity Analysis]]

#chess960 #variables
