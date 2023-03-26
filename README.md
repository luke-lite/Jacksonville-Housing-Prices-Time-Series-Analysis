# Jacksonville Housing Prices Time Series Analysis
## Luke DiPerna
### January, 2023
![jax_skyline](https://github.com/luke-lite/Jacksonville-Housing-Prices-Time-Series-Analysis/blob/b13235d253d31b86c32ed238273c4c6157d5fa03/jax_skyline.jpg)

## Project Goal
The goal of this project is to use time series data from Zillow to forecast home prices in Jacksonville, Fl. I will take the role of an analyst for a real estate consulting agency. The agency specializes in helping clients relocate in a relatively short time frame. The current client I am working with is a contractor who just agreed to a 2-year contract with a company based in Jacksonville, Fl.

The contract starts in 3 months, so the client would like to be in their new home by that time. They have a budget of $275,000. Additionally, there is a chance that they will be relocating again at the end of the current contract, so they would like to buy a home that will offer the best ROI if they need to sell it in 2 years time. My job is to help narrow the search by identifying zip codes in the Jacksonville area that meet the clients criteria. Once this is done, the client can make an informed choice while considering other options (commute time, neighborhood, convenience, etc.).

## Table of Contents

- [Understanding the Data](#Understanding-the-Data)
- [Exploratory Data Analysis (EDA)](#Exploratory-Data-Analysis(EDA))
- [Time Series Analysis](#Time-Series-Analysis)
    - [Naive Model](#Naive-Model)
    - [Model Building](#Model-Building)
        - [Train-Test Split](#Train-Test-Split)
    - [Model Forecasting](#Model-Forecasting)
    - [Forecasting Every Zip Code](#Forecasting-Every-Zip-Code)
- [Results](#Results)
- [Final Recommendation](#Final-Recommendation)
- [Appendix](#Appendix)
    - [Additional Data](#Additional-Data)
    - [Economic Conditions](#Economic-Conditions)
    
## Understanding the Data

The main dataset is a collection of monthly median housing prices from Zillow dating back to 1996 and grouped by zip code. The data has been smoothed and the seasonality has been removed. I trimmed the data to only include the 56 zip codes in the Jacksonville Metropolitan area. After accounting for the client's budget, I was left with 14 zip codes.

In the Appendix, I use additional seasonal data from Zillow to demonstrate how a more nuanced analysis could be performed. Unfortunately, most of the seasonal data only goes back to 2018 is not available by zip code, but it still offers some insight when forecasting future house prices.

## Exploratory Data Analysis

After preparing the data, it was ready to be visualized and modeled. Below is the median house price for each zip code in the Jacksonville area.

![jax_zc_housing_prices](https://github.com/luke-lite/Jacksonville-Housing-Prices-Time-Series-Analysis/blob/b71d6a5a0157278315105e8d8091807c4c70d5d5/Graphs/jax_zc_housing_prices.png)

After a more detailed discussion with the client regarding their budget range, I limited the analysis to only include the 14 zip codes with a current price between $200,000 and $300,000.
