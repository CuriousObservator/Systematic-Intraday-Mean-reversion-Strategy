# Systematic-Intraday-Mean-reversion-Strategy
A systematic, market-neutral intraday strategy for Indian equities — an overnight-gap reversion signal, deployed under realistic capital constraints across **118 NSE constituents** and **11+ years** of daily data.

DASHBOARD: https://curiousobservator.github.io/Systematic-Intraday-Mean-reversion-Strategy/

## Performance Summary

The strategy is evaluated two ways: the **raw signal** (every qualifying gap taken, no capital limit) and a **realistic deployment** (₹10,00,000 starting capital, max 10% of equity per position, max 10 concurrent positions). The realistic version is the one that matters for anyone actually allocating capital — it converts a strong but unfundable raw signal into something a real account could sit through.

| Metric | Unconstrained (signal only) | Realistic Deployment |
|---|---|---|
| CAGR | 68.6% | 29.0% |
| Sharpe Ratio | 1.92 | 1.95 |
| Max Drawdown | -34.4% | -13.0% |
| Capital limit | None | 10% / trade, 10 max positions |

| Metric | Value |
|---|---|
| Profit Factor | 1.31 |
| Win Rate | 55.1% |
| Total Trades | 8,079 |
| Final Equity (realistic) | ₹1.75Cr from ₹10L starting capital |
| Backtest Period | 2015 – Apr 2026 (11.2 years) |
| Universe | 118 NSE-listed equities |

> *All figures are net of a 20 bps round-trip transaction cost assumption. Backtest uses daily OHLC data. Backtest, not live trading.*

---

## Motivation

Opening price gaps are a well-documented phenomenon in equity markets. This project investigates whether such gaps carry a statistically predictable mean-reversion signal in the Indian equity market, and whether that signal survives realistic position-sizing and capital constraints — not just in an idealized, unlimited-capital backtest.

The raw signal produces a striking headline CAGR (68.6%) but with a drawdown (-34.4%) that would be difficult for most allocators to hold through. The central question this project addresses is what happens to the edge once it's forced through a realistic capital and concentration limit.

---

## Methodology

- **Signal:** Cross-sectional, price-based. Computed from publicly available OHLC data at market open.
- **Execution:** Enter at open, exit at close. Both long and short sides.
- **Universe:** 118 NSE-listed equities, filtered to remove illiquid and erroneous data points.
- **Position sizing:** Each position sized at up to 10% of live equity, capped at a maximum of 10 concurrent positions per day. When more than 10 candidates qualify on a given day, signals are ranked by absolute gap size and the top 10 are taken.
- **Costs:** 20 bps round-trip transaction cost applied to every trade.
- **No lookahead:** Signal is fully known before the trading session begins.

What is **not** disclosed here: the gap threshold(s) used to trigger a trade, strike/stock selection criteria beyond "NSE universe," and any filter logic beyond what's described above.

---

## Why Sizing Is Part of the Edge

A raw, unconstrained version of this signal — taking every qualifying gap with no position limit — backtests to a 68.6% CAGR and 1.92 Sharpe, but with a -34.4% max drawdown. That drawdown is the kind of number that looks fine on a spreadsheet and is very difficult to actually sit through with real capital.

Capping exposure to 10% of equity per position, with a maximum of 10 concurrent positions, brings max drawdown down to -13.0% while *increasing* Sharpe slightly to 1.95 — at the cost of roughly two-thirds of the unconstrained CAGR (29.0% vs. 68.6%). This is the realistic, fundable version of the strategy, and it's the version reflected in the headline performance summary above.

---

## Year-by-Year (Realistic Deployment)

| Year | Return | Sharpe | Max DD | Trades | Win % |
|---|---|---|---|---|---|
| 2015 | 68.2% | 5.31 | -2.5% | 603 | 63.0% |
| 2016 | 8.4% | 0.82 | -10.0% | 701 | 54.5% |
| 2017 | 1.6% | 0.21 | -13.0% | 490 | 57.3% |
| 2018 | 37.0% | 2.71 | -6.1% | 686 | 55.7% |
| 2019 | 4.9% | 0.44 | -10.4% | 605 | 52.6% |
| 2020 | 80.1% | 2.40 | -12.9% | 1,228 | 53.8% |
| 2021 | 55.0% | 3.14 | -7.2% | 937 | 55.4% |
| 2022 | 33.0% | 2.54 | -8.8% | 806 | 55.5% |
| 2023 | 10.4% | 0.85 | -9.3% | 640 | 47.3% |
| 2024 | 25.3% | 1.71 | -12.0% | 684 | 57.5% |
| 2025 | 28.9% | 2.88 | -4.7% | 484 | 59.3% |
| 2026 YTD | -1.7% | -0.85 | -3.8% | 215 | 44.7% |

