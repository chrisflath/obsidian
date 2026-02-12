# aoeFamiliarity Project

**Paper Title:** "What Drives Team Success? Large-Scale Evidence on the Role of the Team Player Effect"
**Target Venue:** Management Science (MNSC) - INFORMS
**Setting:** Age of Empires II: Definitive Edition (competitive RTS)

## Core Research Question

Do certain individuals systematically improve team performance beyond what their technical skills predict? How do social/coordination skills and team familiarity interact?

## Core Finding

The **Team Player Effect (TPE)** -- a measurable coordination/social skill distinct from individual technical ability -- systematically predicts team outcomes and grows in importance as team size and strategic complexity increase.

- TPE is ~30% as important as individual skill (Solo Elo)
- TPE remains stable when game mechanics change ("compass" vs "roadmap")
- TPE is valued by players through revealed preference (partner re-selection)

## Dataset

- **3.7M+ matches total**, 1.6M team-based, 14,000 focal players
- **Time period:** December 2019 -- December 2023
- **Game modes:** 1v1 (solo), 2v2, 3v3, 4v4 (teams)

## Project Components

### Methodology
- [[Research Design]]
- [[Three-Stage Pipeline]]
- [[Key Variables]]
- [[Data Sources]]

### Results
- [[Core Results]]
- [[Effect Sizes Summary]]

### Heterogeneity Analyses
- [[Map Type Effects]]
- [[Skill Tier Effects]]
- [[Team Size Effects]]
- [[Player Role Effects]]
- [[TPE-Familiarity Complementarity]]

### Identification & Causal Inference
- [[1v1 Falsification Test]]
- [[Patch Shock Analysis]]
- [[Oster Bounds]]
- [[Stranger Matches]]
- [[Player Fixed Effects]]
- [[Permutation Tests]]
- [[Partner Re-Selection]]
- [[Meta Maturity Recovery]]
- [[Coordination Gradient]]

### Supplementary
- [[Terminology Glossary]]
- [[Scripts Reference]]
- [[Calibration and Model Quality]]
- [[Nomad Anomaly]]
- [[Project Status]]

## Key Metaphor: Roadmap vs Compass

- **Solo Elo = "roadmap"**: Game-specific mechanical knowledge; disrupted when patches change the meta
- **TPE = "compass"**: Adaptive coordination skills; remains valuable regardless of meta shifts
- **Familiarity = "old habits"**: Sometimes helps, sometimes hurts when meta shifts

## Cross-Project Link

See [[Skill Decomposition — Cross-Project Bridge]] — the two-rating decomposition in the [[Chess960 Project/Research Design|Chess960 project]] is structurally identical to the patch shock identification here: both separate transferable skill from context-specific capital using natural experiments that disable the context-specific channel.

## Scientific Contributions

1. **Measurement Innovation** -- First large-scale quantification of team coordination skill as distinct from individual ability
2. **Theoretical Insight** -- Coordination skill is transferable (not dyad-specific), familiarity amplifies it (complementarity)
3. **Methodological Rigor** -- Multi-pronged identification via patch shocks, Oster bounds, permutation tests, player FE
4. **Organizational Relevance** -- Human capital has a team-specific dimension; coordination costs scale with team size
