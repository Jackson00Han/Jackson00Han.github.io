---
title: "Jane Street 金融时间序列预测"
excerpt: "使用 LightGBM（CV WR2=0.0143）、Polars ETL（~20× 快于 pandas）和快速 memmap 推理进行金融市场预测。<br/><img src='/images/js.jpg' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: true
date: 2025-11-01
permalink: /zh/portfolio/item-1/
lang: zh
ref: js
---

这个项目面向 Kaggle 的 [Jane Street 实时金融时间序列预测竞赛](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting)，需要处理 **重尾分布、非平稳性以及突发的结构性变动** 等典型金融时间序列难点。

代码仓库：  
[Jackson00Han/Jane-Street-Time-Series-Forecasting](https://github.com/Jackson00Han/Jane-Street-Time-Series-Forecasting/tree/main)


为了在**训练时间、模型复杂度和精度**之间取得平衡，我首先采用了 LightGBM。  
离线交叉验证的结果是加权零均值决定系数 **WR2 ≈ 0.0143**，还有较大提升空间，但已经能和该任务公开排行榜上的顶尖结果相当。  
在线学习排行榜链接：  
[Online leaderboard](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting/leaderboard)

**亮点概览**

- 交叉验证 **WR2 ≈ 0.0143**，与公开排行榜 Top-10 水平接近  
- 使用 **Polars** 做特征工程和 ETL，在我的环境下预处理约比 pandas 快 **~20×**  
- 稳健的数据清洗策略：  
  - 对异常值使用 **3σ 裁剪（clipping）**  
  - 对缺失值使用 **时间感知的前向填充（time-aware forward-fill）**
- **配置优先（config-first）** 的可复现性设计：  
  - 通过一个 `config.yaml` 统一控制数据区间、特征开关、交叉验证方案以及模型超参数
- 特征工程包括：  
  - **日度季节性信号**（如工作日 / 周末、交易时段等）  
  - **跨天同一时间的时滞特征（same-time cross-day lags）**  
  - **短时间窗口的 tick 历史特征**，用于捕捉高频动态
- 使用 **memory-mapped（内存映射）数组** 加速数据重载，并降低训练时的峰值内存占用


**模型选择的经验**

我也尝试过 Temporal Fusion Transformer（TFT）。  
即便在做了采样、减小模型规模之后：

- 训练仍然比较耗时  
- 当 encoder 窗口变长时，推理开销也显著增大  

对于这类 **高频、大规模金融时间序列**，我的经验是：

- **第一轮优先尝试树模型（如 LightGBM / XGBoost）**，用来快速探索特征和上线效果  
- 只有在明确看到深度模型在**精度和效率**上都有明显收益时，才值得进一步投入到复杂的序列建模架构上
