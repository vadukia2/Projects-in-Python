# **Projects-in-Python - Bollinger Bands Strategy**
This repository showcases some of the code I have written in the Python language

##  Discription

What are Bollingers Bands? 
Bollinger Bands are one of the many indicator tools used in Visual Analysis. Created in the 1980s by John Bollinger, the purpose of the bands is to define high and low prices in the market. High prices are represented by the upper band and low prices by the lower band. The middle band acts as a simple moving average between the two other bands. When the bands are analyzed, they aids in pattern recognition as well as price action comparison which can be viewed simultaneously with other indicators to come to a conclusion.

### **Strategy implemented in this project**

In our model, the upper and the lower band are set 2 standard deviations apart from the 20-day moving average of the QQQ ETF fund. 
As per Bollinger Bands strategy: 
-When the stock price is above the upper band, we sell the stock.
-When the stock price is between the 20-day moving average and the upper band, we buy the stock. 
-When the stock price is below the lower band, we buy the stock. 
-When the stock price is between the 20-day moving average and the lower band, we sell the stock.

#### **Motivation**
To test different strategy applied by investors in the stock markets and compare their performance. 


##### **Code**

```python
# Installation of required modules
import pandas as pd
import pandas_datareader as pdr
import matplotlib.pyplot as plt
import numpy as np

# Importing data
qqq = pdr.get_data_yahoo('QQQ',start='2018-01-01',end='2020-10-31')

# Main Code

qqq['ma_20'] = qqq['Adj Close'].rolling(window=20).mean()
qqq['Std'] = qqq['Adj Close'].rolling(window=20).std()
qqq.dropna(inplace=True)
qqq['return'] = qqq['Adj Close']/qqq['Adj Close'].shift(1) -1



#Upper and Lower bands of Bollinger Bands
qqq['Upper band'] = qqq['ma_20'] + 2*qqq['Std']
qqq['Lower band'] = qqq['ma_20'] - 2*qqq['Std']


qqq['BB Strategy(upper)'] = np.where(qqq['Adj Close']>qqq['Upper band'],-1,0)


qqq['BB Strategy(within the range)'] = np.where((qqq['Adj Close']<qqq['Upper band']) & 
                                                (qqq['Adj Close']>qqq['ma_20']),1,0)


qqq['BB Strategy(within the range2)'] = np.where((qqq['Adj Close']<qqq['ma_20']) & 
                                                 (qqq['Adj Close']>qqq['Lower band']),-1,0)


qqq['BB Strategy(lower)'] = np.where(qqq['Adj Close']<qqq['Lower band'],1,0)

qqq['BB Strategy(total)'] = (qqq['BB Strategy(upper)'] + 
                            qqq['BB Strategy(lower)'] + 
                            qqq['BB Strategy(within the range)'] + 
                            qqq['BB Strategy(within the range2)'])
            
            
qqq['BB Strategy Return'] = qqq['BB Strategy(total)'].shift(1)*qqq['return']
qqq['BB Strategy Cummulative Return'] = qqq['BB Strategy Return'].add(1).cumprod().sub(1)


qqq['Cum return'] = qqq['return'].add(1).cumprod().sub(1)

plt.figure(figsize=(20,10))
qqq['Cum return'].plot(color='red')
qqq['BB Strategy Cummulative Return'].plot(color='blue')
plt.legend(['Buy and Hold','BB Strategy'])
plt.show()
```
**Please see the executed code here:**
[Visit executed code](https://github.com/vadukia2/Projects-in-Python/blob/main/Bollinger%20Bonds%20strategy.ipynb)


###### **Purpose of the code**
The Code compares the performance of Bollingers Bands strategy with the Buy and holds strategy on Nasdaq's (QQQ) stock price.    


####### **Conclusion**
Though BB strategy is no longer widely used, it has outperformed the popular buy and hold strategy in the last 12 months, especially after COVID.
