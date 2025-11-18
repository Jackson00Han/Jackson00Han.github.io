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

这个项目是我在哈佛大学开设的课程 **“Introduction to Data Science with Python”** 的结课项目。  
目标是：根据患者**出现新冠症状的时间点及相关信息**，预测其需要被送入医院治疗的紧急程度。

代码仓库：  
[Jackson00Han/Data-Science-Project-Diary](https://github.com/Jackson00Han/Data-Science-Project-Diary/blob/main/projects/Data_Science_with_Python/8.%20capstone%20project/4.%20roc/roc.ipynb)

---

为了更好理解这份数据，我首先做了较为系统的 **探索性数据分析（EDA）**。  
分析结果发现：

- 年龄段 **“40–50 岁”** 对医院床位的需求最高；
- 在紧急入院的病例中，**发烧** 是最常见的症状。

在此基础上，我构建并评估了两个经典模型，用于预测“是否紧急入院”：

- **K 近邻（KNN）**
- **逻辑回归（Logistic Regression）**

评估方面使用了 **ROC 曲线** 和相关指标来比较不同模型与阈值的表现，并结合现实场景讨论不同取舍：

- 若希望**尽量不漏掉真正紧急的患者**，会倾向于牺牲部分精度、提高召回率；
- 若资源有限，需要控制误报率，则会选择在准确率与召回率之间做更谨慎的平衡。

整个项目的重点在于：

- 用 EDA 找出与入院紧急程度高度相关的特征；
- 在可解释性较强的经典模型上，结合 ROC/阈值分析，讨论在**真实医疗资源约束**下如何做决策。
