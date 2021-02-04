# Projects-in-Python
This repository shocases some of the code i have written in Python language

##  Discription
Whats is Bollingers Band? 
Bollinger Bands are one of many indicator tools used in Visual  Analysis. Created in the 1980’s by  John Bollinger, the purpose of the  bands is to provide a definition of  high and low prices in the market.
High prices are represented by  the upper band and low prices  by the lower band. The middle  band acts as a simple moving  average between the two other  bands.
When the bands are analyzed, it  aids in pattern recognition as well  as price action comparison which  can be view simultaneously to  other indicators in order to come to  a conclusion as to the movement of  the market at that time.

### Strategy implemented in this project.
In our model the upper and the lower band are set 2 standard deviation apart from the 20-day moving average of QQQ ETF fund.
As per Bollinger Bands strategy:
-When the stock price is above the upper band, we sell the stock.
-When the stock price is between the 20-day moving average and the upper band, we buy the stock.
-When the stock price is below the lower band, we buy the stock.
-When the stock price is between the 20-day moving average and the lower band, we sell the stock.

#### Motivation
To test different strategy applied by investors in the stock markets and compare their performance. 


##### Purpose of the code
The Code compares the performance of Bollingers Bands strategy with the Buy and hold strategy on Nasdaq's (QQQ) stock price.  


###### Conclusion
Though BB strategy is no longer widely used, it has out performed the popular buy and hold strategy in the last 12 months especially after COVID. 
