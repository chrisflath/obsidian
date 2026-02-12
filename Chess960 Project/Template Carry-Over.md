# Template Carry-Over

## Research Question

Do players with narrow standard repertoires carry their habitual opening moves into Chess960? And does this help or hurt?

## Method

For each player×color, extract the top 2 most frequent move-1 choices in standard rapid games (HHI as concentration measure). Then check how often the same moves appear in their 960 games, and whether the CPL differs.

Data: 18,358 matched 960 move-1 observations across 333 player-color pairs (≥20 standard games, ≥10 960 games each).

## Key Findings

### 1. Template carry-over is substantial

Players play their standard top-2 moves in **27%** of 960 games. If moves were position-appropriate (random across legal options), this rate would be much lower (~4%).

| Metric | Value |
|--------|-------|
| Plays std top-1 move in 960 | 17.0% |
| Plays std top-2 move in 960 | 10.0% |
| Plays either top-1 or top-2 | 27.0% |

### 2. Repertoire concentration predicts carry-over

| Group | N | Std HHI | Std top-2% | 960 carry-over% | CPL template | CPL novel | Diff |
|-------|---|---------|-----------|-----------------|-------------|-----------|------|
| Broad (<P33) | 109 | 0.264 | 63.6% | 21.5% | 30.7 | 34.4 | -3.7 |
| Medium | 114 | 0.507 | 89.6% | 25.9% | 25.8 | 31.1 | -5.3 |
| Narrow (>P67) | 110 | 0.922 | 99.0% | 31.3% | 26.0 | 28.1 | -2.1 |

Correlations (N=333):
- std HHI vs 960 carry-over rate: **r = 0.199*** (p = 0.0003)
- std top-2 share vs 960 carry-over rate: **r = 0.231*** (p < 0.0001)

### 3. Position similarity is the key moderator

This is the critical interaction — template carry-over works near standard but degrades to mere habit as displacement grows:

| Position type | Carry-over rate | CPL template | CPL novel | Diff |
|--------------|----------------|-------------|-----------|------|
| Near-standard (fd ≤ 8) | **34.3%** | 21.0 | 27.7 | **-6.7** |
| Far-from-standard (fd > 14) | 23.2% | 32.3 | 32.0 | **+0.2** |

> [!important] The punchline
> Near standard positions: template moves **help** (-6.7 CPL). Far positions: template moves give **zero benefit** (+0.2 CPL). Template carry-over is rational near standard but degrades to mere habit as displacement grows.

### 4. Move quality varies dramatically

**White template moves in 960:**

| Move | Count | % of template | Avg CPL |
|------|-------|--------------|---------|
| e4 | 1,553 | 54.1% | 22.9 |
| d4 | 938 | 32.7% | 22.1 |
| c4 | 140 | 4.9% | 19.3 |
| Nf3 | 41 | 1.4% | 38.4 |

**Black template moves in 960:**

| Move | Count | % of template | Avg CPL |
|------|-------|--------------|---------|
| e5 | 945 | 45.1% | 29.3 |
| d5 | 618 | 29.5% | 28.8 |
| Nf6 | 87 | 4.2% | 40.7 |
| c6 | 37 | 1.8% | 45.6 |
| d6 | 35 | 1.7% | 59.3 |

Central pawn pushes (e4, d4, e5, d5) are general-purpose heuristics that work reasonably across positions. Position-specific moves (Nf6, c6, d6) are terrible when carried over — these rely on piece configuration that doesn't exist in 960.

## Interpretation

Template carry-over operates at two levels:
1. **Surface level (move 1):** General heuristics (central pawns) transfer well — they're good moves in most positions
2. **Structural level (subsequent development):** Templates break down — where to develop pieces, castling plans, pawn structure all depend on the specific 960 position

The position-similarity interaction directly supports the **graded transfer** story: the template distance gradient isn't just about *missing* knowledge, it's about *misapplied* knowledge. Near-standard positions allow partial template reuse; far positions render templates useless.

This also connects to [[Error Composition]]: the format gap comes from mid-range errors (mistakes, blunders), not catastrophes. Template carry-over at the surface level prevents catastrophes (e4 is never terrible), but the structural mismatch generates the costly mid-range errors in subsequent moves.

## Within-player CPL test

Playing your standard move in 960 overall **saves 3.2 CPL** (t=-2.95, p=0.003, N=357). But this is driven entirely by near-standard positions; in far positions, the benefit vanishes.

See also: [[Gelbach Decomposition]], [[Error Composition]], [[Key Results]]

#chess960 #methods #template-transfer
