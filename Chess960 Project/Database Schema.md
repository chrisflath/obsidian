# Database Schema

SQLite database at `db/chess960.db`.

## Core Tables

### `games`
Game-level metadata.

| Column | Type | Notes |
|--------|------|-------|
| `id` | INTEGER | Primary key |
| `player_username` | TEXT | Lichess username |
| `format` | TEXT | `'standard'` or `'chess960'` |
| `time_control` | TEXT | `'rapid'`, `'blitz'`, etc. |
| `chess960_position` | INTEGER | SP number (0-959), NULL for standard |
| `player_color` | TEXT | `'white'` or `'black'` |
| `opponent_rating` | INTEGER | |
| `pgn` | TEXT | Full PGN string |
| `played_at` | TEXT | ISO timestamp |
| `result` | TEXT | Game result |
| `analyzed_at` | TEXT | NULL = unanalyzed, sentinel = claimed |

### `move_metrics`
Per-move Stockfish analysis.

| Column | Type | Notes |
|--------|------|-------|
| `game_id` | INTEGER | FK to `games.id` |
| `move_number` | INTEGER | |
| `player_color` | TEXT | `'white'` or `'black'` |
| `centipawn_loss` | REAL | CPL for this move |
| `eval_before` | INTEGER | Position eval before move (White POV, centipawns) |
| `eval_after` | INTEGER | Position eval after move |
| `best_move_uci` | TEXT | Engine's best move |
| `time_spent` | REAL | Seconds spent on move |
| `clock_time_remaining` | REAL | Pre-move clock (seconds) |
| `game_phase` | TEXT | `'opening'`, `'middlegame'`, `'endgame'` |
| `analysis_depth` | INTEGER | Stockfish depth reached |

### `players`
Player-level data.

| Column | Type | Notes |
|--------|------|-------|
| `username` | TEXT | Primary key |
| `standard_rating` | INTEGER | Lichess standard rapid rating |
| `chess960_rating` | INTEGER | Lichess chess960 rating |

### `chess960_position_metrics`
Per-SP structural features (960 rows).

| Column | Type | Notes |
|--------|------|-------|
| `position_number` | INTEGER | SP 0-959 |
| `file_distance` | REAL | Total piece displacement from SP 518 |
| `lopsidedness_cp` | REAL | \|starting eval\| in centipawns |
| `n_unprotected` | INTEGER | Count of unprotected pawns (0-3) |
| `kq_same_color` | INTEGER | Boolean: K and Q on same color |
| `delta_rooks` | REAL | Rook displacement |
| `delta_bishops` | REAL | Bishop displacement |
| `delta_knights` | REAL | Knight displacement |
| `delta_king` | REAL | King displacement |
| `delta_queen` | REAL | Queen displacement |

### `position_complexity`
MultiPV analysis results (see [[Complexity Analysis]]).

| Column | Type | Notes |
|--------|------|-------|
| `game_id` | INTEGER | FK to `games.id` |
| `move_number` | INTEGER | |
| `player_color` | TEXT | |
| `multipv_level` | INTEGER | Number of PVs computed |
| `eval_pv1`-`eval_pv5` | INTEGER | Eval for each PV (centipawns) |
| `mate_pv1`-`mate_pv5` | INTEGER | Mate-in-N for each PV |
| `complexity_1v2` | REAL | \|pv1 - pv2\| |
| `complexity_1v3` | REAL | \|pv1 - pv3\| |
| `complexity_avg` | REAL | Mean dropoff across PVs |
| `num_legal_moves` | INTEGER | Legal move count |
| `analysis_depth` | INTEGER | Depth reached |

## Key Joins

```sql
-- Game-level analysis with position features
SELECT g.*, pm.file_distance, pm.lopsidedness_cp
FROM games g
LEFT JOIN chess960_position_metrics pm
  ON g.chess960_position = pm.position_number

-- Move-level with complexity
SELECT m.*, pc.complexity_1v2, pc.share_good_top5
FROM move_metrics m
LEFT JOIN position_complexity pc
  ON m.game_id = pc.game_id
  AND m.move_number = pc.move_number
  AND m.player_color = pc.player_color
```

See also: [[Sample & Inclusion Rules]], [[Key Variables]]

#chess960 #data #schema
