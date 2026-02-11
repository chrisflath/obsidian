# Analysis Pipeline

## Package Management

Always use `uv`:
```bash
uv pip install <package>
uv run python <script>
uv add <package>
```

## Scripts

### Data Collection
| Script | Purpose |
|--------|---------|
| `scraper/player_discovery.py` | Find paired players on Lichess |
| `scraper/game_fetcher.py` | Download games via Lichess API |
| `scripts/clock_backfill.py` | Backfill player clock from PGN `[%clk]` |
| `scripts/clock_backfill_opponent.py` | Backfill opponent clock |

### Analysis (Stockfish)
| Script | Purpose |
|--------|---------|
| `analysis/stockfish_runner.py` | Core Stockfish wrapper, game analysis (FEN cache) |
| `analysis/complexity_analyzer.py` | MultiPV complexity (FEN cache, see [[Complexity Analysis]]) |

Both pipelines use cross-game FEN caching — identical positions are analyzed once and reused. See [[Complexity Analysis#FEN Cache]] for hit rates.

```bash
# Game analysis
uv run python -m analysis.stockfish_runner --batch 50 --time-limit 0.1

# Complexity analysis (parallel)
uv run python -m analysis.complexity_analyzer \
  --batch 500 --multipv 5 --time-limit 0.5 \
  --threads 2 --workers 5
```

### Statistical Analysis
| Script | Purpose |
|--------|---------|
| `analysis/two_rating_decomposition.py` | Two-rating, SP FE, Gelbach, random slopes |
| `analysis/revision_analyses.py` | Reviewer robustness (items 2,4,5,6,7) |
| `analysis/difficulty_rubric.py` | Time mechanism, complexity x format |
| `scripts/game_level_analysis.py` | Primary game-level decomposition |

```bash
uv run python -m analysis.two_rating_decomposition
uv run python -m analysis.revision_analyses
```

### Figures
| Script | Purpose | Output |
|--------|---------|--------|
| `scripts/publication_figures.py` | Hero, theta3, BLUP scatter | `plots/publication/` |
| `scripts/paper_figures.py` | Three-panel + regression table | `plots/` |

```bash
uv run python scripts/publication_figures.py
```

Figures are copied to `/Users/chris/chess960Paper/figures/` for the paper.

## Database

SQLite at `db/chess960.db`. See [[Database Schema]].

```bash
# Quick status check
uv run python -c "
from db_utils import get_connection
c = get_connection().cursor()
c.execute('SELECT format, COUNT(*) FROM games WHERE analyzed_at > \"2000\" GROUP BY format')
print(dict(c.fetchall()))
"
```

#chess960 #pipeline #infrastructure
