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
| Period found | Jan 2025 – Oct 2025 (19 tournaments via Hikaru's history) |
| Peak field | 476 players |
| Estimated total games | ~23K across all tournaments |

## Why This Complements the Main Study

The main dataset is Lichess rapid (10+0, 15+10). Two potential elite complements exist:

| | Freestyle Friday | Elite OTB (Weissenhaus etc.) |
|--|---|---|
| N games | ~23K | ~100-200 |
| Clock data | Yes | No |
| Time control | 3+1 blitz | 15+10 rapid / classical |
| Rating | Blitz (pooled, no separate 960) | FIDE (no 960 rating) |
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

1. Pull player lists from all 19 tournament endpoints
2. Deduplicate players across tournaments
3. Fetch monthly game archives, filter for `rules: chess960` + tournament tag
4. Also fetch standard blitz games for within-player pairing
5. Store in same DB schema (or parallel table with `source='chess.com'`)

Estimated API calls: ~500 players × ~12 months × 2 (960 + std) ≈ 12K calls ≈ 3-4 hours at 1/sec.

## Data Properties

### Available in PGN

- Full move list with **clock data** (`[%clk h:mm:ss]`)
- Starting FEN (the 960 position)
- Player usernames and ratings (chess.com blitz)
- Result, termination reason
- Tournament tag linking back to the Freestyle Friday event

### NOT Available

- No engine evaluation in PGN (need to run Stockfish ourselves)
- No separate Chess960 rating (pooled blitz rating)
- No `accuracies` field in API response (despite chess.com having game review)
- Player standard blitz games need separate collection

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

1. **No two-rating decomposition**: chess.com pools 960 into regular blitz rating → θ3 analysis impossible
2. **No prep rent**: can't compute R_std − R_960 without separate ratings
3. **Blitz vs rapid**: different cognitive regime — but mitigated by expertise argument
4. **Selection**: Freestyle Friday players self-select into 960 → may have smaller format gaps (experienced 960 players)
5. **No Lichess overlap guarantee**: can't link chess.com accounts to Lichess accounts for cross-platform validation

## What CAN Be Replicated

- Error composition (catastrophe invariance, satisficing in forgiving positions)
- Reference-point clarity / S-curve (format gap by eval domain)
- Anti-calibration (time × complexity × format, since clock data is available)
- Template distance gradient (starting FEN → piece displacement)
- Within-960 graded transfer
- Complexity analysis (need to run Stockfish on the positions)

## Status

Not yet collected. See [[Analysis Pipeline]] for collection scripts when built.

See also: [[Error Composition]], [[Research Design]], [[Key Results]]

#chess960 #data #chesscom #freestyle-friday
