---
title: "Portfolio item number 1"
excerpt: "Short description of portfolio item number 1<br/><img src='/images/js.jpg'>"
collection: portfolio
featured: true
date: 2025-01-15
permalink: /portfolio/item-1/
---

This project tackles a Jane Street–style market time-series task on Kaggle. Building a daily trading model in live-like conditions means dealing with fat tails, non-stationarity, and sudden shifts.

To balance training time, complexity, and accuracy, I started with LightGBM. My offline cross-validation achieves a weighted zero-mean R² (WR2) ≈ 0.0143, which is competitive with the top public results on this task.

Repo: [Jackson00Han/Jane-Street-Time-Series-Forecasting](https://github.com/Jackson00Han/Jane-Street-Time-Series-Forecasting/tree/main)

**Highlights**
- WR2 ≈ 0.0143 (CV): stable across folds with conservative leakage checks.

- Fast preprocessing with Polars: ~20× faster than pandas on my setup.

- Robust data cleaning: 3σ clipping for outliers; forward-fill with time-aware limits for missing values.

- Config-first reproducibility: a single config.yaml controls data ranges, feature flags, CV, and model hyperparameters.

- Feature engineering: daily seasonality signals, same-time cross-day lags, and short-horizon tick-history features.

- Memory-mapped arrays: quicker reloads and lower peak RAM during training.

**Notes on deep models**
I also tried Temporal Fusion Transformer. Even with subsampling and a lighter configuration, training was slow, and inference became heavy with longer encoder windows. For large, high-frequency datasets, I’d use tree-based models as the first pass and only move to deep models when they clearly win on both accuracy and runtime.