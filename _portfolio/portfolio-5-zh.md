---
title: "联邦学习反洗钱（AML）流水线"
excerpt: "各银行在本地基于账户级 SAR 标签训练模型，仅共享模型更新，在不共享原始交易数据的前提下学习跨行的可疑账户检测器。<br/><img src='/images/fl.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2025-12-20
permalink: /zh/portfolio/item-5/
lang: zh
ref: decentralized-aml
---

本项目是一个精简版的 **联邦学习（FL）** 反洗钱系统，基于 **AMLSim** 生成的多银行零售交易数据。在该设置下，各银行在本地使用**账户级 SAR 标签**训练模型，只上传模型更新，不共享原始交易数据。通过FL方法，结果显示模型表现全面优于各银行单独训练的基线模型，同时保护了数据隐私。

代码仓库：  
[Jackson00Han/decentralized_aml_demonstrator](https://github.com/Jackson00Han/decentralized_aml_demonstrator)

![联邦学习 client–server 工作流](/images/fl_flow.png)

## 目标

演示一个可运行的**跨行可疑账户检测**方案，同时做到：

- 各银行原始数据不出域
- 跨行特征空间可对齐、可训练
- 在极度类别不均衡场景下公平评估（避免 test 泄露）

## 方法

- **数据**：用 AMLSim 在 small/medium/large 三种规模下模拟多银行数据，并切分为每家银行各自的 train/val/test。
- **特征**：以账户为单位，按固定时间窗聚合交易行为特征，并将处理后的数据持久化以保证可复现。
- **联邦训练**：采用 client–server 多轮训练 + **FedAvg** 聚合；服务端构建**全局类别词表**用于一致的 one-hot 编码（客户端未见类别映射到 "unknown"）；评估阶段使用演示级的 masked 统计聚合增强隐私性。
- **模型**：SGD 版逻辑回归，使用**类别加权的 log loss** + **early stopping**；并在相同数据划分与评估协议下，对比调参后的本地训练基线。
- **模型选择**：仅用聚合后的验证集指标选最优全局模型，最终在留出的测试集上报告表现。

## 结果（概述）

![联邦学习 vs 本地基线的结果对比](/images/fl.png)

在我的实验中，联邦学习相较本地训练在不同银行/规模上整体更优：

- Precision/Recall/F1 与排序指标（Average Precision、ROC-AUC）更好
- 加权 log loss 更低（概率估计更稳定）
- 单轮联邦训练后即可观察到相对提升

