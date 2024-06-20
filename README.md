# Supertrend Strategy With Bayesian Optimization

## Overview

This repository contains the implementation of a trading strategy based on the Supertrend indicator, optimized using Bayesian optimization techniques. The goal of this strategy is to identify market trends and make informed trading decisions.

## Supertrend Indicator

The Supertrend Indicator is a popular technical analysis tool used to identify market trends. It combines the Average True Range (ATR) with a multiplier (ATR Multiplier) to calculate its value.

### Formula
Supertrend = (High + Low) / 2 + ATR Multiplier * ATR Period


- **ATR Multiplier** determines the sensitivity of the Supertrend line to price fluctuations.
- **ATR Period** influences the responsiveness of the Supertrend line to recent price movements.

## Calculations

### True Range (TR)

True Range (TR) is the maximum of:
1. Difference between the highest and lowest price of the current trading day.
2. Difference between the closing price of the previous trading day and the highest price of the current trading day.
3. Difference between the closing price of the previous trading day and the lowest price of the current trading day.

### Actual True Range
Actual True Range = TR.rolling(window=ATR Period).mean()


### Bands

- **Upper band**: `(High + Low) / 2 + ATR Multiplier * ATR Period`
- **Lower band**: `(High + Low) / 2 - ATR Multiplier * ATR Period`
- **Middle band**: `(Upper band + Lower band) / 2`

## Trading Strategy Assumptions

- **Mean Reversion**: The middle band serves as the mean, with prices oscillating between the upper and lower bands and reverting to the mean.
- **Upper Band (Resistance Line)**: When the price approaches or exceeds the upper band, it indicates an overbought condition where a pullback or reversal might occur.
- **Lower Band (Support Line)**: When the price approaches or falls below the lower band, it indicates an oversold condition where a bounce or reversal might occur.
- **Middle Band (Average Line)**: The middle band represents the mean price level and serves as a target for price reversion.

## Trading Strategy

### No Existing Position

- **Long Signal**: Enter a long position when the closing price is less than the lower band, assuming the price will rebound from an oversold condition and move upwards.
- **Short Signal**: Enter a short position when the closing price is greater than the upper band, assuming the price will pull back from an overbought condition and move downwards.

### Currently Long or Short

- End position as soon as the closing price hits the middle band.

## Supertrend Strategy Setup

### Data

- **Date range**: 05/27/2007 to 05/27/2024
- **Frequency**: Daily
- **Dataset includes**: MSFT, AMZN, CSCO, TXN
- **Source**: Historical prices acquired from Yahoo Finance
- **Train set**: 05/27/2007 - 05/27/2020
- **Test set**: 05/27/2020 - 05/27/2024

### Model Development

1. Calculate Supertrend.
2. Implement optimization in the train set and apply tuned parameters in the test set.
3. Build performance metrics of Total Return, Annual Return, Sharpe Ratio, and Maximum Drawdown.
4. Compare strategy cumulative return with the benchmark (S&P500).

### Optimization

- **ATR Multiplier** ranges from 1 to 5.
- **ATR Period** ranges from 5 to 30.
- **Objective Function**: Maximize annual return.
- **Package**: `skopt.gp_minimize`

## Conclusion

This repository demonstrates the application of the Supertrend indicator in a trading strategy, with parameter optimization achieved through Bayesian techniques. The performance of the strategy is evaluated using key financial metrics and compared to a benchmark.

---





