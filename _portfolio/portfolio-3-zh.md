---
title: "COVID-19 入院紧急程度预测"
excerpt: "基于 EDA 提取特征，使用 KNN 和逻辑回归等经典机器学习模型，预测新冠患者从症状出现到住院的紧急程度。<br/><img src='/images/covid.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2023-10-01
permalink: /zh/portfolio/item-4/
lang: zh
ref: covid-urgency
---

这个项目是我在 *Introduction to Data Science with Python*（Harvard/edX）课程中的 **结课项目（capstone project）**。  
目标是基于患者在**出现新冠症状时**即可获得的信息，预测 **其需要住院治疗的紧急程度**。

[代码仓库 Repo](https://github.com/Jackson00Han/Data-Science-Project-Diary/blob/main/projects/Data_Science_edx/8.%20capstone%20project/4.%20roc/roc.ipynb)

为了更好地理解数据，我首先做了 **探索性数据分析（EDA）**，其中有几个现象比较突出：

- **40–50 岁** 年龄段对医院床位的需求最高  
- 在紧急入院的病例中，**发烧** 是最常见的症状  

随后，我以 ROC 曲线作为主要评估工具，构建并比较了两类经典模型：

- **k 近邻（k-Nearest Neighbors, KNN）**
- **逻辑回归（Logistic Regression）**

对于每个模型，我都结合不同的现实场景（例如：医院床位紧张 vs. 尽量不漏掉真正的紧急病例），  
讨论了如何选择合适的 **决策阈值（decision threshold）**，在召回率和误报率之间做权衡。

![](/images/covid.png)
