# Jacksonville Housing Prices Time Series Analysis
## Luke DiPerna
### January, 2023
![jax_skyline](https://github.com/luke-lite/Jacksonville-Housing-Prices-Time-Series-Analysis/blob/b13235d253d31b86c32ed238273c4c6157d5fa03/jax_skyline.jpg)

## Project Goal
The goal of this project is to use time series data from Zillow to forecast home prices in Jacksonville, Fl. I will take the role of an analyst for a real estate consulting agency. The agency specializes in helping clients relocate in a relatively short time frame. The current client I am working with is a contractor who just agreed to a 2-year contract with a company based in Jacksonville, Fl.

The contract starts in 3 months, so the client would like to be in their new home by that time. They have a budget of $275,000. Additionally, there is a chance that they will be relocating again at the end of the current contract, so they would like to buy a home that will offer the best ROI if they need to sell it in 2 years time. My job is to help narrow the search by identifying zip codes in the Jacksonville area that meet the clients criteria. Once this is done, the client can make an informed choice while considering other options (commute time, neighborhood, convenience, etc.).

## Table of Contents

- [Understanding the Data](#Understanding-the-Data)
- [Exploratory Data Analysis](#Exploratory-Data-Analysis)
- [Time Series Modeling](#Time-Series-Modeling)
    - [Model Forecasting](#Model-Forecasting)
    - [Forecasting Every Zip Code](#Forecasting-Every-Zip-Code)
- [Results](#Results)
- [Final Recommendation](#Final-Recommendation)
- [Appendix](#Appendix)
    - [Additional Data](#Additional-Data)
    - [Economic Conditions](#Economic-Conditions)
    
## Understanding the Data

The main dataset is a collection of monthly median housing prices from Zillow dating back to 1996 and grouped by zip code. The data has been smoothed and the seasonality has been removed. I trimmed the data to only include the 56 zip codes in the Jacksonville Metropolitan area. After accounting for the client's budget, I was left with 14 zip codes.

I chose to remove the data prior to 2012. This is because this timeframe best captures the current state of the housing market. Prior to 2012, the housing market was tumultous due to the global financial crisis and housing bubble in 2008.

In the Appendix, I use additional seasonal data from Zillow to demonstrate how a more nuanced analysis could be performed. Unfortunately, most of the seasonal data only goes back to 2018 is not available by zip code, but it still offers some insight when forecasting future house prices.

## Exploratory Data Analysis

After preparing the data, it was ready to be visualized and modeled. Below is the median house price for each zip code in the Jacksonville area.

![jax_zc_housing_prices](https://github.com/luke-lite/Jacksonville-Housing-Prices-Time-Series-Analysis/blob/b71d6a5a0157278315105e8d8091807c4c70d5d5/Graphs/jax_zc_housing_prices.png)

After a more detailed discussion with the client regarding their budget range, I limited the analysis to only include the 14 zip codes with a current price between $200,000 and $300,000. I then calculated the past 3-year and 6-year ROI for each zip code:

![past_roi_3_and_6](https://github.com/luke-lite/Jacksonville-Housing-Prices-Time-Series-Analysis/blob/c3b67cd8a48eeea0d8f20253c606dec1e70c7aae/Graphs/past_roi_3_and_6.png)

## Time Series Modeling

After examining the data, I decided to create a train-test split of 80-20. This was a key decision because of the difference in price growth between the two splits, which can be seen here:

![train_test_split](https://github.com/luke-lite/Jacksonville-Housing-Prices-Time-Series-Analysis/blob/c3b67cd8a48eeea0d8f20253c606dec1e70c7aae/Graphs/train_test_split.png)

Starting around 2021, the housing prices begin to increase at a much faster rate before flattening out in the last few months. There are several factors for this, but the biggest one is the effect of the COVID pandemic and the resulting economic policies, such as a drastic and long laasting reduction in the interest rate, which contributed to a rapid rise in house prices.

By training a model on pre-pandemic data, it is almost guaranteed to struggle at accounting for the change in price growth in the test set. Ultimately, I have decided to still create a model based on the training set because I believe that data is more indicative of the long term housing price growth, and as I demonstrate in the Appendix, it appears that the market is undergoing a correction that will likely return it to pre-pandemic levels.

I used the average median house price data from all Jacksonville zip codes to train and test an initial model, which made the following predictions:

![train_model_pred](https://github.com/luke-lite/Jacksonville-Housing-Prices-Time-Series-Analysis/blob/c3b67cd8a48eeea0d8f20253c606dec1e70c7aae/Graphs/train_model_pred.png)

As expected, it was unable to anticipate the increase in price growth in the test set. However, I used the same parameters when training a model on the entire dataset, as it provided the best results. The diagnostics of the model trained on the entire set are shown below, and display the expceted issues of an increase in residuals at the tail end, and deviation in the QQ-plot and correlogram:

![X_model_diag](https://github.com/luke-lite/Jacksonville-Housing-Prices-Time-Series-Analysis/blob/c3b67cd8a48eeea0d8f20253c606dec1e70c7aae/Graphs/X_model_diag.png)

