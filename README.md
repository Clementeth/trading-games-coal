# Coal Trading Games — Statistical Arbitrage in Coal Equities

## Introduction

This project is an academic study of statistical arbitrage applied to coal-related equities.

It is inspired by Rafael Palazzi (2025), *Trading Games: Beating Passive Strategies in the Bullish Crypto Market* (https://onlinelibrary.wiley.com/doi/full/10.1002/fut.70018), and its associated implementation:  
https://github.com/rafaelpalazzi/trading-games-crypto

Palazzi develops an enhanced pairs trading framework based on cointegration, combining systematic pair selection, parameter optimization, and risk controls (volatility filters and trailing stop-loss). His results show that such strategies can outperform traditional pairs trading and passive benchmarks on a risk-adjusted basis.

This project adapts a simplified version of this approach to the coal equity market, focusing on pair selection, mean-reversion dynamics, and backtesting.

---

## Project Structure

- `Data_Analyse.ipynb`: exploratory analysis and pair selection  
- `pair_trading.ipynb`: strategy implementation and backtesting  

---

## Data Analysis and Pair Selection

- data cleaning and alignment  
- return computation  
- correlation analysis  
- outlier detection  
- stationarity testing (ADF)  
- cointegration testing  

Correlation is used as a first filter, but cointegration is required to identify stable long-run relationships.

---

## Strategy Design

- spread construction  
- z-score normalization  
- entry and exit signals based on deviations from equilibrium  
- simple trading rules  

The implementation remains intentionally simple compared to Palazzi’s full framework.

---

## Backtesting

- position tracking  
- cumulative returns  
- comparison across pairs  
- sensitivity to thresholds  

No transaction costs or slippage are included.

---

## Performance and Risk

- cumulative returns  
- return distribution  
- drawdowns  
- Sharpe ratio  
- Calmar ratio  
- VaR / CVaR  

---

## Results

- cointegration improves pair relevance but does not ensure profitability  
- some pairs show stable mean-reversion, others break down  
- performance is highly dependent on pair selection  
- NRP and ARLP show relatively consistent behavior  

---

## Data

The dataset is structured around a coal benchmark and a set of related equities and sector proxies.

The main anchor is Newcastle Coal Futures, located in:
`coal_data/the_primary_anchor/Newcastle Coal Futures Historical Data.csv.xls`

The equity universe is stored in `coal_data/individual_universe/` and includes the following tickers:
AMR, ARLP, BHP, BTU, HNRG, NC, NRP, RIO, TECK

Two additional files (WHC_AU and YAL_AU) are present but contain no usable observations and are excluded from the analysis.

Sector proxies are stored in `coal_data/sector_proxies/` and include:
GNR, IXC, XLE

Equity and proxy datasets contain daily OHLCV data (Date, Open, High, Low, Close, Volume) over the period 2021-03-08 to 2026-03-05.  
The Newcastle coal futures dataset contains daily market data (Date, Price, Open, High, Low, Vol., Change %).

The analysis is performed on closing prices: Close for equities and proxies, and Price for coal futures.  
All time series are converted to datetime format, indexed by date, cleaned, and aligned to ensure consistent pairwise comparisons.

The empirical setup focuses on pairs formed between coal futures and each equity, with sector ETFs used as reference benchmarks during the exploratory phase.

---
## Usage

Run the notebooks in order:

```bash
1. Data_Analyse.ipynb
2. pair_trading.ipynb
