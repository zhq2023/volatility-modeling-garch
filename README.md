# Volatility Modeling with GARCH Family Models

Repository for code and analysis accompanying the paper:  
**"Volatility Modeling with GARCH Family Models: Evidence from S&P 500 ETF Daily Data"**

---

## 📌 Overview

Understanding and forecasting volatility is critical in quantitative finance, from risk management to derivative pricing. This study evaluates various GARCH family models—including the classic GARCH(1,1), EGARCH, GJR-GARCH, and the advanced AR(1)-GJR-GARCH with skewed t-distribution—to model volatility in the SPY ETF (S&P 500 proxy) using over 25 years of daily data.

All code, model outputs, and visualizations are available in this repository.

---

## 📊 Data Source

- **Ticker:** SPY (S&P 500 ETF)  
- **Date Range:** November 1999 – May 2025  
- **Source:** [Alpha Vantage](https://www.alphavantage.co/)  
- **Features:**  
  - Raw: Open, High, Low, Close, Volume  
  - Derived: HL2, OHLC4, ATR(14), ATR%, daily range  

The data pipeline uses Python (`requests`, `pandas`) to fetch, process, and store the data in CSV format.

### Data Fetching Steps:

1. Go to [Alpha Vantage](https://www.alphavantage.co/) and sign up for a free API key.  
2. Open the `data_fetch.py` script and replace the following line with your own API key.

> ⚠️ Remember to replace `'YOUR_API_KEY'` with your own API key in `data_fetch.py`.  

---

## 🧠 Modeling Strategy

This study compares 12 model configurations across:

- **Volatility Structures:** GARCH(1,1), EGARCH(1,1), GJR-GARCH(1,1)  
- **Mean Structures:** Constant Mean, AR(1)  
- **Error Distributions:** Student's t, Skewed t  

### Notable Models:

| Model                          | AIC      | BIC      |
|-------------------------------|----------|----------|
| **AR(1)-GJR-GARCH(1,1)-skew-t** | **17192.67** | **17246.81** |
| GJR-GARCH(1,1)-skew-t (Constant) | 17210.53 | 17257.91 |
| GJR-GARCH(1,1)-t (AR1)        | 17287.73 | 17335.10 |

### Best Performing Model:

- **Model:** AR(1)-GJR-GARCH(1,1) with Skewed t-distribution  
- **Log-Likelihood:** -8588.33  
- **Why it works:**  
  - Captures autocorrelation (AR1)  
  - Models asymmetry in shocks (γ = 0.2075)  
  - Handles fat tails and skew (η = 7.57, λ = -0.1794)  

---

## 🔍 Diagnostic Highlights

- **Ljung-Box Test:** No residual autocorrelation  
- **Jarque-Bera Test:** p < 0.0001 → Residuals are left-skewed and fat-tailed  
- **Volatility Clustering:** ACF/PACF of squared residuals show no significant lags  

---

## 📈 Applications

- **10-day Volatility Forecasting**  
- **Value-at-Risk (VaR)** with skewed t-distribution  
- **Expected Shortfall (ES)** for tail risk  
- **Backtesting:**  

---

## 📂 Repository Structure
├── data/
├── results/
├── visualization/
├── data_fetch.py/
├── main_notebook.ipynb/
├── requirements.txt/
├── environment.yml/
├── README.md/
└── LICENSE

---

## 🛠️ Dependencies

Install via pip:

```bash
pip install -r requirements.txt

```
---

## ✍️ Author 
Zhiqi Pang (GitHub @zhq2023) 
Feel free to use, cite, or fork this project for academic or professional use.

---

## 🧾 License
This project is licensed under the MIT License — feel free to reuse, modify, and distribute with proper attribution.

