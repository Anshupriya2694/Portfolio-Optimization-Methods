## Portfolio Rebalancing Techniques

### Introduction

Modern Portfolio Theory is the cornerstone of portfolio risk management, because the efficient frontier is a standard method of assessing both investor risk tolerance and market risk-return tradeoffs. To compute the efficient frontier, both expected returns and the covariance matrix of the portfolio are required. Portfolio optimization relies upon an unbiased and efficient estimate of asset covariance.
This project uses two models - ARIMA and Neural Networks to predict stock prices and assign weights for an optimal portfolio optimization. This experiment also accounts for the economic crisis of 2007-2009 and the current COVID pandemic. The aim is to create a portfolio with lowest possible volatility. 

### Data

Data has been sourced from Yahoo Finance, Consumer Finance and Coronavirus Source Data. Daily Stock prices for financial services firms – Citigroup, JP Morgan, Morgan Stanley and Goldman Sacs from 2005 to present has been extracted from Yahoo finance. To study of effect of the 2008 housing crisis, delinquency data from Consumer Finance is used. Also, data about COVID-19 (starting March 2020) is also being used.

### Methodology and Results

Initial analysis of the data

1.	Volatility in stocks: Volatility is the degree of variation of trading prices over-time. We can see that there is a spike in volatility between 2008 to 2009 and in the early months of 2020. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.11.46%20AM.png)

2.	Closing price: The closing price is the last price at which a stock is traded during a regular trading day. The stock prices for Goldman Sacs are very volatile. However, they seem to be oscillating within a fixed range of closing prices. The stocks for Citi group show a sharp decline around 2009 and have not recovered yet. JP Morgan and Morgan Stanley seem to be relatively stable despite two economic crises between 2005 and 2020.

3.	Daily Returns (based on equal weighted portfolio): Percentage change in stock prices compared to previous day. High variations create a loss in confidence and indicate uncertainty of an asset. High variations can be observed between 2008 to 2009 and early months of 2020. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.12.07%20AM.png)

4.	Exposure to Risk: Risk exposure refers to the amount of risk an investor has taken on a particular investment. It refers to the quantified loss potential of an investment or activity. The calculated risk exposure is also very high during 2008 and 2020 as well.

![](Images/Screen%20Shot%202020-11-19%20at%2010.12.15%20AM.png)


### Study the impact of 2007-2008 Financial Crisis on chosen portfolio

During 2007-2008, the volatility in stock prices increased greatly. This can be seen from the covariance matrix that Citigroup shows the highest covariance followed by Morgan Stanley.

![](Images/Screen%20Shot%202020-11-19%20at%2010.12.26%20AM.png)

The graphs below show the delinquency rate from 2008 to 2010. Delinquency rate refers to the percentage of loans that are past-due. There is a sharp increase in delinquency rate from 2008 onwards. It has taken a long time to get it back to an acceptable level. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.12.34%20AM.png)

Initial assessment indicates that there is little correlation between average returns and mortgage delinquencies, but a strong negative correlation exists between minimum returns and delinquency.

![](Images/Screen%20Shot%202020-11-19%20at%2010.12.42%20AM.png)

To quantify the effect of the housing crisis on this portfolio, a regression analysis is performed with respect to average monthly portfolio returns, minimum monthly returns and monthly volatility. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.12.51%20AM.png)

Mortgage delinquencies are acting as a systematic risk factor for both minimum monthly returns and average volatility of returns (p-value), but not for average monthly returns. The R-squared goodness of fit isn't high in any case, but a model with more factors would likely generate greater explanatory power.

Using the modern portfolio theory, an efficient frontier is created. The dataset is broken into three parts for this analysis. These three will help analyze the covariances in returns of assets in the portfolio. The three parts are:
1.	Before Recession: 2005 to 2006
2.	During Recession: 2007-2008
3.	After Recession: 2009-2010

![](Images/Screen%20Shot%202020-11-19%20at%2010.13.00%20AM.png)

