# AAPL Covered Call Strategy Backtest

## Project Overview
- This project backtests a Cash-Secured Put (CSP) strategy on Apple (AAPL) from 2018 to 2024. The strategy evolved from a standard income-focused model to a Reinvestment Hybrid Model, where realized option premiums are reinvested into AAPL stock

## Mathmatical Modeling
- Premium is calculated as:
$$Premium \approx 0.3 \cdot Strike \cdot \sqrt{\frac{DTE}{365}} \cdot \sigma$$
- The reinvestment model: instead of holding cash, the model simulates purchasing AAPL shares at the moment of trade exit.For every trade $i$ that closes, the profit $PnL_i$ is tracked. Its profit or loss to the final portfolio value is calculated as:$$Gain_i = PnL_i \times \frac{Price_{final} - Price_i}{Price_i}$$


## Strategy Parameters
- Ticker: AAPL
- Initial capital: $100,000
- Days till expiration: 30
- Profit Rarget: when open market gain hits 50% --> rollout and realize the gain
- Leverage: 0.5 (Utilizing 50% of available capital for collateral to maintain a cash safety net)
- Risk free rate: the return you would get from just leaving cash in a savings account

## Performance Analysis
- The hybrid model shows that 8% OTM strikes is the most optimal for AAPL.

    - Volatility Dampening: While AAPL experienced significant drops in 2020 and 2022, the strategy's Max Drawdown remained under 8% of the total account value.


## Key Features
- Data Acquisition: Automatically downloads historical AAPL stock data using the yfinance library.
Volatility Calculation: Calculates annualized historical volatility using pandas and NumPy (np.sqrt(252) logic).
- Backtesting Engine: Simulates the opening and closing of options positions every 30 days (DTE=30), utilizing specific entry/exit logic and a "time machine" loop structure.
- Performance Analysis: Uses pandas DataFrames to track individual trade results and visualize overall portfolio performance.

## Future Enhancements
- Dynamic OTM Scaling: Adjusting the strike buffer based on the VIX (Volatility Index).
- Tax Drag Simulation: Accounting for short-term capital gains tax on option premiums.
- The Wheel Strategy: Implementing a "Covered Call" leg if the Put is assigned (Full Wheel).

## Technologies Used
- Python
- Pandas
- NumPy
- yfinance
- Matplotlib
