# Freestyle Friday Data

## Overview

Chess.com's **Freestyle Friday** is a weekly Chess960 tournament for titled and strong players. It provides an elite complement to the main Lichess rapid dataset.

| Property | Value |
|----------|-------|
| Platform | Chess.com |
| Format | Chess960 (Freestyle) |
| Time control | 3+1 blitz |
| Structure | Swiss, 11 rounds |
| Frequency | Weekly (Fridays) |
| Participation | Open (not invite-only), but de facto tilted toward titled players |
| Period found | 44 tournaments discovered (via Hikaru, Magnus, Naroditsky histories) |
| Peak field | 476 players |
| Players discovered | 200 unique across all tournaments |
| Estimated total games | ~23K+ across all tournaments |

## Why This Complements the Main Study

The main dataset is Lichess rapid (10+0, 15+10). Two potential elite complements exist:

| | Freestyle Friday | Elite OTB (Weissenhaus etc.) |
|--|---|---|
| N games | ~23K | ~100-200 |
| Clock data | Yes | No |
| Time control | 3+1 blitz | 15+10 rapid / classical |
| Rating | Blitz (format-specific in-game) | FIDE (no 960 rating) |
| Player level | Titled + strong amateurs | Super-GMs only |
| Within-player std games | Fetchable from archive | Separate databases |
| Replicable analyses | Error composition, S-curve, anti-calibration | Barely powered |

### The Time-Control Argument

> [!important] Expertise compresses the time scale
> Template access is nearly automatic (System 1) for titled players — pattern recognition at GM level is sub-second. At 3+1, a GM is still fully engaging templates in standard chess, meaning the 960 disruption should be just as visible. A 1500-rated player might need 10 seconds to retrieve the same template a GM accesses in 200ms.

This means the "wrong" time control is mitigated by the expertise level. If anything, blitz may make the template disruption MORE visible among strong players, since they're more template-dependent.

## API Access

Chess.com PubAPI (read-only, JSON, no authentication required).

### Endpoints

1. **Tournament metadata:** `api.chess.com/pub/tournament/{slug}`
   - Returns: settings, player list, round URLs
   - Example slug: `freestyle-friday-january-24-2025-5384073`

2. **Tournament rounds:** `api.chess.com/pub/tournament/{slug}/{round}/{group}`
   - Returns: games (PGN + metadata) and player standings

3. **Player game archives:** `api.chess.com/pub/player/{username}/games/{year}/{month}`
   - Returns: all games for that month, filterable by `rules: "chess960"` and tournament tag
   - This is the primary collection path (tournament endpoint only exposes last round)

4. **Player stats:** `api.chess.com/pub/player/{username}/stats`
   - Returns: ratings by time class (blitz, rapid, bullet, etc.)
   - Note: `chess960_daily` exists but `chess960_blitz` does NOT — live 960 uses the regular blitz pool

### Rate Limiting

Chess.com API asks for reasonable usage. Include `User-Agent` header. Expect ~1 req/sec to be safe.

### Collection Strategy

1. Pull player lists from all tournament round endpoints (not just registered — actual participants from game data)
2. Deduplicate players across tournaments
3. Fetch monthly game archives for each player:
   - **All chess960 blitz games** (FF + non-tournament)
   - **Titled Tuesday standard blitz games** as control arm (capped at 100/player)
   - Standard blitz rating extracted from in-game data even when games aren't stored
4. Extract format-specific ratings from in-game data (median across games)
5. Store in separate `db/chesscom.db` (not mixed with Lichess data)

Estimated API calls: ~200 players × ~12 months ≈ 2400 archive calls ≈ 40 min at 1/sec.

### Analysis-Time Filtering

Prioritize games where **both players are in the FF pool** — this gives controlled opponent quality and bilateral rating data. Same logic applies to TT control games: TT games between two FF participants are the cleanest control.

## Data Properties

### Available in PGN

- Full move list with **clock data** (`[%clk h:mm:ss]`)
- Starting FEN (the 960 position)
- Player usernames and ratings (chess.com blitz)
- Result, termination reason
- Tournament tag linking back to the Freestyle Friday event

### NOT Available

- No engine evaluation in PGN (need to run Stockfish ourselves)
- No `accuracies` field in API response (despite chess.com having game review)

### In-Game Ratings Are Format-Specific

> [!important] Two-rating decomposition IS possible
> The chess.com `/stats` endpoint does NOT expose a live 960 blitz rating. However, in-game ratings (`WhiteElo`/`BlackElo` in PGN) ARE format-specific. Example: Magnus Carlsen shows 2896 in 960 blitz games vs 3301 in standard blitz games. The `/pub/leaderboards` endpoint confirms a `live_blitz960` category exists.
>
> We extract per-player median ratings from in-game data, separately for standard and chess960 format. This enables θ3 (prep capital interaction) analysis.

### Sample PGN

```
[Event "Live Chess - Chess960"]
[White "MagnusCarlsen"]
[Black "Oleksandr_Bortnyk"]
[WhiteElo "2919"]
[BlackElo "2866"]
[FEN "bbqnrkrn/pppppppp/8/8/8/8/PPPPPPPP/BBQNRKRN w GEge - 0 1"]
[TimeControl "180+1"]
[Variant "Chess960"]
[Tournament "https://www.chess.com/tournament/live/freestyle-friday-january-24-2025-5384073"]
1. e4 {[%clk 0:02:50]} e5 {[%clk 0:02:59]} ...
```

## Limitations for Our Design

1. **Blitz vs rapid**: different cognitive regime — but mitigated by expertise argument (see above)
2. **Selection**: Freestyle Friday players self-select into 960 → may have smaller format gaps (experienced 960 players)
3. **No Lichess overlap guarantee**: can't link chess.com accounts to Lichess accounts for cross-platform validation
4. **Rating pools differ**: chess.com blitz ratings are NOT comparable to Lichess rapid ratings — data must be stored and analyzed separately

## What CAN Be Replicated

- Error composition (catastrophe invariance, satisficing in forgiving positions)
- Reference-point clarity / S-curve (format gap by eval domain)
- Anti-calibration (time × complexity × format, since clock data is available)
- Template distance gradient (starting FEN → piece displacement)
- Within-960 graded transfer
- Complexity analysis (need to run Stockfish on the positions)
- **Two-rating decomposition (θ3)** — since in-game ratings are format-specific
- **Prep rent (R_std − R_960)** — derivable from median in-game ratings

## Data Storage

> [!warning] Separate from Lichess
> Chess.com data is stored in a dedicated `db/chesscom.db` — completely separate from the main Lichess database (`db/chess960.db`). Rating pools, time controls, and player populations differ between platforms. Analysis scripts should never mix cross-platform data without explicit harmonization.

## Status

Discovery complete: **44 tournaments, 200 players, 8636 participation records**.
Game fetching in progress. Script: `scraper/chesscom_collector.py`

```bash
# Check status
uv run python -m scraper.chesscom_collector --status

# Fetch games (long-running)
uv run python -m scraper.chesscom_collector --fetch-games

# Extract format-specific ratings from in-game data
uv run python -m scraper.chesscom_collector --extract-ratings
```

See also: [[Error Composition]], [[Research Design]], [[Key Results]]

#chess960 #data #chesscom #freestyle-friday
