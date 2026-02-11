# Project Status

Part of [[aoeFamiliarity Project]]

**Last Updated:** January 2026

## Current Focus

Paper revision for **Management Science (MNSC)** submission at INFORMS.

## Completed Work

- [x] Three-stage estimation pipeline (upstream -> decomposition -> downstream)
- [x] Core regression results with match-level aggregation
- [x] 10+ heterogeneity analyses (map, role, skill tier, team size)
- [x] 12+ identification tests (patches, falsification, Oster bounds, permutation, player FE)
- [x] Behavioral validation (partner re-selection analysis)
- [x] Documentation overhaul (MASTER_ANALYSIS_DOC, ANALYSIS_INDEX, glossary)

## In Progress

- Manuscript writing (two venue strategies outlined in WRITING_WORKPLAN.md)
- Figure production (100+ PDFs in `Social Skills in eSport/figures/`)
- Theoretical positioning ("roadmap vs compass" narrative)

## Pending / Technical Debt

- 1v1 match data request for enhanced [[1v1 Falsification Test]]
- Post-patch exclusion robustness check (S10)
- TPE re-estimation with map fixed effects (addresses [[Nomad Anomaly]])
- eAPM analysis (78k matches with APM data -- test communication efficiency)
- Network analysis of partner re-selection dynamics

## Two-Venue Strategy

1. **AEJ Micro** -- Emphasize clean identification, causal claims, and natural experiment design
2. **Organization Science** -- Emphasize team composition theory, human capital framework, and managerial implications

## Git Workflow

- **Main branch:** Stable, reviewed code
- **Feature branches:** `feature/pipeline-rewrite` (current)
- **Commit style:** `[tag] descriptive message` (e.g., `[upstream] Fix raw selo support`)

## Project Timeline

| Period | Activity |
|--------|----------|
| Dec 2019 | Data collection begins |
| Oct 2024 | Initial analyses (V1 notebooks) |
| Nov 2024 | Legacy COG version |
| Dec 2024 | Systematic ablations |
| Jan 2026 | Pipeline rewrite, documentation overhaul |

## Key Files

| File | Purpose |
|------|---------|
| `CLAUDE.md` | High-level project context |
| `revision_work/documentation/MASTER_ANALYSIS_DOC.md` | Comprehensive analysis tracker |
| `revision_work/documentation/ANALYSIS_INDEX.md` | Quick reference with effect sizes |
| `revision_work/documentation/WRITING_WORKPLAN.md` | Manuscript strategy |
