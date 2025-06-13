# 📈 US CPI Forecasting using SARIMAX  
**A Structural Time Series Analysis using FRED Macroeconomic Data**

---

## 🧾 Project Overview

This project aims to forecast **US monthly inflation rates (YoY)** by applying the **SARIMAX (Seasonal ARIMA with Exogenous Variables)** model to macroeconomic data retrieved from the [FRED API](https://fred.stlouisfed.org/).  
The model incorporates both **time-series dynamics and exogenous economic indicators** to produce interpretable, policy-sensitive inflation forecasts.

---

## 🔧 Methodology

### 1. **Data Source**
- FRED API (2000–2025)
  - CPI (`CPIAUCSL`)
  - 10Y Treasury Yield (`DGS10`)
  - Unemployment Rate (`UNRATE`)
  - Crude Oil Prices (`MCOILWTICO`)
  - Consumer Sentiment Index (`UMCSENT`)

### 2. **Model: SARIMAX**
SARIMAX is a generalized form of the ARIMA model. It combines:

| Component            | Description |
|----------------------|-------------|
| ARIMA (p, d, q)      | Autoregressive + Differencing + Moving Average |
| Seasonal (P, D, Q, s)| Captures periodic patterns (monthly cycle: s=12) |
| Exogenous Variables  | External economic indicators like interest rate, unemployment, oil price |

### 3. **Model Selection**
- Grid search over all combinations of (p,q,P,Q) ∈ {0,1}
- Model evaluation based on **Akaike Information Criterion (AIC)**

---

## 📉 What is AIC?

AIC (Akaike Information Criterion) is a metric to evaluate model performance by balancing **fit vs. complexity**.  

\[
\text{AIC} = -2 \cdot \log(\hat{L}) + 2k
\]

Where:
- \(\hat{L}\): model likelihood
- \(k\): number of estimated parameters

✅ **Lower AIC = better model**  
⚠️ AIC penalizes overfitting, encouraging parsimonious models.

---

## ✅ Best Model Summary

```plaintext
Model: SARIMAX(1, 0, 1)(1, 1, 1, 12)
Exogenous Variables: Interest Rate, Unemployment, Oil, Consumer Sentiment
AIC: 221.39 (lowest among all candidates)
