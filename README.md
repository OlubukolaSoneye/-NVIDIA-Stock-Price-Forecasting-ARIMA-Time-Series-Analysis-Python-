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

  **Figure 1: NVIDIA Monthly Closing Price (Linear Scale)**
The series shows a pronounced upward movement from 2023, coinciding with 
heightened market interest in AI and data centre investment, alongside 
widening volatility consistent with a non-stationary process.
<p align="left">
  <img src="Screenshot 2026-02-23 at 23.48.30.png" width="700"/>
</p>

**Figure 2: Multiplicative Decomposition**
Decomposition confirms a dominant non-linear upward trend with negligible 
seasonal effects. Multiplicative residuals cluster around zero with 
homogeneous variance, confirming level-dependent variability in the series.
<p align="left">
  <img src="Screenshot 2026-02-23 at 23.50.24.png" width="700"/>
</p>

## 🔬 Methodology

## Stationarity Testing
The Augmented Dickey-Fuller test confirmed non-stationarity in price 
levels. First differencing of log prices achieved stationarity 
(ADF statistic: −7.61, p < 0.001).

**Figure 3: ACF and PACF of Monthly Log Returns**
All lags fall within the 95% confidence bounds, confirming the absence 
of serial correlation and supporting the random-walk characterisation 
of NVIDIA's monthly returns.
<p align="left">
  <img src="Screenshot 2026-02-23 at 23.52.01.png" width="700"/>
</p>

**Model Selection**
ACF and PACF analysis of the differenced series revealed no significant 
autocorrelation at any lag, guiding selection of ARIMA(0,1,0) as the 
optimal specification.


## 📊 Results

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

**Figure 4: Six-Month Forecasts — All Models vs Actual**
Simpler models tracking recent observations closely outperform those 
imposing fixed trend or seasonal structure. The divergence between 
model groups is pronounced over the forecast horizon.
<p align="left">
  <img src="Screenshot 2026-02-24 at 00.39.07.png" width="700"/>
</p>

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

**Figure 5: ARIMA(0,1,0) Six-Month Forward Forecast**
The optimal model produces a flat forecast equal to the final training 
value, consistent with random-walk dynamics where future price changes 
are driven by unpredictable innovations rather than past patterns.
<p align="left">
  <img src="Screenshot 2026-02-23 at 23.55.05.png" width="700"/>
</p>

**Figure 6: ARIMA(0,1,0) Residual Diagnostics**
Residuals oscillate around zero with no significant autocorrelation 
confirmed by a non-significant Ljung-Box test (p = 0.999). While mild 
non-normality is present in the upper tail, the absence of serial 
correlation validates the model for forecasting purposes.
<p align="left">
  <img src="Screenshot 2026-02-23 at 23.56.41.png" width="700"/>
</p>

## 💡 Conclusion
For volatile equity time series exhibiting near-random-walk dynamics, 
simpler models outperform complex specifications. Increasing 
parameterisation introduced additional forecast error rather than 
improving accuracy — a finding with practical implications for 
short-term financial forecasting and model selection.

## 🛠 Tech Stack
Python (Pandas, Statsmodels, Matplotlib, Jupyter)

## 📬 Contact
Made by Bukola Soneye
🔗 LinkedIn: https://linkedin.com/in/bukola-soneye/


