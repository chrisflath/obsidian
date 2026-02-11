# Time Mechanism

## Question

Do players compensate for lost templates by spending more time thinking? Does this explain the performance gap?

## Caveat

> [!warning] Standard clock coverage is ~7%
> Lichess only exports clock data for some standard games. Cross-format time comparisons are **suggestive only**.

## Results (Move-Level)

| Variable | Coefficient | p | Interpretation |
|----------|------------|---|----------------|
| format x relative_time | -0.084 | *** | 960 players are LESS time-sensitive |
| format x clock_remaining | -0.002 | n.s. | No clock pressure interaction |

### Within-960 Quartiles

Monotonic relationship between time spent and CPL:

| Quartile | Mean CPL |
|----------|----------|
| Q1 (fast) | 2.85 |
| Q2 | 3.03 |
| Q3 | 3.16 |
| Q4 (slow) | 3.32 |

Slower moves have *higher* CPL — players spend more time on harder positions (endogenous).

### Phase Split

| Phase | format x time interaction | p |
|-------|--------------------------|---|
| Early opening (2-6) | -0.096 | *** |
| Late opening (7-12) | -0.025 | * |

The format-time interaction is strongest in the earliest moves where template disruption is greatest.

## Clock in Gelbach Decomposition

Clock state (player + opponent pre-move clock) explains only **1.1%** of the format gap in the [[Gelbach Decomposition]]. Time allocation is not a major mechanism.

See also: [[Key Results]], [[Gelbach Decomposition]]

**Script**: `analysis/difficulty_rubric.py`

#chess960 #methods #time
