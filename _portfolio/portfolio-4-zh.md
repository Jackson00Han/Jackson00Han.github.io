---
title: "b-jet 分类"
excerpt: "从 Z⁰ 玻色子衰变产生的喷注中筛选 b-jet（b 夸克），本质上是一个二分类问题，并使用 XGBoost 与深度学习方法建模。<br/><img src='/images/bquark.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2023-05-25
permalink: /zh/portfolio/item-3/
lang: zh
ref: bjet
---

这个项目的目标是：在 **Z⁰ 玻色子衰变为夸克–反夸克对** 产生的喷注中，识别出其中的 **b-jet（来自 b 夸克的喷注）**。  
简单来说，这是一个标准的 **二分类问题**。

我使用的主要机器学习方法包括：

- **XGBoost**
- 基于 **TensorFlow** 的前馈神经网络
- 基于 **PyTorch** 的神经网络模型

通过比较不同模型在 ROC 曲线、AUC 等指标上的表现，讨论在高能物理场景下如何平衡模型复杂度与可解释性。

---

## 数据集

这个数据集来自我在尼尔斯·玻尔研究所上的 **Applied Machine Learning** 课程（非常棒的一门课，已在「资源」页面中给出链接）。  
本项目使用的数据特征包括：

- **prob_b：**  
  由轨迹指向顶点（vertex）的信息得到的「是 b-jet 的概率估计」。

- **spheri：**  
  事例的 **球形度（sphericity）**，刻画事件在三维动量空间中有多接近“球形”。

- **pt2rel：**  
  喷注内各条径迹相对于喷注轴的**横向动量平方**，可以理解为喷注的“宽度”。

- **multip：**  
  喷注的**多重性（multiplicity）**，在相对意义上衡量喷注中径迹数量的多少。

- **bqvjet：**  
  喷注的 **b 夸克顶点（vertex）信息**，即是否存在脱离主顶点的次级顶点的概率。

- **ptlrel：**  
  相对于喷注轴的**轻子横向动量（GeV）**。如果该喷注中没有轻子，这个量会接近 0。

- **energy：**  
  喷注的实测能量（单位 GeV）。理论上应接近 45 GeV，但会有涨落。  
  （在我进一步做回归问题时，这个特征也会被使用。）

- **isb（目标变量）：**  
  若该喷注来自 b 夸克，则 `isb = 1`；否则 `isb = 0`。

---

更多可视化与训练日志目前暂时放在一个临时页面中：  
[Temporary link](https://jackson-han-data-insights.webflow.io/work/project-3)
