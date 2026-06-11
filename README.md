# Systematic-Intraday-Mean-reversion-Strategy
A systematic, market-neutral intraday strategy for Indian equities, validated across 247,000+ observations spanning 11 years and multiple market regimes.

DASHBOARD: https://curiousobservator.github.io/Systematic-Intraday-Mean-reversion-Strategy/

## Performance Summary

| Metric | Value |
|---|---|
| CAGR | ~72% |
| Annualised Sharpe Ratio | 1.98 |
| Max Drawdown | -37.9% |
| Win Rate | 55.2% |
| Profit Factor | 1.31 |
| Backtest Period | Jan 2015 – Jun 2026 |
| Universe | NSE Equities |

> *All figures include a round-trip transaction cost assumption. Backtest uses daily OHLC data.*

---

## Motivation

Opening price gaps are a well-documented phenomenon in equity markets. This project investigates whether such gaps carry a statistically predictable mean-reversion signal in the Indian equity market, and whether that signal is tradeable after costs.

A cross-sectional bucket analysis across **247,000+ observations** confirms a monotonic, statistically significant relationship between gap magnitude and subsequent intraday return direction (ρ = −0.06).

---

## Methodology

- **Signal:** Cross-sectional, price-based. Computed from publicly available OHLC data at market open.
- **Execution:** Enter at open, exit at close. Both long and short sides.
- **Universe:** NSE-listed equities, filtered to remove illiquid and erroneous data points.
- **Costs:** Fixed round-trip cost applied to every trade.
- **No lookahead:** Signal is fully known before the trading session begins.

The strategy is parameterised by a single threshold, swept across multiple values to validate robustness.

---

## Threshold Sensitivity

| Threshold | Trades | Avg Trade | Win Rate | Profit Factor |
|---|---|---|---|---|
| 1% | 38,276 | +0.16% | 54.5% | 1.18 |
| 2% | 10,669 | +0.35% | 55.2% | 1.31 |
| 3% | 4,733 | +0.56% | 55.2% | 1.47 |
| 5% | 1,280 | +0.93% | 58.5% | 1.63 |

Edge strengthens monotonically with threshold — consistent with a genuine mean-reversion signal rather than noise.

---

## Yearly Performance

| Year | Trades | Win Rate |
|---|---|---|
| 2015 | 725 | 60.0% |
| 2016 | 811 | 58.4% |
| 2017 | 461 | 59.0% |
| 2018 | 801 | 60.8% |
| 2019 | 590 | 52.7% |
| 2020 | 2,493 | 52.2% |
| 2021 | 963 | 54.1% |
| 2022 | 1,171 | 54.5% |
| 2023 | 518 | 48.5% |
| 2024 | 791 | 53.4% |
| 2025 | 695 | 61.9% |

Positive expectancy in 11 of 12 years. Performance is consistent across different market regimes, including the COVID volatility spike of 2020.

---

## Long vs Short Breakdown

|  | Trades | Avg Trade | Profit Factor |
|---|---|---|---|
| Long | 4,982 | +0.46% | 1.41 |
| Short | 5,687 | +0.25% | 1.22 |

Both sides are independently profitable, confirming the edge is not one-directional.

---

## Known Risks & Limitations

- **Survivorship bias:** Results may be overstated if the universe excludes delisted or suspended securities.
- **Execution:** Open and close prices on NSE are auction-determined; live slippage may exceed the assumed round-trip cost.
- **Concentration risk:** Drawdown is elevated on high-volatility days where the strategy takes a large cross-sectional book.
- **2026 YTD:** Recent months show below-average performance; regime shift being monitored.

---

## Tech Stack

- **Python** — NumPy, Pandas, Matplotlib
- **Data** — Daily OHLC, NSE universe
- **Analysis** — Cross-sectional bucketing, threshold sweep, rolling Sharpe, monthly/yearly attribution

---

## Author

**Malapaka Venkata Ratna Abhishek**
Astrophysics | Quantitative Researcher | Hyderabad, India
[GitHub](https://github.com/CuriousObservator) · [arXiv](https://arxiv.org/a/0009-0006-2553-6540) · mvrquant@gmail.com

---

*Strategy logic is not disclosed in this repository. This README presents performance and methodology at a level consistent with academic and professional communication.*
