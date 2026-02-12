# Patch Shock Analysis

Part of [[aoeFamiliarity Project]] | Identification Test (Natural Experiment)

**Script:** `id_temporal_patches.py`

## Logic

Game balance patches change game mechanics, disrupting game-specific knowledge (Solo Elo predictive power). If TPE captures transferable coordination skill, it should remain stable through patches.

## Patches Analyzed

| Patch | Date | Type | Mechanism |
|-------|------|------|-----------|
| Auto-Scout | 2020-02-27 | Mechanical | Automated scouting reduces micro burden |
| Lords of West | 2021-01-26 | Content | New civilizations, balance changes |
| Dawn of Dukes | 2021-08-10 | Content | New civilizations, new campaigns |
| Dynasties of India | 2022-04-28 | Content | Split Indian civs into 3, major rebalance |

## Model

```
win ~ selo + tpe + fam + post + selo*post + tpe*post + fam*post + controls
```

Window: +/- 45 days around each major patch.

## Results (Major Patches Pooled, N=248,928)

| Predictor | Pre-Patch | Post-Patch Change | p-value |
|-----------|----------|-------------------|---------|
| **Solo Elo** | baseline | **-8.7%** | <0.001 |
| **TPE** | baseline | **-0.8%** | 0.850 |
| **Familiarity** | baseline | **-30.3%** | 0.050 |

## By Individual Patch

| Patch | Selo Change | Selo p | TPE Change | TPE p |
|-------|-------------|--------|------------|-------|
| Auto-Scout | -10.4% | 0.025 | -0.3% | 0.93 |
| Lords of West | -7.8% | <0.001 | -1.6% | 0.30 |
| Dawn of Dukes | -9.1% | <0.001 | -2.6% | 0.09 |
| Dynasties of India | -14.2% | <0.001 | -0.1% | 0.97 |

## The "Roadmap vs Compass" Narrative

- **Solo Elo = "roadmap"**: Game-specific knowledge that becomes unreliable when the terrain changes (patches)
- **TPE = "compass"**: Adaptive coordination skill that points "north" regardless of meta changes
- **Familiarity = "old habits"**: Prior coordination patterns that may or may not transfer to the new meta

This is the paper's central identification result. See also [[Permutation Tests]] for placebo validation, [[Meta Maturity Recovery]] for the recovery curve, and [[Skill Decomposition — Cross-Project Bridge]] for the structural parallel with the Chess960 two-rating decomposition.
