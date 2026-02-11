# Terminology Glossary

Part of [[aoeFamiliarity Project]]

## AoE2 Terms -> Organizational Science Mapping

| AoE2 Term | Org Science Equivalent | Definition |
|-----------|----------------------|------------|
| **Solo Elo** | Individual Human Capital | Rating from 1v1 matches; measures mechanical/strategic skill in isolation |
| **Team Player Effect (TPE)** | Team-Specific Human Capital / Coordination Skill | Residualized contribution to team wins beyond individual skill |
| **Familiarity** | Team Tenure / Relationship Capital | Cumulative shared experience between specific teammates |
| **Match** | Task Episode | A single competitive game (15-60 min) |
| **Patch** | Environmental Shock / Regime Change | Developer update that changes game mechanics and balance |
| **Elo Rating** | Skill Measure | Chess-derived rating system; higher = more skilled |
| **Civilization (Civ)** | Role / Specialization | In-game faction choice with distinct strengths |
| **Flank** | Specialist Role (Boundary) | Outer team position; early aggression and defense |
| **Pocket** | Specialist Role (Core) | Inner team position; economic boom and late-game support |
| **APM / eAPM** | Task Efficiency / Throughput | Actions Per Minute (effective); measures execution speed |
| **Meta** | Best-Practice Knowledge | Currently dominant strategies and builds |
| **Build Order** | Standard Operating Procedure | Optimized sequence of early-game actions |
| **TC (Town Center)** | Home Base / Core Asset | Central building for economy and unit production |
| **Boom** | Growth Strategy | Economic expansion focus (delayed aggression) |
| **Rush** | Exploitation Strategy | Early aggressive attack (sacrifice economy) |

## Key Construct Definitions

### Team Player Effect (TPE)
The residual of a player's contribution to team wins after removing:
1. Their individual skill (Solo Elo)
2. Team familiarity effects
3. Map-specific effects

Conceptually: "How much better does a team perform when this player is on it, beyond what their individual skill predicts?"

### Familiarity (Fam)
Weighted sum of prior shared matches between all teammate pairs on a team. Captures relationship-specific learning and trust. Exponentially distributed (most teams are strangers or near-strangers).

### Solo Elo (Selo)
Elo rating derived exclusively from 1v1 matches. Used as the "pure individual skill" benchmark. Key property: cannot be inflated by good teammates.

## Statistical Terms

| Term | Definition |
|------|------------|
| **Upstream** | Stage 1 of pipeline: estimating player-level TPE coefficients |
| **Downstream** | Stage 3: validating TPE on held-out data |
| **Residualization** | Removing the portion of TPE correlated with Solo Elo |
| **Oster Bounds** | Method to assess robustness to omitted variable bias |
| **Placebo Test** | Using fake treatment dates to verify real effects aren't artifacts |
| **Within-Tier** | Standardizing variables within Elo quartiles (local comparisons) |
| **Global Standardization** | Standardizing across the full sample (broad comparisons) |
