---
title: "Federated Learning Pipeline for Anti-money Laundering"
excerpt: "Each bank trains locally on labeled account-level SAR data and shares model updates to learn a global detector of suspicious accounts without sharing raw data.  <br/><img src='/images/fl.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2025-12-20
permalink: /portfolio/item-5/
lang: en
ref: bjet
---

Decentralized AML Demonstrator is a federated learning pipeline for bank anti-money laundering on AMLSim-generated multi-bank data. Each bank trains locally on labeled account-level SAR data and shares model updates to learn a global detector of suspicious accounts without sharing raw data. The model layer is adapter-based and currently defaults to logistic regression (SGD), with room to extend to other ML/DL/GNN models.