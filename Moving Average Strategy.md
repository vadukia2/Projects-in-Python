# **Projects-in-Python - Moving Average Strtegy**
This repository showcases some of the code i have written in Python language

##  Description
Whats are Moving Averages? 
-A moving average is a technical analysis technique that smooths price data by calculating a
 constantly updated average price.
A crossover is the most basic type of signal for trading. This crossover represents a change in momentum and can be used as a point of making the decision to enter or exit the market.

**Two forms of crossover**
-The simplest form of a crossover is when the price of an asset moves from one side of a moving  average to the other.
-A second type of crossover, referred to as a dual moving average crossover, occurs when a short-term average crosses a long-term average.

**Buy and sell signals**
A buy signal is generated when the short-term average crosses the long-term average and rises  above it
A sell signal is triggered by a short-term average crossing long-term average and falling below it.



#### **Motivation**
To test different strategies applied by investors in the stock markets and compare their performance. 


##### **Code**

```python
# Installation of modules
import numpy as np
import pandas as pd
import pandas_datareader as pdr
import matplotlib.pyplot as plt

# Moving Average Strategy for any stock. If the lower moving average is bigger than the higher moving average we buy else sell 
def strategy(ticker,n1,n2):
    df = pdr.get_data_yahoo(ticker, start='2010-01-01',end='2018-12-31')[['Adj Close']]
    df['return'] = np.log(df['Adj Close'] / df['Adj Close'].shift(1))
    df['mv1'] = df['Adj Close'].rolling(n1).mean()
    df['mv2'] = df['Adj Close'].rolling(n2).mean()
    df.dropna(inplace=True)
    df['position'] = np.where(df['mv1'] > df['mv2'], 1 , -1)
    df['strategy'] = df['position'].shift(1) * df['return']
    df[['return','strategy']].cumsum().apply(np.exp).sub(1).plot(figsize=(20, 10))
    plt.show()

# example
strategy('AAPL',42,252)

```
**Please see the executed code here:**
[Visit executed code](https://github.com/vadukia2/Projects-in-Python/blob/main/Moving%20Average%20Strategy.md)


###### **Purpose of the code**
The Code compares the performance of the Moving Average Strategies with the Buy and Hold strategy on any stock price with a ticker.  

######## **Conclusion**
Using these few lines of code, one can estimate the performance of the moving average strategy compared to the traditional buy and hold strategy for any stock out there.
