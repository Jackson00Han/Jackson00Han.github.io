---
title: "b-jet 分类"
excerpt: "从 Z⁰ → q\\bar{q} 过程中产生的喷注中识别 b-jet（来自 b 夸克），本质上是一个二分类问题，并使用 TensorFlow、PyTorch 与 XGBoost 进行建模。<br/><img src='/images/bquark.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2023-05-25
permalink: /zh/portfolio/item-3/
lang: zh
ref: bjet
---

这个项目面向高能物理中的一个经典任务：  
在 **Z⁰ → q\\bar{q} 衰变产生的喷注中，识别其中属于 b 夸克的 b-jet**。  
从机器学习的角度看，这是一个标准的 **二分类问题**。

我主要比较了三类模型：

- 基于 TensorFlow 的前馈神经网络（DNN）
- 基于 PyTorch 的 DNN
- 带超参数搜索的 XGBoost

并使用留出测试集上的 **AUC** 来对比它们的表现。

---

## 数据集 Dataset

数据来自尼尔斯·玻尔研究所的 *Applied Machine Learning* 课程。  
每个喷注由一组高层物理特征描述：

- `prob_b` – 由径迹指向次级顶点的信息得到的「是 b-jet 的概率估计」  
- `spheri` – 事例的球形度（sphericity），刻画事件在三维动量空间中有多“球形”  
- `pt2rel` – 喷注内径迹相对喷注轴的**横向动量平方**（反映喷注“宽度”）  
- `multip` – 喷注的多重性（multiplicity），以相对尺度衡量径迹数量  
- `bqvjet` – 存在与 b 夸克一致的脱离主顶点的次级顶点的概率  
- `ptlrel` – 相对于喷注轴的轻子横向动量（GeV），若无轻子则该值接近 0  
- `energy` – 喷注的测量能量（GeV），理论上约为 45 GeV，但会有涨落  
- 目标变量 `isb` – 若喷注来自 b 夸克则为 1，否则为 0  

通过 pairplot 和相关性热力图的探索性分析可以看到：

- `prob_b` 对区分 b-jet 和非 b-jet 的效果非常好  
- `bqvjet` 与 `prob_b` 高度相关，信息有较大冗余  
- `pt2rel` 是一个很强的判别特征，并在 XGBoost 中表现为最重要的特征  
- `ptlrel` 与其他变量相关性较弱，可以提供一定的互补信息  

---

## 模型与结果 Models and results

### TensorFlow DNN

在 TensorFlow 中，我使用了前馈神经网络并：

- 通过 `MinMaxScaler` 对输入特征做缩放  
- 使用 **1-cycle 学习率调度策略** 高效搜索合适的学习率  
- 采用二元交叉熵损失，在验证集上监控 AUC 指标  

在测试集上，最好的 TensorFlow 模型达到了 **AUC ≈ 0.934**。

### PyTorch DNN

随后，我在 PyTorch 中实现了一个类似的网络结构：

- 三个隐藏层（64–64–32）+ ReLU 激活  
- 使用带动量的 SGD 优化器  
- 自定义训练与验证循环  

PyTorch 模型在测试集上取得的 **AUC ≈ 0.933**，与 TensorFlow 模型基本持平。

### XGBoost

最后，我训练了一个 **XGBoost** 分类器：

- 使用 `RandomizedSearchCV` 对树深度、学习率、正则化强度和树数量等进行超参数搜索  
- 借助早停（early stopping）在交叉验证中选择最佳迭代轮数  
- 在完整训练集上重训最优模型  

最终的 XGBoost 模型在测试集上的 **AUC ≈ 0.936–0.937**，性能与神经网络相当，  
但有一个明显优势：**可解释性**。

特征重要性图显示 `pt2rel` 是最关键的特征，这也印证了物理直觉：  
喷注内横向动量相对喷注轴的分布，确实很好地区分了来自 b 夸克和非 b 夸克的喷注。

---

## 总结 Summary

- 在一组紧凑但物理含义明确的特征上，  
  三种方法（TensorFlow DNN、PyTorch DNN、XGBoost）都达到了 **AUC ≈ 0.93+**。  
- 在这个任务上，**XGBoost 是我更偏好的模型**：  
  在保持高性能的同时，特征重要性能够直接连回物理图像，为分析提供了更清晰的解释框架。

[Repo](https://github.com/Jackson00Han/Data-Science-Project-Diary/tree/main/physics)
