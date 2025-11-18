---
title: "b-jet Classification"
excerpt: "Classification: Select b-jets (b-quark) from the bdecays of the Z0 boson decaying to a quark and an anti-quark <br/><img src='/images/bquark.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2023-05-25
permalink: /portfolio/item-3/
lang: en
ref: bjet
---

This project tackles a classic problem from high-energy physics:  
**classifying b-jets (originating from b-quarks) among jets produced in Z⁰ → q\bar{q} decays.**  
In machine-learning terms, it is a **binary classification** task.

I explored three families of models:

- TensorFlow DNN
- PyTorch DNN
- XGBoost with hyperparameter tuning

and compared them using the AUC on a held-out test set.


## Dataset

The dataset comes from the *Applied Machine Learning* course at the Niels Bohr Institute.  
Each jet is described by a small set of high-level physics features:

- `prob_b` – probability of being a b-jet from track pointing to the secondary vertex  
- `spheri` – event sphericity, describing how spherical the event is  
- `pt2rel` – squared transverse momentum of tracks relative to the jet axis (jet “width”)  
- `multip` – jet multiplicity in a relative measure  
- `bqvjet` – probability of a detached (secondary) vertex consistent with a b-quark  
- `ptlrel` – transverse momentum (GeV) of a possible lepton w.r.t. jet axis (≈0 if no lepton)  
- `energy` – measured jet energy in GeV (nominally ≈45 GeV, but fluctuates)  
- target `isb` – 1 if the jet is from a b-quark, 0 otherwise  

Exploratory analysis (pairplots and a correlation heatmap) shows:

- `prob_b` cleanly separates b-jets from non-b jets  
- `bqvjet` is highly correlated with `prob_b` and contains largely redundant information  
- `pt2rel` is a strong discriminator and later appears as the most important feature in XGBoost  
- `ptlrel` is only weakly correlated with other variables and can add complementary signal


## Models and results

### TensorFlow DNN

Using a feed-forward neural network in TensorFlow, I:

- scaled inputs with `MinMaxScaler`
- used a **1-cycle learning-rate schedule** to efficiently search a good learning rate
- trained with binary cross-entropy and tracked AUC on a validation split

The best TensorFlow model reaches an **AUC ≈ 0.934** on the test set.

### PyTorch DNN

I then re-implemented a similar architecture in PyTorch:

- three hidden layers (64–64–32 units) with ReLU activations  
- SGD optimizer with momentum  
- custom training and validation loops

The PyTorch model achieves **AUC ≈ 0.933**, essentially matching the TensorFlow result.

### XGBoost

Finally, I trained an **XGBoost** classifier:

- used `RandomizedSearchCV` over depth, learning rate, regularization and number of trees  
- performed cross-validation with early stopping to pick the optimal number of boosting rounds  
- retrained the best model on the full training set

The final XGBoost model reaches **AUC ≈ 0.936–0.937** on the test set—comparable to the neural networks—but with a major advantage: **interpretability**.

The feature-importance plot highlights `pt2rel` as the most influential variable, suggesting that the transverse momentum distribution relative to the jet axis captures key differences between b-quark and non-b jets.


## Summary

- Three different approaches (TensorFlow DNN, PyTorch DNN, XGBoost) all achieve **AUC ≈ 0.93+** on a compact, physics-motivated feature set.  
- **XGBoost** is my preferred model here: it keeps performance high while providing clear feature importances that connect back to physical intuition.  
- Next steps include extending the analysis to **regression of jet energy** and experimenting with dimensionality reduction (e.g. PCA) under stricter resource constraints.

[Repo](https://github.com/Jackson00Han/Data-Science-Project-Diary/tree/main/physics)
