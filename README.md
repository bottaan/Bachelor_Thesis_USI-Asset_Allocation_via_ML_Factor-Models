# Bachelor_Thesis_USI-Asset_Allocation_via_ML_Factor-Models
Empirical implementation of a Bachelor's thesis at USI: forecasting multi-asset returns and optimizing portfolios using Econometric Factor Models and Machine Learning (Elastic Net, Neural Network).


# Asset Allocation via Machine Learning and Factor Models

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-enabled-orange.svg)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Bachelor's degree in Economics, major in Finance** – **Università della Svizzera Italiana (USI)** 

**Thesis Title:** *Asset Allocation via Machine Learning and Factor Models: An Empirical Evaluation of Portfolio Optimization Approaches*

**Author:** Andrea Botta

**Supervisor:** Prof. Patrick Gagliardini

## Project Overview
This repository contains the empirical implementation of my Bachelor's thesis. The project investigates whether Machine Learning techniques can outperform traditional econometric factor models in forecasting asset returns and translating those forecasts into economically superior portfolio allocations within a Mean-Variance Optimization (MVO) framework.

The analysis evaluates a 50+ year timeframe (May 1973 – December 2024), rigorously testing models over a rolling/expanding Out-of-Sample (OOS) period across five major US asset classes: Equities (S&P 500), Government Bonds (7-10y Treasuries), Commodities, Gold, and REITs.

## Data Pipeline & Feature Engineering
* **Asset Data:** FactSet Total and Price Returns.
* **Macro Predictors:** The 37 macroeconomic variables from the Goyal-Welch (GWZ 2023) dataset.
* **Risk Factors:** Fama-French 3-Factor Model (Mkt-RF, SMB, HML)
* **Technical Features:** 20 custom engineered features (Momentum, Moving Averages, Volatility.
* **Dimensionality:** A total of 57 predictors + 3 lagged Fama-French factors. All data is strictly lagged ($t-1$) and aligned to month-end to prevent look-ahead bias. Forward-fill (LOCF) is applied where necessary.

## Forecasting Models
Four distinct predictive architectures are implemented and compared against the Historical Average and a theoretical "Oracle" (perfect foresight) model:

1. **Two-Step OLS Baseline:** A traditional structural factor model forecasting factor premia via the 37 GW macro predictors, and subsequently estimating asset returns. Estimated via a 120-month rolling window.
2. **Two-Step OLS-Lasso:** An $L_1$-penalized extension addressing the high-dimensional feature space (57 predictors). Optimal regularization ($\alpha$) is selected via rolling validation grid search.
3. **Elastic Net (ENet):** Direct return forecasting applying $L_1/L_2$ regularization. Features a dynamic grid search for penalty parameters, with the option to utilize outlier-robust Huber Loss.
4. **Deep Neural Network (NN-3):** A shallow architecture closely following *Gu, Kelly, and Xiu (2020)*. Features 3 hidden layers (16-8-4), BatchNorm, ReLU, Adam optimizer, early stopping (patience=5), and an ensemble of 10 random seed initializations to stabilize variance.

## Portfolio Optimization (MVO)
Return forecasts ($\mathbb{E}[y]$) are fed into a Mean-Variance Optimizer.
* **Covariance Matrix ($\Sigma$):** Estimated using the robust **Ledoit-Wolf shrinkage** over a 60-month rolling window to ensure invertibility and mitigate estimation error.
* **Setups Evaluated:**
  * **Unconstrained:** Long-only, fully invested.
  * **Realistic (Constrained):** Long-only, fully invested, maximum weight capped at 60% per asset, with an **Adaptive Hard Turnover Constraint** (capped at 20% in normal regimes, relaxed to 40% during high-volatility crisis periods).

## Evaluation & Diagnostics
The codebase computes a comprehensive suite of academic and financial metrics:
* **Statistical Power:** Out-of-Sample $R^2$, Predicted vs. Actual regressions (Slope, Pearson r), Directional Accuracy (Hit Rate).
* **Significance Tests:** Diebold-Mariano tests (Model vs. Historical Mean), Jensen's Alpha.
* **Predictor Importance:** Advanced feature extraction including *Gradient $\times$ Input* methods for Neural Networks to open the "black box" of ML forecasts.
* **Economic Value:** Annualized Returns, Volatility, Sharpe Ratio, Sortino Ratio, Max Drawdown, VaR/CVaR, and sub-period robustness checks during major market crashes (Dot-com, GFC, COVID-19, 2022 Inflation).

## Repository Structure
```text
├── data/                               # Folder for datasets (see README_DATA.md for licensing details)
│   └── README_DATA.md                  # Instructions on data replication and proprietary restrictions
├── output-charts/                      # Folder containing all generated PDF plots and visualizations
├── Thesis_Implementation.ipynb         # Main Jupyter Notebook with full source code and execution pipeline
├── Thesis_Implementation.html          # Static HTML export of the executed notebook for quick preview
├── requirements.txt                    # Python dependencies required to run the notebook
└── README.md                           # This file
