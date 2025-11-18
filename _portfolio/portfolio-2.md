---
title: "European Energy Market Forecasting"
excerpt: "Day-ahead electricity price forecasting using multiple ML models; XGBoost vs. LSTM. <br/><img src='/images/xgb_lstm_val_abs.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2025-11-17
permalink: /portfolio/item-2/
lang: en
ref: eu-energy
---

This is a brief intro to my recent project where I trained a robust model to forecast **day-ahead hourly electricity prices**.  
The goal is to predict the next 24 hours of prices using historical prices, load, generation mix, and weather.

Repo: [Jackson00Han/energy_market_forecasting](https://github.com/Jackson00Han/energy_market_forecasting/tree/main/main).

### Data

The data ranges from 2015 to 2019. The plot below shows that, even at a daily scale, the price series has sharp spikes and shifting levels, which makes it difficult to forecast reliably.

![Price actual (daily average)](/images/price_actual_daily_average.png)

_**Figure 1.** Daily average electricity price from 2015 to 2019, showing sharp spikes and shifting levels._

The price-by-weekday-and-hour plot demonstrates a strong weekly and intraday seasonality.

![Price by weekday and hour](/images/price_weekday_hour.png)

_**Figure 2.** Weekday–hour price heatmap revealing pronounced weekly and intraday seasonality._


### Model and setup

I tried a few approaches (including an LSTM) using the Darts library, but the best performing model was **XGBoost with quantile regression**:

- Input features:  
  - time features (hour, day of week, month),  
  - lagged prices and load (e.g. 24h, 48h, 168h),  
  - generation mix and weather variables,  
  - derived features (rolling mean, standard deviation, differences, min, max, etc.).
- Output:  
  - price point forecast,  
  - plus prediction intervals (e.g. 5% and 95% quantiles).

The main baseline I compare against is very simple:  
**Baseline**: at hour _h_, tomorrow’s price is set equal to yesterday’s price at the same hour.

---

### Results

On a held-out test period, the XGBoost model:

- reduces **MAE by ~28%** vs the naïve “yesterday” baseline,  
- reduces **RMSE by ~30%**,  
- produces **90% prediction intervals** with coverage close to 90%.

Below is an example of the forecast vs actual prices for a few days on the validation set:

![validation forecasts](/images/xgb_lstm_val.png)

_**Figure 3.** The model tracks the daily pattern and general level of prices quite well, but very sharp spikes are still hard to predict._

Here is the forecast from the final model on the test set:

![test forecasts](/images/xgb_prob_test.png)

_**Figure 4.** The probabilistic XGBoost model provides both point forecasts and prediction intervals on the test set._

---

PS: In addition to the Darts-based experiments above, you can also find my earlier implementations of several classic time-series models in the `training_his` folder of this repository:
[training_his](https://github.com/Jackson00Han/energy_market_forecasting/tree/main/training_his). These include:

- XGBoost  
  - Single-Step Single-Output + Autoregressive  
- CNN-LSTM-DNN  
  - Single-Step Single-Output  
  - Single-Step Multi-Output  
  - Multi-Step Multi-Output (single shot, seq2vec)  
  - Multi-Step Multi-Output (seq2seq)


