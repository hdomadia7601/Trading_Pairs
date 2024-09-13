# Trading_Paris
This repository contains a comprehensive algorithmic trading strategy inspired by the Paris Trading model. The strategy is built to leverage arbitrage opportunities in stock or forex markets, focusing on capturing small price discrepancies between related financial instruments.
Overview of Pairs Trading Strategy As a market-neutral trading strategy, pairs trading entails finding two co-movable stocks and establishing opposing positions in each of them in an attempt to profit from brief alterations in their historical pricing patterns. The law of mean reversion, which says that prices will eventually return to their historical mean and the trader will profit from this convergence, is the foundation of this technique.

Components of Strategy Pair Selection: Finding two stocks with a high level of co-movement and correlation is the first step in pairs trading. Usually, this entails statistical tests like cointegration and correlation coefficients.

Signal Generation: After determining a pair, traders keep an eye on the difference in value between the two stocks. The price difference between the two equities after accounting for volatility is known as the "spread".

Trade Execution: When the spread reaches a predefined level, a trade is executed. One stock is overpriced in comparison to the other if the spread is unusually high or low. After that, the trader would short the overvalued stock and buy the undervalued one.

Risk management: To make sure that possible losses are maintained within reasonable bounds, appropriate risk management strategies are used. This covers restricting the size of positions and establishing stop-loss orders.

Exit Strategy: The positions are closed when the spread narrows down again, or based on specific profit targets or time frames.

**A. PAIR IDENTIFICATION AND SELECTION**
A pair is selected based on their good statistical arbitrage opportunities over time.
Correlation and cointegration are two key terms that we calculated to ensure that the stocks followed the necessary relative price movements, i.e., in line with good statistical arbitrage. 

Correlation: Correlation describes the relation between variables and is quantified by the correlation coefficient ρ, ranging from -1 to +1. A value of +1 indicates a perfect positive correlation, a value of -1 indicates a perfect negative correlation, and a value of 0 means there is no correlation. Correlation(X,Y) = ρ = COV(X,Y) / σ(X),σ(Y) Where, COV is covariance and σ is standard deviation.

Cointegration: A statistical feature of two or more time-series variables called cointegration shows whether a linear combination of the variables is stationary.Variance and mean, for example, are constant over time. Spread is equal to Y - n*X. Given that the hedge ratio is n. (The best scenario is spread = 0)

ANALYSIS TOOLS FOR PAIR SELECTION: Data from sites NSE (Nifty 50) are taken. Pairs of 2 stocks are checked for their sharpe ratio and CAGR. The pair with highest sharpe ratio and CAGR is selected. After that, we proceed further in the trading strategy. If the co-integration test meets our threshold statistical significance (in our case 5%), then that pair of tickers will be stored in a list for later retrieval. Libraries imported for downloading data for the past years are yfinance. This library provides extensive data regarding the stocks' opening price, closing price, adjacent close price, low price, and high price over the years for different stocks/tickers.

**B. THE SIGNAL GENERATION METHOD AND TRADING STRATEGY**



