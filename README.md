# 📈 Mean-Reversion Strategy with EWMA (3-Lag) & Volatility Filter

This project implements a quantitative intraday trading strategy on minute-level data for TSLA and NVDA (April–June 2025). The strategy exploits temporary deviations from an Exponentially Weighted Moving Average (EWMA), filtered by local volatility levels to avoid entries during unstable market conditions.

---

## 🧠 Strategy Overview

- **Objective**: Capture short-term mean-reversion opportunities using a smoothed price baseline.
- **Core Idea**: When the price significantly deviates from a smoothed trajectory (EWMA with 3-lag structure), and volatility is below a threshold, the strategy enters a contrarian position.
- **Signal**:
  - **Long** if z-score < *n* and volatility < *vol_level*
  - **Short** if z-score > -*n* and volatility < *vol_level*
  - Else: flat
- **Execution**: Trades only on signal changes, with transaction costs accounted for.

---

## 🛠️ Technical Details

- **Data**: 1-minute OHLCV from Alpha Vantage via CSV for `TSLA` and `NVDA` (2025-04 to 2025-06)
- **Smoothing**: EWMA with lagged terms:
  \[
  \text{EWMA}_t = \alpha P_t + \beta \text{EWMA}_{t-1} + \theta \text{EWMA}_{t-2} + (1 - \alpha - \beta - \theta) \text{EWMA}_{t-3}
  \]
- **Z-Score Calculation**: Deviation from EWMA normalized by rolling standard deviation (60-min window)
- **Volatility Filter**: Rolling standard deviation compared to a predefined threshold
- **Sharpe Ratio**: Annualized using 252 × 390 observations (1-minute bars)
- **Transaction Costs**: Configurable (default 0.1%). It's really high but I wanted to test the robustness of my strategy.

---

## 📊 Performance Summary (Sample: NVDA, 1-min data)

| Metric                    | Strategy   | Buy & Hold|
|---------------------------|------------|-----------|
| Annualized Sharpe Ratio   | > 2.26     | 0.98      |
| Max Drawdown              | -61.71%    | -43.75%   |
| Cumulative Return         | Higher     | Lower     |
| Trades Executed           | Controlled | Passive   |

> 🏁 **Result**: Strategy consistently outperforms buy-and-hold over the sample period, with better risk-adjusted returns but with higher drawdown.

---

## 📁 Files

- `nvda_1min.csv` / `tsla_1min.csv`: Historical minute-level data
- `script.ipynb`: Main strategy logic, visuals, and performance metrics

---

## 📌 Future Improvements

- Hyperparameter optimization (alpha, beta, threshold n)
- Optimization of the strategy in order to adapt to different market conditiosn (My strategy became a little bit innacurate at one point)
- Backtest on multiple timeframes (5m, 15m)
- Maybe a live test with paper trading
---

<img width="1918" height="773" alt="image" src="https://github.com/user-attachments/assets/10f96d02-8d13-4022-85b1-996b182b92b3" />

## 🧠 Author

Yassine Housseine — Quantitative Finance Student  
[📫 LinkedIn](www.linkedin.com/in/yassine-housseine-181835210)
