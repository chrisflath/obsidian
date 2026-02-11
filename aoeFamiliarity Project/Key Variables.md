# Key Variables

Part of [[aoeFamiliarity Project]] | See also: [[Three-Stage Pipeline]], [[Data Sources]]

## Dependent Variable

| Variable | Definition | Type |
|----------|-----------|------|
| **win** | Binary outcome (1 = team 0 wins, 0 = team 0 loses) | Binary |

## Independent Variables (Predictors)

| Variable | Aliases | Definition | Distribution | Notes |
|----------|---------|-----------|--------------|-------|
| **Solo Elo** | `selo`, `p_solo_elo` | Solo Elo rating from 1v1 matches | mean ~1450, sd ~280 | Individual skill; log-odds scale |
| **TPE** | `team_player_effect`, `tpe` | Residualized team contribution | mean ~0, sd ~0.05-0.10 | Coordination/social skill |
| **Familiarity** | `fam`, `team_fam_score` | Prior shared experience between teammates | Exponentially distributed | Relationship capital |
| **Experience** | `exp`, `team_match_count` | Cumulative match experience | Varies, log-transformed | Learning curve position |

## Aggregation Levels

### Player-Match Level
- One row per player per match
- Includes player's individual attributes (selo, tpe)
- Used for upstream estimation

### Match Level (Aggregated)
- One row per match
- Team-level differences: `team0_selo_sum - team1_selo_sum`
- Used for **main regression analysis** (downstream)

### Player-Level (Stratified)
- One row per player
- Used for heterogeneity analyses by tier/experience

## Fixed Effects & Controls

| Control | Purpose | Implementation |
|---------|---------|-----------------|
| Map Fixed Effects | Absorb map-specific winrate | Categorical dummies (Open/Closed/Nomad) |
| Mode (2v2/3v3/4v4) | Capture team size effects | Categorical dummies |
| Civilization | Civ-specific balance | Included in some specs |
| Player ID | Individual unobservables | Used in FE models only (see [[Player Fixed Effects]]) |

## RAW vs STANDARDIZED -- Critical Distinction

**CRITICAL RULE:** Before using any variable, verify standardization status.

| Type | `p_solo_elo` (Raw) | `selo` (Standardized) |
|------|--------------------|-----------------------|
| Mean | ~1400-1600 | ~0 |
| SD | ~280-310 | ~1 |
| Use for | Upstream estimation | Downstream analysis |
| Risk | None | Cobb-Douglas violations |

**Why it matters:** The [[Three-Stage Pipeline]] upstream stage uses Cobb-Douglas specifications requiring multiplicative interaction terms. Standardized variables compress the range and violate proportional contribution assumptions.
