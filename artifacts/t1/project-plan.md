# T1 Project Plan

## Project Goal

Develop a clear and reproducible research workflow for comparing three familiar asset classes — `SPY` (US equities), `TLT` (long-term US Treasury bonds), and `GLD` (gold) — based on the fixed illustrative ETF dataset in this repository. The focus is on project versioning, AI-assisted analysis, verification, and agent collaboration rather than data collection or environment setup.

## Available Data

- `data/etf_snapshot.csv` — a deliberately small, fixed dataset with one row per ETF:
  - `SPY` — US Equity; expected return 8.2%/yr, volatility 18%/yr, max drawdown -24%, expense ratio 0.09%
  - `TLT` — Long-Term US Treasury; expected return 4%/yr, volatility 14%/yr, max drawdown -18%, expense ratio 0.15%
  - `GLD` — Gold; expected return 5.5%/yr, volatility 15.5%/yr, max drawdown -16%, expense ratio 0.4%
- `data/data_dictionary.md` — definitions for the columns (`ticker`, `asset_class`, `expected_return_pct`, `volatility_pct`, `max_drawdown_pct`, `expense_ratio_pct`).

The dataset is synthetic teaching data: all values are illustrative assumptions, not live or historical market observations, and must not be used as investment advice.

## Expected Final Deliverable

A documented, reproducible workflow (plan plus a bounded analysis script/report) that compares the three ETFs on expected return, volatility, maximum drawdown, and costs, with results that can be verified by re-running the same steps. The analysis itself is planned work for later tutorials and has not been completed yet.

## Three Project Milestones

1. **Project setup (T1, current):** Write this project plan, have it reviewed, and version it with Git.
2. **Analysis task:** Design a bounded analysis task using the ETF snapshot (e.g., a risk/return comparison) and implement it in a reproducible script.
3. **Verification and agent workflow:** Organize a verifiable agent workflow, cross-check results, and document how the analysis can be reproduced.

## One Data Limitation

All numeric values in `etf_snapshot.csv` are synthetic teaching assumptions rather than current quotations, verified historical estimates, or forecasts, and the dataset omits correlations, taxes, transaction costs, liquidity, currency exposure, and investor-specific constraints. Any findings are therefore illustrative only and cannot support real investment decisions.

## Next Action

Review this plan against the repository contents, then save it with Git as the versioned starting point for the project. After versioning, proceed to design the bounded analysis task for the next milestone.

