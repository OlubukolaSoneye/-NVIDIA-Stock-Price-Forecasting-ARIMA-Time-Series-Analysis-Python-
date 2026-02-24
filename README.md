## 📈 NVIDIA Stock Price Forecasting | Time Series Modelling

## 💼 Business Context
Forecasting equity prices is central to portfolio management, risk 
assessment and financial modelling. NVIDIA's stock has experienced 
rapid growth and significant volatility in recent years, making it 
a compelling case for testing forecasting methods under near-random-walk 
market conditions. This project evaluates whether increasing model 
complexity improves six-month forecasts of NVIDIA's monthly closing price.

## 📌 Project Overview
Six time series models were built and compared using 66 months of 
Nasdaq closing price data. Daily prices were resampled to monthly 
end-of-period observations before modelling. The goal was to determine 
which forecasting approach delivers the most reliable short-term 
predictions under volatile market dynamics.

## 📁 Dataset
- **Source:** Nasdaq.com
- **Period:** 66 monthly observations
- **Processing:** Daily prices aggregated to monthly using end-of-month 
  resampling
- **Characteristics:** Strong upward trend from 2023, widening volatility, 
  non-stationary price levels
  <p align="center">
  <img src="Screenshot 2026-02-23 at 23.48.30.png"250"/>
</p>

<p align="center">
  <img src="Screenshot 2026-02-23 at 23.50.24.png"250"/>
</p>

## 🔬 Methodology

**Stationarity Testing**
The Augmented Dickey-Fuller test confirmed non-stationarity in price 
levels. First differencing of log prices achieved stationarity 
(ADF statistic: −7.61, p < 0.001).
<img src="Screenshot 2026-02-23 at 23.52.01.png" width="400"/>

**Model Selection**
ACF and PACF analysis of the differenced series revealed no significant 
autocorrelation at any lag, guiding selection of ARIMA(0,1,0) as the 
optimal specification.

**Models Benchmarked**
| Model | Type |
|-------|------|
| Naïve | Baseline |
| Historical Mean | Baseline |
| Simple Moving Average (3-month) | Classical |
| Simple Exponential Smoothing | Classical |
| Holt's Linear Trend | Classical |
| Holt-Winters | Classical |
| ARIMA(0,1,0) | Statistical |
| SARIMA(0,1,0)(0,0,1)₁₂ | Statistical |
| Regression (lagged returns) | Statistical |

## 📊 Results
<img src="Screenshot 2026-02-23 at 23.53.48.png"400"/>

| Model | MAE | MSE | MAPE |
|-------|-----|-----|------|
| Simple Exponential Smoothing | 1.57 | 2.90 | 0.83% |
| ARIMA(0,1,0) | 1.57 | 2.90 | 0.83% |
| Naïve | 1.74 | 3.39 | 0.93% |
| Simple Moving Average | 1.61 | 4.45 | 0.86% |
| Holt's Linear Trend | 11.17 | 156.48 | 5.95% |
| Holt-Winters | 18.72 | 461.54 | 9.97% |
| SARIMA | Higher than ARIMA | — | — |
| Regression | 30.72 | 1215.83 | 16.32% |
| Historical Mean | 119.05 | 14,175.29 | 63.59% |

<img src="Screenshot 2026-02-23 at 23.55.16.png" width="400"/>
<img src="Screenshot 2026-02-23 at 23.56.41.png" width="400"/>


## 🔍 Key Findings
- ARIMA(0,1,0) and SES achieved the lowest forecast errors (MAPE 0.83%)
- Complex models incorporating trend, seasonality or lagged returns 
  performed substantially worse
- Regression produced the highest error at MAPE 16.32% — lagged returns 
  carry no meaningful predictive signal for this series
- Results are consistent with near-random-walk behaviour, where price 
  changes are driven by unpredictable innovations rather than stable patterns
- Findings support the principle of parsimony in financial time series 
  forecasting

## 💡 Conclusion
For volatile equity time series exhibiting near-random-walk dynamics, 
simpler models outperform complex specifications. Increasing 
parameterisation introduced additional forecast error rather than 
improving accuracy — a finding with practical implications for 
short-term financial forecasting and model selection.

## 🛠 Tech Stack
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Statsmodels](https://img.shields.io/badge/Statsmodels-4051B5?style=flat)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

## 📬 Contact
Made by Bukola Soneye
🔗 LinkedIn: https://linkedin.com/in/bukola-soneye/
