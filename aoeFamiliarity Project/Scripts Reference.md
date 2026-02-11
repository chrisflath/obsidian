# Scripts Reference

Part of [[aoeFamiliarity Project]]

All scripts are in `/aoeFamiliarity/revision_work/code/` and use **Marimo** reactive notebooks.

## Data Pipeline

| Script | Purpose | Input | Output |
|--------|---------|-------|--------|
| `01_data_prep.py` | Load data, create estimation/validation splits | `long_matches.parquet` | `match_data_*.parquet` |
| `02_upstream_final.py` | Estimate TPE coefficients (gamma_i) | Estimation sample | `gamma_raw.csv` |
| `03_decomposition.py` | Residualize gamma against selo | `gamma_raw.csv` | `tpe_final.csv` |
| `04_downstream_final.py` | Validate TPE on held-out sample | Validation + TPE | Core results |

## Core Analysis

| Script | Purpose |
|--------|---------|
| `core_main_regression.py` | Main TPE effect (Selo, TPE, Fam coefficients) |
| `data_loader.py` | Standardized data loading functions |
| `match_level_utils.py` | Helper functions for match-level aggregation |

## Heterogeneity Analyses (`het_*.py`)

| Script | Focus | Key Finding |
|--------|-------|-------------|
| `het_skill_tiers.py` | Elo quartiles | U-shape in Selo; TPE stable |
| `het_skill_variance.py` | Variance mechanism | r=0.98: variance explains U-shape |
| `het_player_role.py` | Pocket vs Flank | Minimal difference (1.6%, NS) |
| `het_map_types.py` | Open/Closed/Nomad | Closed +45% TPE importance |
| `het_temporal_stability.py` | Early vs late career | r=0.41 correlation |
| `het_temporal_tpe_drift.py` | Calendar time drift | Stable with seasonality |

## Identification Tests (`id_*.py`)

| Script | Test | Key Result |
|--------|------|-----------|
| `id_solo_falsification.py` | 1v1 floor | ~14.8% (Open maps) |
| `id_patch_placebo.py` | Permutation tests | Placebo = null |
| `id_temporal_patches.py` | Patch shocks | Selo -8.7%, TPE -0.8% |
| `id_patch_recovery.py` | Meta maturity | Selo recovers, TPE flat |
| `id_robustness.py` | Spec robustness | Generally robust |
| `id_oster_bounds.py` | OVB bounds | delta = -0.53 |
| `id_stranger_matches.py` | Stranger test | TPE = 0.131 for strangers |
| `id_coordination_gradient.py` | 1v1 to 4v4 gradient | >5x |
| `id_early_career.py` | Early manifestation | Visible after ~25 matches |
| `id_partner_selection.py` | Revealed preference | 27% re-selection premium |
| `id_match_closeness.py` | Match quality | Larger effect in tight games |
| `id_tpe_matching.py` | Assortative matching | Weak assortative |

## Sensitivity Analyses (`s*.py`)

| Script | Topic | Finding |
|--------|-------|---------|
| `s1b_civ_interactions.py` | Civ-specific TPE | Minor interactions |
| `s7c_triple_interaction.py` | TPE x Fam x Elo Tier | Strongest at high Elo |

## Running All Analyses

```bash
./run_all_analyses.sh
```

This batch script exports all Marimo notebooks to HTML for review.
