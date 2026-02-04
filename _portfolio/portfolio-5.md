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

Decentralized AML Demonstrator is a compact **federated learning (FL)** pipeline for **bank anti-money laundering (AML)** on **AMLSim-generated multi-bank retail transaction data**. Each bank trains locally on labeled **account-level SAR** data and shares only model updates—no raw transactions. Through FL, the results show consistent improvements over local-only baselines while preserving data privacy.

Repo: [Jackson00Han/decentralized_aml_demonstrator](https://github.com/Jackson00Han/decentralized_aml_demonstrator)

![Federated learning client–server workflow](/images/fl_flow.png)

## Objective

Demonstrate **cross-bank suspicious-account detection** while:

- keeping each bank's raw data private,
- aligning heterogeneous features across banks, and
- evaluating fairly under extreme class imbalance (no test leakage).

## Approach

- **Data**: AMLSim multi-bank simulation at small/medium/large scales; split into per-bank datasets with aligned train/val/test splits.
- **Features**: account-level windows aggregating transactional behavior; persisted processed datasets for reproducibility.
- **Federation**: client–server rounds with **FedAvg**; server builds a **global categorical vocabulary** for consistent one-hot encoding (clients map unseen values to "unknown"); masked aggregation for demo-level privacy during evaluation.
- **Model**: SGD logistic regression with **class-balanced weighted log loss** and **early stopping**; compared against a tuned local-only baseline under identical splits.
- **Selection**: choose the global model using only aggregated validation metrics, then report final test performance.

## Results (summary)

![Federated learning results vs baseline](/images/fl.png)

In my experiments, FL consistently beat local-only training across banks/scales:

- higher **Precision/Recall/F1** and better ranking (**Average Precision**, ROC-AUC),
- lower **weighted log loss** (better probability estimates),
- improvements visible even after a **single federated round**.
