# Skill Decomposition — Cross-Project Bridge

Both research projects share a core identification strategy: **decomposing observed performance into transferable skill vs context-specific capital**, using natural experiments that selectively disable the context-specific component.

## The Parallel

| | [[aoeFamiliarity Project\|AoE Familiarity]] | [[Chess960 Project/Research Design\|Chess960]] |
|--|---|---|
| **Composite measure** | Solo Elo (individual skill + game knowledge) | Standard rating (skill + prep capital) |
| **Transferable component** | TPE (coordination skill) | Chess960 rating (raw chess ability) |
| **Context-specific component** | Game-specific knowledge (meta, civ matchups) | Preparation capital (opening theory) |
| **Natural experiment** | Balance patches disrupt meta knowledge | Chess960 disables memorized openings |
| **Key test** | TPE stable through patches (-0.8% n.s.) while Elo drops (-8.7%***) | θ3 > 0: std rating's predictive advantage shrinks in 960 |
| **Phase specificity** | Patch effects concentrated in knowledge-heavy phases | θ3 concentrated in opening (vanishes in middlegame/endgame) |
| **Metaphor** | Roadmap (Elo) vs compass (TPE) | Template (std rating) vs raw ability (960 rating) |

## The Two-Rating Decomposition

Both projects use a **two-rating decomposition** to separate skill components:

**Chess960:**
```
Y = θ1·R_std + θ2·R_960 + θ3·(R_std × is_960) + θ4·(R_960 × is_960) + u_i + ε
```
- θ3 > 0 → standard rating (prep-inflated) loses predictive power in 960
- θ4 < 0 → 960 rating (prep-free) gains predictive power in 960

**AoE:**
```
win ~ selo + tpe + fam + selo×post_patch + tpe×post_patch + ...
```
- selo × post < 0 → Elo (meta-inflated) loses predictive power after patch
- tpe × post ≈ 0 → TPE (transferable) remains stable through patch

The structural form is identical: interact each rating component with a treatment indicator that disrupts the context-specific channel.

## Shared Conceptual Framework

1. **Observed skill = transferable + context-specific** — ratings conflate both
2. **Natural experiments selectively disable context-specific capital** — patches (AoE) / randomized positions (Chess960)
3. **Within-unit design** — same player before/after patch (AoE) or in both formats (Chess960) absorbs individual heterogeneity
4. **Specificity tests** — effects are concentrated where context-specific capital matters most (knowledge-heavy phases / opening phase)
5. **Behavioral consequence** — loss of context-specific capital leads to miscalibration (anti-calibrated time in Chess960; familiarity disruption in AoE)

## What Differs

- **Chess960** has a *permanent* treatment (960 always lacks templates) while **AoE patches** are *transient* shocks (meta eventually stabilizes)
- Chess960 uses **within-player cross-format** comparison; AoE uses **within-player before/after** comparison
- AoE has a third component (familiarity / relationship capital) with no direct Chess960 analog
- Chess960 can measure the *magnitude* of the prep advantage continuously (via template distance); AoE patch shocks are binary

## For the Papers

This parallel strengthens both papers independently:
- Chess960 paper can cite AoE as converging evidence from a different domain
- AoE paper can cite Chess960 as converging evidence with a cleaner (permanent, within-person) design
- Together they support a general theory of **expertise as composite capital** where domain-specific components inflate traditional performance metrics

#cross-project #methods #identification #skill-decomposition