The breakdown of the 2005 - 2010 period into sub-periods shows how the portfolio's risk increased during the crisis, and this changed the risk-return trade-off after the crisis. Using the information on covariance and expected returns (calculated earlier) the efficient frontier can be made. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.13.10%20AM.png)

### Study the impact of COVID-19 on chosen portfolio

The covariance matrix during COVID also shows high volatility in Citigroup stocks when compared to Goldman Sacs, JP Morgan and Morgan Stanley. However, the volatility is lesser than that of the 2008-2009 crisis. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.13.18%20AM.png)

There isn’t enough data available for the delinquency rate in 2020. The latest updated data only contains value till March. According a National Delinquency Survey, the 90-day delinquency is currently at 3.72 percent. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.13.27%20AM.png)

Initial assessment indicates that there is little correlation between average/minimum returns and number of COVID cases.

![](Images/Screen%20Shot%202020-11-19%20at%2010.13.35%20AM.png)

![](Images/Screen%20Shot%202020-11-19%20at%2010.36.29%20AM.png)

Increasing COVID cases are acting as a systematic risk factor for both minimum monthly returns and average volatility of returns (p-value), but not for average monthly returns. The R-squared goodness of fit isn't high in any case, (better than 2008-2009 data however) but a model with more factors would likely generate greater explanatory power.

![](Images/Screen%20Shot%202020-11-19%20at%2010.13.44%20AM.png)

### Using Python Library Pypopt to calculate optimal weights and risks on entire Dataset

In the third step, all the data points (2005 – 2020) are analyzed. For this analysis covariance shrinkage is used to shrink large errors to improve efficiency. The Covariance matrix produced as a result of this analysis will give an idea of asset returns. The efficient covariance matrix over stock prices from 2005 to 2020:

![](Images/Screen%20Shot%202020-11-19%20at%2010.13.51%20AM.png)

The variance of the stock prices of Morgan Stanley and Citigroup is the highest. However, when compared to the economic crisis and COVID, the variance is low. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.13.59%20AM.png)

### Using ARIMA and Neural Networks to forecast stock prices

An ARIMA model with lag value set to 5 for autoregression, a difference order of 1 to make the time series stationary, and a moving average model of 0 is created. Along with an ARIMA model, a neural net is designed with 4 inputs and 4 outputs. There are two hidden layers or size 16 in this model. The model is computing loss in mean squared logarithmic error and rmsprop is used as the optimizer. 

Both these models read the asset prices from the test dataset (70% of the entire data) as the input and test it to predict stock prices (30% of the dataset).

The predictions by these models are shown below:

![](Images/Screen%20Shot%202020-11-19%20at%2010.14.09%20AM.png)

It is very evident that ARIMA follows the actual prices very closely. Mean Squared error is used to evaluate the performance of both models. The MSE of Neural Net is 295.69 which is a very high value. ARIMA has a fairly low MSE of 5.07. 

The covariances for ARIMA and Neural Net model are also fairly close to that of the Actual. ARIMA’s predictions are closer to that of Actual visually. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.14.17%20AM.png)

Comparing the efficient boundaries, it can be seen that ARIMA is mimicking the actual efficient boundary. However, ARIMA seems to be slightly overestimating returns. The neural network on the other hand is underestimating returns. While estimating weights, both models assign the same weights despite differences in return estimation. These weights have been calculated to ensure minimum volatility. 

![](Images/Screen%20Shot%202020-11-19%20at%2010.14.27%20AM.png)

From the entire analysis, it looks like Goldman Sacs and JP Morgan the most stable stock throughout. Even during an economic crisis, the most efficient weights suggest acquiring larger weights of these two stocks. 

### Future Work

The effect of an economic crisis requires analysis of more variables to explain the phenomenon in depth. 
The neural network model needs to be tweaked to be able to perform as well as or better than ARIMA. A good neural net model will be able to auto-balance portfolios to either minimize risk or increase returns based on the consumers risk tolerance. 

### Acknowledgement 
Datacamp Course - Quantitative Risk Analysis
