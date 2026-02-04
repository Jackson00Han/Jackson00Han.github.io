---
title: "Federated Learning Pipeline for Anti-money Laundering"
excerpt: "Each bank trains locally on labeled account-level SAR data and shares model updates to learn a global detector of suspicious accounts without sharing raw data.<br/><img src='/images/fl.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2025-12-20
permalink: /portfolio/item-5/
lang: en
ref: decentralized-aml
---

Decentralized AML Demonstrator is a **federated learning (FL)** pipeline for **bank anti-money laundering (AML)** on **AMLSim-generated multi-bank retail transaction data**. Each bank trains locally on labeled **account-level SAR** data and shares only model updates, enabling a cross-bank detector of suspicious accounts **without sharing raw transactions**.

Repo: [Jackson00Han/decentralized_aml_demonstrator](https://github.com/Jackson00Han/decentralized_aml_demonstrator)

![Federated learning client–server workflow](/images/fl_flow.png)

## Objective

Build a practical demonstrator of **cross-bank AML detection** where:

- each institution keeps its raw data private,
- the system still learns from **combined signal across banks**, and
- evaluation and model selection avoid **test leakage** under severe class imbalance.

## Approach

### Data simulation and splits

- Simulated multi-bank datasets at three institutional scales (**small / medium / large**) using **AMLSim**.
- Partitioned the generated data into **per-bank** datasets (accounts, transactions, SAR labels).
- Built an **account-level** preprocessing + feature engineering pipeline:
  - aggregate transactional behavior into fixed time windows,
  - create aligned train/validation/test splits,
  - persist processed datasets for reproducibility.

### Federated workflow (client–server)

Implemented a decentralized FL workflow with a client–server architecture:

- client-side statistics reporting and dataset alignment,
- server-side global plan construction,
- per-round local training and **FedAvg** parameter aggregation,
- demonstration-level **secure masking** during federated evaluation (server aggregates masked statistics only; not production-grade cryptographic secure aggregation).

To handle heterogeneous categorical spaces across banks, the server constructs a **global categorical vocabulary** to align feature spaces for consistent one-hot encoding, while clients can map unseen values to an **unknown** bucket.

### Model and training

The model layer is adapter-based and currently defaults to **logistic regression trained with SGD**:

- optimized with **class-balanced weighted log loss** (for extreme label imbalance),
- used **early stopping** as the selection criterion for both federated training and local baselines,
- implemented a local (non-federated) baseline with hyperparameter search under identical splits and evaluation protocols.

Model selection is done using only **aggregated validation metrics**, followed by final evaluation on held-out test data.

## Results (summary)

Across the three banks and simulated scales, the federated model consistently improved both:

- **ranking quality** and classification performance (Precision / Recall / F1, **Average Precision**, ROC-AUC), and
- **probability calibration** (lower **weighted log loss**),

compared with local-only baselines. Notably, the FL setup outperformed local models even after a **single federated round** in my experiments.

## Engineering notes

- Modularized client/server operations into independent scripts for reproducibility.
- Added a **one-round smoke test** pipeline to support fast validation and debugging.
