# Gelbach Decomposition

## Purpose

Decompose the format gap into interpretable channels. Uses OLS with player FE dummies for an exact accounting identity: the sum of channel contributions equals the total gap reduction.

## Setup

- **Base model**: `Y = beta_base * is_960 + player_FE`
- **Full model**: adds piece displacements, structural features, clock, matchmaking
- `beta_base = 0.1554`, `beta_full = 0.1000`
- **Total explained**: 0.0555 (35.7% of gap)

## Decomposition

### Piece Displacement (28.4% of gap)

| Piece | Contribution | % of gap | Interpretation |
|-------|-------------|----------|----------------|
| Bishops | +0.0240 | +15.4% | Largest contributor — displaced bishops hardest to develop |
| Queen | +0.0183 | +11.8% | Non-standard queen placement disrupts plans |
| Rooks | +0.0062 | +4.0% | Moderate effect |
| King | +0.0054 | +3.5% | King safety changes |
| Knights | -0.0096 | -6.2% | Displacement *helps* — better squares than g1/b1 |

> [!info] Knights are the exception
> Displaced knights often land on better squares than their standard g1/b1 positions, making the opening slightly easier along this dimension.

### Structural Features (8.2% of gap)

| Feature | Contribution | % of gap |
|---------|-------------|----------|
| Unprotected pawns | +0.0070 | +4.5% |
| K-Q same color | +0.0058 | +3.7% |

### Other Channels

| Channel | Contribution | % of gap | Notes |
|---------|-------------|----------|-------|
| Lopsidedness | -0.0041 | -2.6% | Lopsided positions slightly *easier* |
| Matchmaking | +0.0009 | +0.6% | \|R_opp - R_own\| |
| Clock state | +0.0017 | +1.1% | Player clock positive, opponent clock negative (-1.3%) |

### Residual

**0.1000 (64.3% of gap)** — the pure template-absence effect that cannot be attributed to any observable position feature.

## Chess.com Elite Replication (Updated: N=5,182 games, 252 players)

Cross-platform replication using Freestyle Friday (960 blitz 3+1) vs Titled Tuesday (standard blitz 3+1). Updated results with full engine analysis: N=5,182 games (2,481 chess960, 2,701 standard), 252 paired players, 100-game cap per player per format.

### Base and Full Model

| | Chess.com (blitz) | Lichess (rapid) |
|--|--|--|
| β_base | **+0.2910*** | +0.1554*** |
| β_full | **+0.1705*** | +0.1000 |
| Total explained | **41.4%** | 35.7% |
| Residual | **58.6%** | 64.3% |

The format gap is ~1.87x larger on chess.com (0.291 vs 0.155), consistent with elite blitz — time pressure amplifies template loss. The *share* explained by position features is slightly higher in the elite sample (41% vs 36%).

### Piece Displacement (31.9% of gap)

| Piece | Contribution | % of gap | Lichess % |
|-------|-------------|----------|-----------|
| Queen | +0.0494 | **+17.0%** | +11.8% |
| Bishops | +0.0286 | **+9.8%** | +15.4% |
| King | +0.0119 | +4.1% | +3.5% |
| Knights | +0.0090 | +3.1% | -6.2% |
| Rooks | -0.0062 | -2.1% | +4.0% |

> [!info] Queen overtakes bishops in elite sample
> Queen displacement is the single largest contributor at 17.0% (vs 11.8% Lichess). This may reflect elite players' heavier reliance on queen-placement-dependent opening plans. Bishops drop to 9.8% (from 15.4%), while knights flip from negative (-6.2%) to positive (+3.1%).

### Structural Features (8.6% of gap)

| Feature | Contribution | % of gap | Lichess % |
|---------|-------------|----------|-----------|
| Unprotected pawns | +0.0232 | +8.0% | +4.5% |
| K-Q same color | +0.0018 | +0.6% | +3.7% |

> [!note] Unprotected pawns more important for elites
> Unprotected pawns nearly double in importance (8.0% vs 4.5%), suggesting titled players are more sensitive to pawn structure vulnerabilities created by non-standard piece placement.

### Other Channels

| Channel | Contribution | % of gap | Lichess % |
|---------|-------------|----------|-----------|
| Lopsidedness | -0.0018 | -0.6% | -2.6% |
| Matchmaking | +0.0045 | +1.5% | +0.6% |
| Clock state | +0.0000 | +0.0% | +1.1% |

Clock state is zero because chess.com PGN clock data has not been extracted to move_metrics yet.

### Cross-Platform Summary

The decomposition structure replicates well across platforms:
- **Queen and bishops** are the top two positive piece contributors on both platforms
- **~59–64% residual** on both platforms = irreducible template loss
- Structural features (unprotected pawns, K-Q same color) contribute ~8-9% on both
- Lopsidedness is a mild suppressor on both (lopsided positions are slightly easier)
- Queen displacement is amplified in the elite sample (+17% vs +12%)

**Script**: Inline analysis using `db/chesscom.db` with backfilled SP numbers from FEN parsing.

## Design Decisions

- `has_unprotected` is binary (0/1) not count (0-3): the key contrast is standard (always 0) vs 960 (sometimes >0)
- Clock = pre-move clock remaining (state variable, not a post-treatment mediator)
- SP FE variant: 31.5% explained by all SP heterogeneity, 68.5% residual

## Visualization

Panel C of the hero figure (`fig1_hero.pdf`) shows a waterfall chart of these contributions.

See also: [[Start-Position Fixed Effects]], [[Key Variables]], [[Key Results]]

**Script**: `scripts/publication_figures.py` (fig1_panel_c)

#chess960 #methods #decomposition
