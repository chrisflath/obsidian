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

## Design Decisions

- `has_unprotected` is binary (0/1) not count (0-3): the key contrast is standard (always 0) vs 960 (sometimes >0)
- Clock = pre-move clock remaining (state variable, not a post-treatment mediator)
- SP FE variant: 31.5% explained by all SP heterogeneity, 68.5% residual

## Visualization

Panel C of the hero figure (`fig1_hero.pdf`) shows a waterfall chart of these contributions.

See also: [[Start-Position Fixed Effects]], [[Key Variables]], [[Key Results]]

**Script**: `scripts/publication_figures.py` (fig1_panel_c)

#chess960 #methods #decomposition
