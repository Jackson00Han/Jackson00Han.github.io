---
title: "Jane-Street-Time-Series-Forecasting"
excerpt: "Short description of portfolio item number 1<br/><img src='/images/js.png'>"
collection: portfolio
featured: true
date: 2025-11-01
permalink: /portfolio/item-1/
---

This is a Kaggle competition project, host by Jane Street. To get a successful daily trading model in modern financial markets, many challenges have to be conqured proprightly, including fat-tailed distributions, non-stationary time series, and sudden shifts in market behavior.

To ballence the training time, complexity and accuracy, I trained a LightGBM model. The offline CV weighted zero mean R squared score is round 0.014, with a big room to increase. This can be ranked Top 10 arund the world. Work link: [https://github.com/Jackson00Han/Jane-Street-Time-Series-Forecasting](https://github.com/Jackson00Han/Jane-Street-Time-Series-Forecasting)

Highlights:

Strong offline CV: weighted zero-mean R-squared score (WR2) ≈ 0.01435

Fast pipeline with Polars: 20x faster than pandas for data preprocessing

Robust outlier & missing-value handling: 3σ clipping + TTL/forward-fill

Config-first reproducibility: a single config.yaml controls data ranges, FE, CV, and model hyperparameters.

Multi-dimensional feature engineering: daily, same-time cross-day, and tick-history features.

Memory-mapped matrices (memmap): fast reloads and lower memory during training.


