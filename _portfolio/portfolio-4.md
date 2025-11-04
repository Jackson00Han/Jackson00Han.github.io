---
title: "B-Quark Jet Classification"
excerpt: "Classification: Select b-jets (b-quark) from the bdecays of the Z0 boson decaying to a quark and an anti-quark <br/><img src='/images/bquark.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2023-05-25
permalink: /portfolio/item-3/
---

This project aims to select b-jets (b-quark) from the decays of the Z0 boson decaying to a quark and an anti-quark. Simply speaking, it is a binary classification problem. I'll develop XGBoost, NN-based TensorFlow and PyTorch machine learning methods to address this problem.  

## Dataset

The dataset and topic is originally from my Applied Machine Learning course at Niels Bohr Institute. It was an amazing course, I have put the link of this course in the resources page. The data (that we will use here) includes:
- prob_b: Probability of being a b-jet from the pointing of the tracks to the vertex
- spheri: Sphericity of the event, i.e. how spherical it is.
- pt2rel: The transverse momentum squared of the tracks relative to the jet axis, i.e. width of the jet.
- multip: Multiplicity of the jet (in a relative measure).
- bqvjet: b-quark vertex of the jet, i.e. the probability of a detached vertex.
- ptlrel: Transverse momentum (in GeV) of possible lepton with respect to jet axis (about 0 if no leptons).
- energy: Measured energy of the jet in GeV. Should be 45 GeV, but fluctuates. (we'll use it later when dealing with regression problem)
- (target variable) isb: 1 if it is from a b-quark and 0, if it is not

[Temperary link](https://jackson-han-data-insights.webflow.io/work/project-3)