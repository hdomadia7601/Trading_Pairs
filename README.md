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

Statistical arbitrage determines the optimal time to execute a trade. After determining the spread of both stocks, it is possible to determine the location of any notable departures from the mean. This will make it easier for us to classify the associated assets into two groups: the "lag" asset and the "lead" asset. Usually, the lead asset performs better than the lag asset. This strategy is predicated on the idea that the spread from pairs exhibiting co-integration qualities is mean reverting in nature, meaning that a considerable deviation from the mean will present opportunities for arbitrage.

Depending on how successful our trade is, the lead asset would take a long position (buy the stock, hoping that its price will increase later) and the lag asset would take a short position (sell the stock, hoping that its price will fall). This difference would give us a profit or loss. By computing the cumulative returns, Sharpe ratio, and compound annual growth rate (CAGR) for a pair of assets based on past price data supplied in a DataFrame, one can backtest the pairs trading method. 
Using the Kalman Filter, we performed a regression study to determine the hedge ratio (hr) between the two assets. Calculating the dynamic hedge ratio using the Kalman filter The process known as Kalman filtering, or linear quadratic estimation, or LQE, makes use of a sequence of measurements that are observed over time and may contain errors related to statistical noise. Through the estimation of a joint probability distribution over the variables for each time-frame, it generates estimates of unknown variables that are typically more accurate than those based on a single measurement alone.
Next, use y - (x * hr) to calculate the spread series. If we are interested in calculating the moving average, this can be used to smooth out estimations of other quantities.

The Z-score indicates the number of standard deviations the spread now deviates from its mean throughout the past. Next, we established Z-score thresholds for long and short positions at entrance and exit. determined the long and short entry and exit points using the Z-score criterion, and the opposite Z-score criteria.

# C. GENERATED TRADING SIGNALS AND POSITION SIZING

Logic of trading

Determine each pair's spread by multiplying Y by the hedging ratio * X. Regression using Kalman Filtering Function for figuring out the hedge ratio Utilizing rolling mean and standard deviation, compute the z-score of's' for the duration of 'half-life' intervals. Keep this as a z-score. To determine the half-life, use the half-life function. Establish the following: Z-scores for the upper and lower entries are 2.0 and 0.0, respectively. Go SHORT when Z-score passes the upper entrance Z-score; use Z-score return exit Z-score to terminate the situation. Proceed LONG; close the position with Z-score return exit Z-score when Z-score crosses lower entry Z-score. Perform a backtest on every pair and determine the performance metrics for each as the max drowns down. Sharpe proportion Assemble portfolios with a distribution of market values that is equal; the market value of each pair is the same.

# D. Backtesting

The back-test engine follows the steps:

Spread is equal to Y - hedging ratio * X. To compute the hedge ratio, use the Kalman Filter Regression Function. Utilizing rolling mean and standard deviation, compute the z-score of's' for the duration of 'half-life' intervals. Keep this as a z-score. Half life can be calculated using the half-life function. Assign the following values to the Z-scores: exit = -0.5, lower entry = -1.25, and upper entry = 1.25. Go SHORT when Z-score passes the upper entrance Z-score; use Z-score return exit Z-score to terminate the situation. Proceed LONG when the Z-score crosses the lower entry Z-score. 

Utilizing Z-score return exit Z-score D, close the location. PORTFOLIO PnL: A $100,000 starting capital is required. The number of shares that must be purchased for each stock is determined by taking into account both the original capital and the stock prices at the start of the trading session. Next, PnL is computed for Stock 1: A dataframe named "portfolio" is made to monitor different PnL components for stock 1. Based on the stock prices and cumulative positions (signals), the holdings for stock 1 are monitored.Following the purchase and sale of stock 1, the remaining funds are monitored. The total worth of stock 1 is determined by adding up all of the holdings, cash, and daily returns for the stock. PnL Estimation for Share 2: For stock 2, all the same variables are monitored and computed as they were for stock 1. The PnL of stocks 1 and 2, which are already stored, are added to determine the total PnL. After the NaN values are eliminated, the DataFrame is cleaned and then restored.


# E. METRICS OF PERFORMANCE

The Sharpe Ratio is a useful tool for evaluating an investment or portfolio's risk-adjusted return.It is frequently used to evaluate which assets or portfolios offer the best return while taking risk into account. * (Rp - Rf) / σp is the Sharpe Ratio (SR). where Rp is the portfolio's or investment's average return. Rf: The rate of return that is risk-free. σp: The standard deviation of the returns on the investment or portfolio. Since a greater sharpe ratio denotes a superior risk-adjusted return, it is often recommended.

CAGR: Assuming that the investment has been compounding, it is used to calculate the yearly growth rate of an asset or investment over a given time period.It provides you with a consistent method to assess the return on an asset or investment, even in cases where growth or returns fluctuate over time. CAGR is equal to (final value / starting value) ^ (1 / n) - 1 Whereas Ending Value is the asset's value at the conclusion of the given time frame. Beginning Value is the asset's initial value at the start of the given time frame. n = The total number of years during the duration. Typically, it is employed to estimate future returns or evaluate the past performance of investments.












