---
title: "欧洲电力市场预测"
excerpt: "使用多种机器学习模型进行日前电价预测；XGBoost 对比 LSTM。<br/><img src='/images/xgb_lstm_val_abs.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2025-11-17
permalink: /zh/portfolio/item-2/
lang: zh
ref: eu-energy
---

这是我近期一个项目的简要介绍：我训练了一个稳健的模型来预测**日前逐小时电力价格**。  
目标是基于历史价格、负荷、发电结构以及天气等信息，预测未来 24 小时的电价。

代码仓库：  
[Jackson00Han/energy_market_forecasting](https://github.com/Jackson00Han/energy_market_forecasting/tree/main/main)

---

### 数据

数据范围是 2015–2019 年。  
下图展示了日均价格的时间序列，即使在日尺度上，价格仍然存在明显的尖峰和水平漂移，这使得稳定预测变得困难。

![Price actual (daily average)](/images/price_actual_daily_average.png)

_**图 1.** 2015–2019 年的电价日均值，可以看到明显的尖峰与水平漂移。_

按「星期几 × 小时」汇总的热力图则展示出很强的**周周期**和**日内周期**特征。

![Price by weekday and hour](/images/price_weekday_hour.png)

_**图 2.** “星期几 × 小时”电价热力图，揭示了显著的周周期和日内季节性。_

---

### 模型与设置

我尝试了多种方法（包括基于 Darts 库的 LSTM），但表现最好的模型是带 **分位数回归（quantile regression）** 的 **XGBoost**：

- 输入特征：  
  - 时间特征：小时、星期几、月份等  
  - 滞后特征：电价与负荷的多种时滞（如 24h、48h、168h）  
  - 发电结构与天气相关特征  
  - 派生特征：滚动均值、标准差、差分、最小值、最大值等
- 输出：  
  - 电价点预测  
  - 同时给出预测区间（例如 5% 与 95% 分位数）

主对比基线非常简单：  

> **基线**：在时刻 _h_，明天的电价 = 昨天同一时刻的电价。

---

### 结果

在留出的测试集上，XGBoost 模型：

- 相比「昨天同一时刻」的朴素基线，**MAE 降低约 28%**  
- **RMSE 降低约 30%**  
- 所给出的 **90% 预测区间** 的覆盖率接近 90%

下面是验证集上若干天的预测 vs 实际价格示例：

![validation forecasts](/images/xgb_lstm_val.png)

_**图 3.** 模型能够较好地跟踪电价的日内形状与整体水平，但极端尖峰仍然较难精确预测。_

这是最终模型在测试集上的预测表现：

![test forecasts](/images/xgb_prob_test.png)

_**图 4.** 概率型 XGBoost 模型在测试集上的点预测与区间预测。_

---

**补充说明**

除了上面基于 Darts 的实验，在仓库的 `training_his` 目录中，我还保留了若干经典时间序列模型的早期实现：

[training_his](https://github.com/Jackson00Han/energy_market_forecasting/tree/main/training_his)

包括但不限于：

- XGBoost  
  - 单步单输出 + 自回归（autoregressive）  
- CNN-LSTM-DNN  
  - 单步单输出  
  - 单步多输出  
  - 多步多输出（单次输出，seq2vec）  
  - 多步多输出（seq2seq）
