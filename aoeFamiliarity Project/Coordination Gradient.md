# Coordination Gradient

Part of [[aoeFamiliarity Project]] | Identification Test

**Script:** `id_coordination_gradient.py`

## Logic

If TPE captures coordination skill, its importance should **scale with coordination demands**. The progression from 1v1 (no teammates) through 2v2, 3v3, to 4v4 (three teammates) provides a natural dose-response test. The key comparison is the jump from solo play to team play.

## The Full Gradient

Combining the [[1v1 Falsification Test]] floor with the [[Team Size Effects]] results:

| Mode | Teammates | TPE Coef | Selo Coef | TPE/Selo Ratio |
|------|-----------|----------|-----------|----------------|
| 1v1 | 0 | 0.252 | 1.704 | 0.148 |
| 2v2 | 1 | 0.416 | 0.798 | 0.522 |
| 3v3 | 2 | 0.410 | 0.761 | 0.539 |
| 4v4 | 3 | 0.373 | 0.626 | 0.596 |

## Two Ways to Read the Gradient

### 1. Raw TPE Coefficient (absolute predictive power)

The jump from 1v1 to team games is stark: TPE goes from 0.252 to 0.373--0.416, roughly a **1.5--1.7x increase**. Within team modes, raw TPE is relatively flat, declining slightly as more players dilute any single player's contribution.

### 2. TPE/Selo Ratio (relative importance of coordination vs skill)

This is the more informative measure. The ratio increases monotonically:

- **1v1:** 0.148 -- TPE is ~15% of Selo (the "floor"; individual skill spillover only)
- **2v2:** 0.522 -- TPE is ~52% of Selo (**3.5x the floor**)
- **3v3:** 0.539 -- TPE is ~54% of Selo (**3.6x the floor**)
- **4v4:** 0.596 -- TPE is ~60% of Selo (**4.0x the floor**)

The monotonic increase in relative importance confirms that as coordination demands grow, individual skill matters less and coordination matters more.

## Why Raw Coefficients Decline While Relative Importance Rises

Both Solo Elo and TPE coefficients decline from 2v2 to 4v4 -- adding more players dilutes any individual's absolute contribution. But Solo Elo **drops faster** (0.798 to 0.626, -21%) than TPE (0.416 to 0.373, -10%). This asymmetric dilution shifts the balance toward coordination.

## What This Rules Out

If TPE were simply "unmeasured individual ability," it should have the same relative importance in 1v1 and team games. The 4x jump in TPE/Selo ratio from 1v1 (0.148) to 4v4 (0.596) rules out this interpretation -- coordination skill manifests specifically when teammates are present.

## Connection to Theory

The gradient mirrors the organizational science prediction that coordination costs scale with group size. Each additional teammate adds synchronization overhead that individual skill cannot address, increasing the premium on coordination ability.
