---
title: "Jane-Street-Time-Series-Forecasting"
excerpt: "Short description of portfolio item number 1"
collection: portfolio
featured: true
date: 2025-11-01
permalink: /portfolio/item-1/
teaser: /images/js.png  
image:  /images/js.png
---

This project tackles a Jane Street–style market time-series task on Kaggle. Building a daily trading model in live-like conditions means dealing with fat tails, non-stationarity, and abrupt regime shifts.

To balance training time, complexity, and accuracy, I trained a LightGBM model. Offline cross-validation achieves WR2 ≈ 0.0143—a strong, competitive result with clear headroom to improve.

Highlights:

Strong offline CV: weighted zero-mean R-squared score (WR2) ≈ 0.01435

Fast pipeline with Polars: 20x faster than pandas for data preprocessing

Robust outlier & missing-value handling: 3σ clipping + TTL/forward-fill

Config-first reproducibility: a single config.yaml controls data ranges, FE, CV, and model hyperparameters.

Multi-dimensional feature engineering: daily, same-time cross-day, and tick-history features.

Memory-mapped matrices (memmap): fast reloads and lower memory during training.


Notes on deep models

I also tried Temporal Fusion Transformer. Even with subsampling and a lighter configuration, training was slow, and inference became heavy with longer encoder windows. For large, high-frequency datasets, I’d use tree-based models as the first pass and only move to deep models when they clearly win on both accuracy and runtime.

