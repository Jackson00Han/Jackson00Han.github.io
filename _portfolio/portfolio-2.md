---
title: "European Electricity Price Forecasting"
excerpt: "Day-ahead electricity price forecasting using multiple ML models; XGBoost vs. LSTM. <br/><img src='/images/electricity.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2024-09-25
permalink: /portfolio/item-2/
---

This is a brief intro about my recent project where I trained a robust model to forecast **day-ahead hourly electricity prices**.  
The goal: predict the next 24 hours of prices using historical prices, load, generation mix, and weather.

### Data

The data ranges from 2015 to 2019. The diagram below shows that even at a daily scale, the price series shows sharp spikes and shifting levels, making it very challenging to forecast reliably.

![Price actual (daily average)](price_actual_daily_average.png)
![Price by weekday and hour](price_weekday_hour.png)







### Model and setup

I tried a few approaches (including an LSTM) based on darts, the best performing model was **XGBoost with quantile regression**:

- Input features:  
  - time features (hour, day of week, month),  
  - lagged prices and load (e.g. 24h, 48h, 168h)
  - generation mix and weather variables.
  - derived features (rolling mean, std, diff, min, max, etc.)
- Output:  
  - median price forecast,  
  - plus prediction intervals (e.g. 5% and 95% quantiles).

The main baseline I compare against is very simple:  
**Baseline**: “tomorrow’s price at the time hour _h_ = yesterday’s price at hour _h_”.

---

### Results

On a held-out test period, the XGBoost model:

- reduces **MAE by ~28%** vs the naïve “yesterday” baseline,  
- reduces **RMSE by ~30%**,  
- produces **90% prediction intervals** with coverage close to 90%.


Below is an example of the forecast vs actual prices for a few days on validation set:

![validation forecasts](xgb_lstm_val.png)

_**Figure 1.** The model tracks the daily pattern and general level of prices quite well, but very sharp spikes are still hard to predict._

Here is the forecasting by the final model on test set:

![test forecasts](xgb_prob_test.png)

_**Figure 2.** Lagged prices, load, and time-of-day features are among the most important predictors._

---





- XGBoost
    - Single-Step Single-Output + Autoregressive
- CNN-LSTM-DNN
    - Single-Step Single-Output
    - Single-Step Multi-Output
    - Multi-Step Multi-Output (single shot, seq2vec)
    - Multi-Step Multi-Output (seq2seq)

Repo: [Jackson00Han/Time-Series-Training](https://github.com/Jackson00Han/Time-Series-Training/blob/main/Multivariate_Time_Series_Forecasting_Hands_On.ipynb)

The results by using PytorchForecasting will be updated soon.