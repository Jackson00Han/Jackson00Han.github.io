---
title: "Jane Street Financial Time Series Forecasting"
excerpt: "Financial market forecasting with LightGBM (wr2=0.0143 CV), Polars ETL (~20× faster than pandas), and fast memmap inference.<br/><img src='/images/js.jpg' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: true
date: 2025-11-01
permalink: /portfolio/item-1/
---

This project tackles Kaggle's [Jane Street real-time time series market data forecasting challenge](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting), addressing heavy tails, non-stationarity, and abrupt regime shifts.

Repo: [Jackson00Han/Jane-Street-Time-Series-Forecasting](https://github.com/Jackson00Han/Jane-Street-Time-Series-Forecasting/tree/main)

To balance training time, complexity, and accuracy, I started with LightGBM. My offline cross-validation achieves a weighted zero-mean R² (WR2) ≈ 0.0143 with a bigroom to improve, which is competitive with the top public results on this task. Online learning leaderboard: [link](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting/leaderboard)

**Highlights**
- CV **WR2 ≈ 0.0143**, comparable to the public leaderboard’s Top-10.
- **Polars** preprocessing ~**20×** faster than pandas on my setup.
- Robust cleaning: **3σ clipping** for outliers; **time-aware forward-fill** for missing values.
- **Config-first** reproducibility: a single `config.yaml` controls data ranges, feature flags, CV, and model hyperparameters.
- Feature engineering: **daily seasonality** signals, **same-time cross-day lags**, and **short-horizon tick-history** features.
- **Memory-mapped** arrays for quicker reloads and lower peak RAM during training.


Note: I also tried Temporal Fusion Transformer. Even with subsampling and a lighter configuration, training was slow, and inference became heavy with longer encoder windows. For large, high-frequency datasets, I’d use tree-based models as the first pass and only move to deep models when they clearly win on both accuracy and runtime.

