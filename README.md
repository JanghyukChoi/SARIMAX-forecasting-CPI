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

```
Model: SARIMAX(1, 0, 1)(1, 1, 1, 12)
Exogenous Variables: Interest Rate, Unemployment, Oil, Consumer Sentiment
AIC: 221.39 (lowest among all candidates)
```

Model	AIC
baseline	238.99
with_oil	273.08
with_conf	239.53
all	221.39 ✅

### 📊 Forecast Result (2025 H2)
```
Month	Forecast YoY (%)	95% CI Lower	95% CI Upper
2025-07	2.47	1.81	3.13
2025-08	2.58	1.42	3.74
2025-09	2.60	1.12	4.09
2025-10	2.55	0.81	4.28
2025-11	2.54	0.60	4.49
2025-12	2.58	0.45	4.70
```
### ⚠️ Limitations
```
Model-Level
Assumes linear relationships between inflation and exogenous variables

Not robust to structural breaks (e.g. pandemic, war, regime shifts)

Requires known future values of exogenous variables for forecasting

Study-Level
Exogenous forecasts are repeated recent values, not forward-looking

Only 4 variables used (misses fiscal policy, housing costs, etc.)

Confidence intervals widen significantly (high uncertainty)

No rolling forecast or out-of-sample validation applied
```
###🚀 Future Direction
```
Dynamic Forecasting of Exogenous Variables

Currently, the SARIMAX model assumes fixed or repeated exogenous inputs.
The next step is to build a more autonomous forecasting system by:

Building forecasting models for each exogenous variable (e.g., VAR, SARIMA, XGBoost)

Feeding predicted exog paths into SARIMAX for full-scenario CPI forecasting

Exploring joint modeling with Bayesian state space models or machine learning ensembles
```
###📁 File Structure

```
├── Using_SARIMAX_Forecast_CPI.ipynb   # Main notebook (analysis + modeling)
├── README.md                          # This file
```



