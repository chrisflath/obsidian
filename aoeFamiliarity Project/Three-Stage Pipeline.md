# Three-Stage Pipeline

Part of [[aoeFamiliarity Project]] | See also: [[Key Variables]], [[Scripts Reference]]

## Overview

The estimation follows a three-stage approach: Upstream (estimate raw TPE), Decomposition (isolate coordination), Downstream (validate).

---

## Stage 1: Upstream (TPE Estimation)

**Goal:** Estimate each player's contribution to team wins

**Script:** `02_upstream_final.py`

**Model:**
```
logit(P(win)) = beta_1 * exp_diff + beta_2 * fam_diff + map_FE
                + SUM_i(gamma_i * player_i * selo_scaled)
```

**Key Details:**
- Uses **raw Solo Elo** (`p_solo_elo / 1000` for scaling) -- NOT standardized
- Interaction term: player indicator x skill creates player-specific coefficients (gamma_i)
- Sparse matrix design for efficient handling of 14k players
- Estimated on **50% estimation sample** only

**Output:** gamma_i coefficients (raw effect estimates) per player

**Critical Rule:** Must use raw Elo, not standardized. Standardized variables compress the range and violate the Cobb-Douglas specification's assumptions about proportional contributions.

---

## Stage 2: Decomposition (Isolate Coordination)

**Goal:** Remove individual skill correlation from gamma

**Script:** `03_decomposition.py`

**Model:**
```
gamma = intercept + slope * selo + residual
gamma_coord = residual  (pure coordination)
```

**Rationale:** gamma may correlate with solo skill (better players might have higher gamma). Residualizing against selo isolates pure coordination ability.

**Validation:** Correlation between gamma_coord and selo should be approximately 0.

---

## Stage 3: Downstream (Validation)

**Goal:** Validate TPE predicts team outcomes on held-out data

**Script:** `04_downstream_final.py`

**Main Model:**
```
win ~ beta_1 * selo_diff + beta_2 * tpe_diff + beta_3 * exp_diff + controls
```

**Key Validation Targets:**

| Test | Target | Interpretation |
|------|--------|----------------|
| TPE/Selo Ratio | 25-50% | Coordination ~1/3 as important as skill |
| 1v1 Floor | ~5-15% | TPE should NOT predict solo games |
| Gradient | >5x | Team effect should be 5x+ larger than 1v1 floor |
| Team Size Gradient | 2v2 < 3v3 < 4v4 | TPE importance scales with complexity |

---

## Data Flow

```
long_matches.parquet
        |
   01_data_prep.py
        |
   +----+----+
   |         |
estimation  validation
 sample      sample
   |
02_upstream_final.py --> gamma_raw.csv
   |
03_decomposition.py --> tpe_final.csv
   |
   +--- validation sample
   |
04_downstream_final.py --> Core regression results
```
