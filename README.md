# 基于高级特征工程与可解释性分析的混凝土抗压强度预测

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![CatBoost](https://img.shields.io/badge/Model-CatBoost%20%7C%20XGBoost-orange.svg)]()
[![SHAP](https://img.shields.io/badge/Interpretability-SHAP-success.svg)]()

## 📌 Project Overview / 项目背景
混凝土抗压强度预测是结构工程质量控制的核心环节。当前机器学习方法虽成为主流，但普遍存在**特征同质化（缺乏材料学物理机理）**及**可解释性差**的痛点。

本项目为 Kaggle 机器学习与土木工程的交叉应用。引入**土木工程材料学规律**构建高级特征工程，并结合 **Stacking 模型**与 **SHAP 框架**，实现了高精度解释性的混凝土抗压强度预测。

## 🔬 Core Methodology / 核心研究内容

### 1. Physics-Informed Feature Engineering (基于土木工程材料水化反应的特征工程)
打破以往局限，基于水化反应机理构造了能够刻画材料协同效应的特征工程：
* **Water-to-Binder Ratio (W/B，水胶比)**：替代传统水灰比，综合考虑水泥、粉煤灰、矿渣的共同作用。
* **Sand Ratio (砂率)**：细骨料占总骨料的体积/质量比，决定混凝土的骨架密实度。
* **Log-scaled Curing Age (对数化龄期)**：高度契合水化深度随时间非线性增长的土木材料学规律。

### 2. Modeling & Ensembling (模型训练与融合)
* 引入基于目标值先验引导的联合插值过采样算法，有效缓解欠拟合现象。
* 利用 **贝叶斯优化 (Bayesian Optimization)** ，并在 5 折交叉验证策略训练并验证。
* 结合基于 OOF RMSE 倒数次幂的**加权融合**，与 **Stacking 模型**两种融合模型策略。

### 3. Interpretability (SHAP 可解释性分析)
引入 SHAP 框架，找出 CatBoost/XGBoost 等最优单模，从定量分析各材料组分对强度的相对贡献大小与方向。

## 📊 Key Results / 核心结论

在交叉验证评估中，加权融合与 Stacking 策略将外部测试集均方根误差 (RMSE) 进一步显著降低至3.51 MPa，拟合优度 $R^2$ **（0.96）**表现优异。模型不仅预测精准，更成功验证了土木工程水化反应规律。

### 1. 全局材料贡献度 (Global Feature Importance)
SHAP 摘要图表明：**水胶比、养护龄期、水泥含量**对混凝土强度具有主导作用。
*(请在此处替换为你的真实图片路径)*
![SHAP Summary Plot](figs/shap_sci_summary.png)

### 2. 核心物理规律的非线性验证 (Non-linear Dependence)
依赖图科学地量化了“水分导致内部孔隙率增加，进而降低强度”的土木材料学逻辑。
![SHAP Dependence Plot](figs/shap_sci_dependence_Water_Binder_Ratio.png)

### 3. 配合比微观推演 (Mix Design Interpretation)
通过单样本瀑布图，能够清晰解释特定工程配合比的强度生成路径，直接指导实际工程中的配比优化。
![SHAP Waterfall Plot](figs/shap_sci_waterfall.png)

## 🚀 How to Run / 快速复现

1. Clone this repository:
   ```bash
   git clone [https://github.com/YourUsername/Concrete-Strength-Prediction.git](https://github.com/YourUsername/Concrete-Strength-Prediction.git)
