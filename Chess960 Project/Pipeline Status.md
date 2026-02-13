# Pipeline Status (2026-02-13)

## Infrastructure Fixes This Session

### FEN Cache Pollution Fix
- **Problem**: Chess.com MultiPV analyzer defaulted to 0.1s/position (vs Lichess 0.5s), producing depth ~11 vs Lichess ~13.5
- **Impact**: ~24K low-depth entries polluted the shared FEN cache
- **Fix 1**: Changed default time-limit to 0.5s in `chesscom_complexity.py`
- **Fix 2**: Changed `INSERT OR IGNORE` to `ON CONFLICT DO UPDATE WHERE excluded.depth > fen_complexity.depth` — higher depth always wins
- **Fix 3**: Purged ~24K recent low-depth entries, cleared chess.com position_complexity, restarted
- **Result**: Chess.com MultiPV now runs at avg depth 13.0, matching Lichess 13.5

### SQLite Concurrent Access Fix
- **Problem**: Both Lichess and chess.com MultiPV analyzers write to shared `fen_cache.db`, causing `database is locked` crashes
- **Fix**: Added 5-attempt retry with exponential backoff (5s, 10s, 15s, 20s, 25s) to `save_complexity_batch()` in `stockfish_runner.py`
- DB already had WAL mode + 30s busy_timeout; retry handles edge cases

## Current Data Status

### Lichess (db/chess960.db)
- Games: 115,640 chess960 / 148,396 standard
- Analyzed: 26,605 (23%) / 60,834 (41%)
- MultiPV: 1.98M positions, avg depth 13.5

### Chess.com (db/chesscom.db)
- Games: 21,085 chess960 / 88,741 standard
- Analyzed: 4,541 (22%) / 5,604 (6%)
- MultiPV: 79,500 positions, avg depth 13.0

### Shared FEN Cache
- 1.43M entries in fen_cache.db

## Running Processes
- Lichess MultiPV (3 workers × 2 threads, 0.5s)
- Chess.com MultiPV (2 workers × 2 threads, 0.5s)
- Chess.com engine analysis
