# T2 ETF Comparison — Fees and Drawdown

This task continues the T1 plan (comparing `SPY`, `TLT` and `GLD` on annual fees and historical drawdown) by upgrading from the illustrative T1 dataset to the T2 ETF Data Pack, a real-data daily price pack prepared by the instructor.

## Inputs and Method

- Input files: `data/t2/daily_prices.csv`, `data/t2/fund_info.csv`, `data/t2/data_dictionary.md` (context: `artifacts/t1/project-plan.md`).
- Pack preparation date: 2026-09-25; daily prices cover **2016-09-01 through 2026-08-31** (2,512 sessions per ETF; 7,536 rows total), daily frequency, US market session dates.
- Adjustment basis: `adjusted_close` (provider's split/dividend adjustments); `close` was inspected but not used for the required calculation.
- Fee disclosure dates (accessed 2026-09-25): **SPY** 0.0945% — fund-information as-of date 2026-09-10, fee-specific effective date not stated; **TLT** 0.15% — current prospectus, specific date not stated in the fee panel; **GLD** 0.4% — not stated in the selected field. These are current disclosure snapshots, not ten-year averages.
- Script: `artifacts/t2/calculate_drawdown.py`; executed command: `python3 artifacts/t2/calculate_drawdown.py` (Python 3.9.6, standard library only).
- Input checks (all passed): exactly the three tickers; unique ticker/date pairs; dates ascending within each ticker; positive finite `close` and `adjusted_close`; 2,512 rows per ETF; common first date 2016-09-01 and last date 2026-08-31; matching date sets across tickers.
- Calculation: for each ticker, drawdown_pct = (adjusted_close / cumulative maximum from window start − 1) × 100 at every date; maximum drawdown = most negative value; earliest-trough / earliest-peak tie rule; full precision kept internally, rounded to two decimals for display.

## 1. Comparison

| Ticker | Annual expense ratio (%) | Max drawdown (%) | Peak date | Trough date |
|---|---|---|---|---|
| SPY | 0.0945 | −33.72 | 2020-02-19 | 2020-03-23 |
| TLT | 0.15 | −48.35 | 2020-08-04 | 2023-10-19 |
| GLD | 0.4 | −26.40 | 2026-01-29 | 2026-07-16 |

## 2. Observation

**GLD had the smallest drawdown loss (closest to zero) in this period** at −26.40%, followed by SPY at −33.72% and TLT at −48.35%; there were no ties among the displayed two-decimal results. These drawdowns were calculated from `adjusted_close` in `daily_prices.csv`, not read from any precomputed snapshot; drawdowns are non-positive, so closer to zero means a smaller loss. Limitation: the drawdowns measure daily-close declines within this fixed 2016–2026 window only — they are not all-time measures, do not capture intraday losses, and the disclosed fees are current snapshots that exclude trading costs such as bid/ask spreads.

## 3. Agent Check

This is the Agent's own self-check, not independent verification, and the student did not check the data. The Agent chose **SPY** and re-read its reported peak/trough rows from `daily_prices.csv`:

- 2020-02-19: `close=338.3399963378906`, `adjusted_close=307.6394958496094`
- 2020-03-23: `close=222.9499969482422`, `adjusted_close=203.91189575195312`

Check command (Python, stdlib): re-read the two rows, then recompute `(trough / peak − 1) × 100`. Actual output: full-precision −33.717257210811404 → −33.72, identical to the report. A second, independently implemented full-series pass over all 2,512 SPY rows (cumulative-max array with earliest-min and earliest-peak indexing) reproduced the same maximum drawdown −33.717257210811404 → −33.72 with peak 2020-02-19 and trough 2020-03-23, and confirmed peak ≤ trough. The observation was re-checked against all three results (−26.40 / −33.72 / −48.35); GLD remains the smallest loss with no ties. No errors were found; no correction or rerun was required.

## Next Action

Submit this report and script for review; the planned next step is to design the bounded analysis workflow with a separate Reviewer (per `tasks/t3_portfolio_research.md`), keeping return analysis outside this task's scope.
