# Oster Bounds

Part of [[aoeFamiliarity Project]] | Identification Test (Omitted Variable Bias)

**Script:** `id_oster_bounds.py`

## Method

Oster (2019) bounds assess how robust a treatment effect is to potential omitted variable bias. The key parameter delta measures how much unobservable confounders would need to relate to the outcome relative to observables.

## Result

**delta = -0.53 (NEGATIVE)**

## Interpretation

A negative delta means that adding controls to the model **increases** the TPE coefficient rather than decreasing it. This implies:

1. Existing confounders work **against** TPE (they suppress the true effect)
2. To bias TPE to zero, one would need unobserved confounders with delta < -0.53
3. Such confounders would need to be **negatively** correlated with both TPE and wins -- hard to construct theoretically

## Why This Is Strong Evidence

- In most applied research, the concern is that adding controls will shrink the treatment effect (positive confounding)
- Here, the opposite occurs: controls **strengthen** the TPE effect
- This makes the omitted variable bias concern essentially moot

## Practical Implication

Reviewers asking "what if there's an omitted variable?" can be addressed with: "Omitted variables would need to work in the opposite direction of all observed confounders, and with 53% of their strength, to eliminate the TPE effect."

## Reference

Oster, E. (2019). "Unobservable Selection and Coefficient Stability: Theory and Evidence." *Journal of Business & Economic Statistics*, 37(2), 187-204.