A few honest observations:
- Performance is **not uniform** — 2017 and 2019 were notably weak years (Sharpe under 0.5), and **2026 year-to-date is negative** (-1.7%, Sharpe -0.85), the only losing calendar period in the sample.
- The strongest year, 2020, coincides with the COVID volatility spike — a period of unusually large overnight gaps, which is consistent with this being a genuine gap-driven signal rather than a fluke.
- 2023's win rate (47.3%) is the weakest in the sample, despite still producing a positive return that year — a reminder that this strategy's edge comes from asymmetric win/loss size, not from winning most of the time.

---

## Long vs. Short Breakdown

| | Trades | Win Rate |
|---|---|---|
| Long | 3,515 | 53.0% |
| Short | 4,564 | 56.6% |

Both sides carry positive win rates, with short trades both more numerous and slightly higher-probability in this sample — consistent with a genuine two-sided mean-reversion effect rather than a long-only or short-only bias.

**Additional detail:**
- Average win: +2.69%
- Average loss: −2.48%
- Average positions held per day: 3.6
- Average capital deployed per day: ~36%

---

## How to Read the Dashboard

The accompanying dashboard visualizes:
- **Unconstrained vs. realistic comparison** — side-by-side CAGR, Sharpe, and drawdown for the raw signal vs. the capital-constrained deployment
- **Equity curve & drawdown** — weekly-sampled cumulative equity (₹10L → ₹1.75Cr) with an underwater drawdown panel on the same time axis
- **Year-by-year table** — return, Sharpe, max drawdown, trade count, and win rate per calendar year
- **Long vs. short breakdown** — trade counts and win rates for each side
- **Monthly returns heatmap** — a calendar view of month-by-month performance across all 11+ years, useful for spotting seasonality or regime-dependence

All figures in the dashboard are net of the assumed transaction cost and computed directly from the underlying trade log.

---

## Known Risks & Limitations

- **Backtest, not live trading.** These are historical simulations using past OHLC data, cost assumptions, and a fixed position-sizing rule. Past performance — simulated or real — does not guarantee future results.
- **Survivorship bias:** Results may be overstated if the 118-stock universe excludes delisted or suspended securities over the full 11-year window.
- **Execution risk:** Open and close prices on NSE are auction-determined; live slippage may exceed the assumed 20 bps round-trip cost, especially when ranking forces selection among many same-day candidates.
- **Concentration risk:** Even with the 10-position cap, drawdown is elevated on high-volatility days where the strategy fills its full book in one direction.
- **Regime dependence:** Performance varies meaningfully by year (Sharpe ranging from -0.85 to 5.31) and the most recent period (2026 YTD) is negative — a regime shift is being monitored, not yet confirmed.
- **Sizing trade-off is real, not free:** the drawdown reduction from capital constraints comes at a substantial cost to absolute CAGR (29.0% vs. 68.6%). This is a deliberate choice to favor a fundable, sittable-through return profile over a maximal one.

---

## Tech Stack

- **Python** — NumPy, Pandas, Matplotlib
- **Data** — Daily OHLC, NSE universe (118 constituents)
- **Analysis** — Position-sizing simulation, threshold-based signal ranking, rolling equity/drawdown, monthly/yearly attribution

---

## Author

**Malapaka Venkata Ratna Abhishek**
Astrophysics | Quantitative Researcher | Hyderabad, India
[GitHub](https://github.com/CuriousObservator) · [arXiv](https://arxiv.org/a/0009-0006-2553-6540) · mvrquant@gmail.com

---

*Strategy logic — including the exact gap threshold(s) used to trigger trades and any additional filters — is not disclosed in this repository. This README presents performance and methodology at a level consistent with academic and professional communication.*
