# Sample & Inclusion Rules

## Overview

~70,196 games from 306 paired players on Lichess.

## Inclusion Criteria

### Players
- Must have games in **both** formats (standard AND chess960)
- Enables within-player comparison
- 300-game cap per player per format (equalizes influence)
- Result: ~36K standard / ~34K chess960

### Time Control
- **Rapid only** — no bullet, no blitz
- `time_control = 'rapid'`
- Consistent thinking time norms across formats

### Move Window
- **Primary**: moves 1-12 (opening phase)
- Move 1 included (non-trivial in Chess960; template features most exploitable)
- Stop at 12 (transition to middlegame)
- **Robustness**: moves 2-12 (excluding move 1)

### Move Filtering
```sql
WHERE m.centipawn_loss IS NOT NULL
  AND m.player_color = g.player_color  -- own moves only
  AND m.move_number BETWEEN 1 AND 12
HAVING COUNT(*) >= 10  -- min moves per game
```

The `HAVING >= 10` filter removes:
- Disconnects / early resignations
- "Didn't realize it's 960" games
- Requires 10 of 12 possible moves for reliable averages

### Time Data (when used)
```sql
AND m.time_spent IS NOT NULL
AND m.time_spent > 0
```

## Clock Coverage

- ~70% of rapid games have clock data overall
- Standard clock coverage: **~7%** (Lichess only exports clocks for some games)
- Cross-format time comparisons are suggestive only

## Balance

| | Standard | Chess960 |
|---|----------|----------|
| Games | ~36K | ~34K |
| Players | 306 | 306 |
| Mean CPL | 40.6 | 51.6 |

See also: [[Key Variables]], [[Database Schema]], [[Research Design]]

#chess960 #data
