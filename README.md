# Crypto_persistence_strategy

This strategy generates “persistence signals “for the ETH coin. A quant indicator known as the Hurst Exponent is calculated and applied to the daily closing prices. The Hurst value indicates the following:
1.	If the value is = 0.5, then the time series is random.
2.	If the value is < 0.5, then the time series is mean reverting.
3.	If the values is > 0.5, then the time series is trending.
An RSI indicator is used to gauge overbought and oversold conditions in the market. The logic of persistence is such that:
Buy signal:
1.	RSI > 75 and hurst exponent > 0.65
2.	RSI < 25 and hurst exponent < 0.35
Short signal:
1.	RSI > 75 and hurst exponent < 0.35
2.	RSI < 25 and hurst exponent > 0.65

Exit signal:  when RSI reaches between 55 and 45 for all the cases.
The buy signal is generated when the RSI is overbought and Hurst > 0.65. It implies that the time series is trending and will continue to do so. Also,
The buy signal is generated when the RSI is oversold and Hurst < 0.35. It implies that the time series will mean revert until the exit condition is triggered.
The opposite is true for short signals.

The back-test is run on daily closing prices for the ETH coin downloaded from a free API source.
The max download limit from the API is 2000 bars. Hence the back-test was run on the most recent 2000 bars.
The back-test is written in an event driven methodology wherein:
1.	The rolling 240 bar Hurst values are calculated.
2.	The 14 period RSI is calculated.
3.	A for loop iterates over each row checking for buy, short and exit signals.
4.	All the trades are recorded in a trade log data-frame.
5.	The cumulative returns of the strategy are calculated and plotted.
6.	 Finally, the cumulative returns of the strategy are compared against the buy and hold returns of the ETH coin.
The performance metrics of the strategy follow next as generated from the back-test code:

![image](https://github.com/user-attachments/assets/ab724d16-590c-4519-b639-b72145d612fe)

![image](https://github.com/user-attachments/assets/44381b3c-1aa4-495d-b9ee-89e808c82fd0)

The strategy incorporates slippage costs as well.
The strategy has underperformed a simple buy and hold strategy of the ETH coin. However, it has a better max drawdown and Calmar ratio.


