# Research Open Ends

Central tracker for open questions, planned analyses, and cross-project opportunities.

---

## Chess960 Project

### Data Collection (in progress)
- [ ] **MultiPV complexity analysis** — Phase 1 at ~55% (960: 87%, standard: 42%). Running via `analysis/complexity_analyzer.py`
- [ ] **Chess.com Freestyle Friday collection** — 200 players, fetching 960 + Titled Tuesday control. Running via `scraper/chesscom_collector.py`
- [ ] **Clean up main DB** — Remove `chesscom_tournaments`, `chesscom_participation` tables and `source='chesscom'` player rows from `chess960.db` (deferred while complexity analyzer holds lock)

### Analysis Open Ends
- [x] **Wire finalized Panel B into hero figure** — DONE. Single-panel Fig 1 with 3 skill tiers, 11 vignettes, raw CPL, template distance index. Dev script at `/tmp/fig1_raw6.py`, final at `fig1_dev_P.pdf`.
- [x] **Fig 2: theta3/theta4 paired coefficient plot** — DONE. Paired dot-and-whisker showing prep capital decays (θ3: +0.056 → +0.026) while general skill transfers uniformly (θ4: ~-0.05 across all phases). Dev script at `/tmp/fig2_dev3.py`, final at `fig2_dev_C.pdf`.
- [ ] **Chess.com replication** — Once FF data is collected: error composition, S-curve, anti-calibration, template distance gradient, two-rating decomposition (θ3)
- [ ] **Within-pool filtering** — At analysis time, prioritize games where both players are in the FF pool for controlled opponent quality
- [ ] **Expertise × time scale** — Does the template disruption show up more strongly in blitz (FF, 3+1) than rapid (Lichess, 10+0) among strong players? System 1 vs System 2 access
- [ ] **Formalize fig1/fig2 into publication_figures.py** — Current dev scripts in /tmp; need to integrate into the main publication script
- [ ] **Regenerate all figures from current sample** — Sample grew from 70K/306 to 106K/438. Figures were generated from older data. Need to re-run fig1 (hero), fig2 (theta3/theta4 phase), fig3, and verify all coefficients match paper text. Phase-specific θ3 shifted: middlegame now significant (p=0.002).
- [ ] **Re-run extended Gelbach from publication_figures.py** — Simpler Gelbach (two_rating_decomposition.py) shows 25.2% explained (was 35.7%). Need to verify the extended Gelbach (piece-level + clock + matchmaking) with current sample.

### Writing
- [x] **nature_short.tex reviewer feedback** — DONE. Fixed sample size (74,892), moves 1-12 throughout (2-12 as robustness), log transform rationale, raw CPL note, Figure 1 caption for single-panel hero, Figure 2 swapped to theta3/theta4 phase plot, moderated "reasoning alone" language. Committed and pushed 2026-02-15.
- [ ] **Reference-point clarity section** — Integrate S-curve, spline, domain split, depth-free validity into paper draft
- [ ] **Gelbach narrative** — 85% residual is the headline; piece displacement channels provide face validity
- [ ] **Update paper Figure 2 caption** — newmain.tex still references old theta3-only bar chart; needs caption for paired coefficient plot

---

## AoE Familiarity Project

### Analysis Open Ends
- [ ] **Gelbach decomposition of coordination gradient** — Decompose the TPE/Selo ratio shift from 1v1 (0.15) → 4v4 (0.60). Channels: map class, civ composition, familiarity, Elo tier. Does a large residual survive = pure coordination scaling?
- [ ] **Gelbach decomposition of map type gradient** — Decompose the +45% TPE importance jump from open → closed maps. Channels: game length, civ selection, Elo composition
- [ ] **Gelbach decomposition of patch shock** — Decompose the -8.7% Elo drop post-patch into civ-specific, mechanic-specific, and residual meta-disruption channels
- [ ] **eAPM analysis** — 78K matches with APM data; test whether TPE correlates with communication efficiency proxies
- [ ] **TPE re-estimation with map FE** — Addresses [[Nomad Anomaly]]
- [ ] **1v1 data request** — Enhanced [[1v1 Falsification Test]]
- [ ] **Network analysis** — Partner re-selection dynamics

### Writing
- [ ] **Manuscript finalization** — Two venue strategies (AEJ Micro vs Org Science)
- [ ] **Theoretical framing** — "Roadmap vs compass" narrative

---

## Cross-Project

- [ ] **Gelbach as shared method** — Both papers use natural experiments + Gelbach to separate channels. Chess960 already done (85% residual). AoE coordination gradient is the next candidate. Shared methodology section opportunity?
- [ ] **Expertise composite capital theory** — Both projects show observed skill ratings conflate transferable + context-specific components. Joint framing for a methods/theory paper?
- [ ] **Cross-cite** — Each paper should cite the other as converging evidence from a different domain. See [[Skill Decomposition — Cross-Project Bridge]]

---

*Updated: 2026-02-19*

#open-ends #todos #cross-project
