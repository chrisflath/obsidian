# Start-Position Fixed Effects

## Purpose

Test whether the format gap is driven by specific starting positions being harder, rather than the absence of templates per se.

## Method: Frisch-Waugh-Lovell (FWL) Demeaning

Include a fixed effect for each of the 960 starting positions. This absorbs **all** between-SP variation — difficulty, asymmetry, piece placement, everything.

## Results

| Specification | is_960 coefficient | R-squared |
|---------------|-------------------|-----------|
| Without SP FE | +0.1757*** | 0.395 |
| With SP FE | +0.1034* | 0.410 |
| **Reduction** | **41.2%** | |

## Interpretation

- 41% of the format gap is explained by SP heterogeneity (some positions are inherently harder)
- **59% survives** after absorbing all SP-level variation
- The residual gap reflects the **absence of templates**, not position difficulty
- SP FE explains Delta-R-squared = 0.035 more variance than `file_distance` alone — displacement is a useful but incomplete summary of SP difficulty

## Relationship to Gelbach

The [[Gelbach Decomposition]] decomposes the 41% into interpretable pieces:
- Piece displacement accounts for 28.4%
- Structural features (K-Q color, unprotected pawns) account for 8.2%

See also: [[Gelbach Decomposition]], [[Key Results]]

**Script**: `analysis/two_rating_decomposition.py`

#chess960 #methods #identification
