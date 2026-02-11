# Chess960 Project

Estimating the **template-applicability advantage** in expert decision-making using Chess960 as a natural experiment.

## Core Idea

Chess960 randomizes the back rank, disabling memorized opening preparation ("templates"). Comparing the same players across standard and Chess960 formats isolates the value of preparation capital.

## Map of Contents

### Design & Data
- [[Research Design]] — identification strategy, within-player comparison
- [[Sample & Inclusion Rules]] — rapid only, paired players, move window
- [[Key Variables]] — DV, treatment, controls
- [[Database Schema]] — tables, joins, coverage

### Methods
- [[Two-Rating Decomposition]] — separating prep capital from general skill
- [[Start-Position Fixed Effects]] — absorbing SP heterogeneity via FWL
- [[Gelbach Decomposition]] — piece-level, structural, clock, matchmaking
- [[Random Slopes & BLUPs]] — player-level format gaps
- [[Complexity Analysis]] — MultiPV position difficulty
- [[Time Mechanism]] — clock usage across formats

### Results
- [[Key Results]] — main findings summary
- [[Robustness Checks]] — reviewer-requested analyses

### Infrastructure
- [[Analysis Pipeline]] — scripts, how to run, dependencies

## Status

| Component | Status |
|-----------|--------|
| Data collection | Complete (~70K games, 306 players) |
| Stockfish analysis | Complete (depth 20, time-limited) |
| MultiPV complexity | In progress (~236K / ~1.5M positions) |
| Publication figures | Complete (3 main figures) |
| Reviewer robustness | Complete (items 2, 4, 5, 6, 7) |

#chess960 #research #MOC
