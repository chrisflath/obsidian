# Research Design

Part of [[aoeFamiliarity Project]]

## Identification Challenge

Team outcomes depend on multiple factors (individual skill, team composition, familiarity, strategy). Isolating coordination skill requires separating it from correlated individual ability.

## Identification Strategy

### 1. Residualization (Core Approach)
- Estimate each player's contribution to team wins via [[Three-Stage Pipeline]]
- Residualize against Solo Elo to remove individual skill correlation
- Output: pure coordination component (TPE)

### 2. Patch Shocks (Natural Experiment)
- Game balance patches disrupt mechanical knowledge
- Solo Elo predictive power drops 8-14%
- TPE remains stable (-0.8%, p=0.850)
- See [[Patch Shock Analysis]]

### 3. 1v1 Falsification
- If TPE = coordination, it should NOT predict solo games
- Finding: ~5-15% spillover (minimal baseline)
- See [[1v1 Falsification Test]]

### 4. Stranger Matches
- TPE predicts wins even for teammates with zero prior experience
- Rules out "learned synergy" interpretation
- See [[Stranger Matches]]

### 5. Oster Bounds (OVB)
- Adding controls *increases* TPE coefficient (negative confounding, delta = -0.53)
- Very difficult to explain away via omitted variables
- See [[Oster Bounds]]

### 6. Permutation Tests
- Placebo patch dates yield null effects; actual dates show real disruption
- See [[Permutation Tests]]

### 7. Player Fixed Effects
- Teammate's TPE predicts YOUR wins after absorbing your own fixed effect
- See [[Player Fixed Effects]]

### 8. Revealed Preference
- Players re-select high-TPE partners 27% more often
- See [[Partner Re-Selection]]

## Validation Strategy

1. **Out-of-Sample Testing**: 50/50 split -- estimation sample (train TPE) vs validation sample (test it)
2. **Cross-Validation**: Folds stored in `revision_work/data/folds/`
3. **Heterogeneity Testing**: Effects hold across subgroups (civs, maps, skill tiers)
4. **Robustness Across Specifications**: Match-level and player-level aggregations yield consistent results

## Causal Claims

**Can claim with confidence:**
- TPE causally predicts team win probability
- TPE has a distinct effect from individual skill (Elo)
- Coordination skill is measurable and valued by players

**Requires caution:**
- Whether TPE captures "pure" coordination or includes unmeasured individual skill
  - 1v1 floor ~15% suggests some spillover
  - Teammate FE model supports team synergy interpretation
- Generalizability beyond the AoE2 setting (single game, acknowledged limitation)
