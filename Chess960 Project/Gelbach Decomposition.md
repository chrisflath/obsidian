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

## Chess.com Elite Replication (Preliminary)

Cross-platform replication using Freestyle Friday (960 blitz 3+1) vs Titled Tuesday (standard blitz 3+1). Preliminary results from N=510 games (312 960, 198 std), 29 paired players. Analysis will sharpen as engine analysis progresses toward ~15K games.

### Base and Full Model

| | Chess.com (blitz) | Lichess (rapid) |
|--|--|--|
| β_base | **+0.7384*** | +0.1554*** |
| β_full | **+0.4450** | +0.1000 |
| Total explained | **39.7%** | 35.7% |
| Residual | **60.3%** | 64.3% |

The format gap is ~4.75x larger on chess.com, consistent with elite blitz — time pressure amplifies template loss. But the *share* explained by position features is remarkably similar (~36-40%).

### Piece Displacement (34.2% of gap)

| Piece | γ (full) | δ (gap) | Contribution | % of gap | Lichess % |
|-------|----------|---------|-------------|----------|-----------|
| Queen | +0.075** | +1.96 | +0.148 | **+20.0%** | +11.8% |
| King | +0.090** | +1.36 | +0.123 | **+16.6%** | +3.5% |
| Bishops | +0.035 | +3.02 | +0.104 | **+14.1%** | +15.4% |
| Rooks | -0.048* | +2.50 | -0.121 | **-16.3%** | +4.0% |
| Knights | -0.000 | +2.97 | -0.001 | -0.1% | -6.2% |

> [!note] Small-sample caution
> With only 29 paired players, individual piece estimates are noisy. King (+16.6%) and rooks (-16.3%) differ from Lichess and will likely stabilize as N grows. Queen (+20.0%) and bishops (+14.1%) already align well.

### Structural Features (10.2% of gap)

| Feature | Contribution | % of gap | Lichess % |
|---------|-------------|----------|-----------|
| Unprotected pawns | +0.050 | +6.8% | +4.5% |
| K-Q same color | +0.025 | +3.4% | +3.7% |

### Other Channels

| Channel | Contribution | % of gap | Lichess % |
|---------|-------------|----------|-----------|
| Lopsidedness | -0.046 | -6.3% | -2.6% |
| Matchmaking | +0.011 | +1.5% | +0.6% |

### Cross-Platform Summary

The decomposition structure replicates strikingly well:
- **Queen and bishops** are consistently the top positive contributors on both platforms
- **~60% residual** on both platforms = irreducible template loss
- Structural features (unprotected pawns, K-Q same color) contribute ~8-10% on both
- Lopsidedness is a suppressor on both (positions with unequal starting evals are slightly easier)

**Status**: Preliminary (N=510). Chess.com engine analysis running at ~360 games/hr. Full sample (~15K paired games) expected to take ~80 hours. Results will be updated as data accumulates.

**Script**: Inline analysis (to be formalized when chess.com analysis completes).

## Design Decisions

- `has_unprotected` is binary (0/1) not count (0-3): the key contrast is standard (always 0) vs 960 (sometimes >0)
- Clock = pre-move clock remaining (state variable, not a post-treatment mediator)
- SP FE variant: 31.5% explained by all SP heterogeneity, 68.5% residual

## Visualization

Panel C of the hero figure (`fig1_hero.pdf`) shows a waterfall chart of these contributions.

See also: [[Start-Position Fixed Effects]], [[Key Variables]], [[Key Results]]

**Script**: `scripts/publication_figures.py` (fig1_panel_c)

#chess960 #methods #decomposition
