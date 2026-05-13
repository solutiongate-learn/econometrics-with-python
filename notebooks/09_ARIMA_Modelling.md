# Notebook 09: ARIMA Modelling

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand AR, MA, ARMA, and ARIMA processes
- Identify ARIMA orders using ACF and PACF plots
- Follow the Box-Jenkins methodology
- Estimate and diagnose ARIMA models
- Generate forecasts

## 1. ARIMA Components

- **AR(p)**: Autoregressive process of order p
- **MA(q)**: Moving average process of order q
- **I(d)**: Integration order (differencing)
- **ARIMA(p,d,q)**: Combined model

## 2. Identification using ACF and PACF

```python
import statsmodels.api as sm

fig, axes = plt.subplots(1, 2, figsize=(12, 4))
sm.graphics.tsa.plot_acf(df['IMPORTS_diff'], ax=axes[0])
sm.graphics.tsa.plot_pacf(df['IMPORTS_diff'], ax=axes[1])
plt.show()
```

**Rules of thumb**:
- ACF decays slowly → Non-stationary (needs differencing)
- ACF cuts off after lag q → MA(q)
- PACF cuts off after lag p → AR(p)

## 3. Box-Jenkins Methodology

1. **Identification** — Determine p, d, q
2. **Estimation** — Estimate parameters
3. **Diagnostic Checking** — Check residuals (should be white noise)
4. **Forecasting**

## 4. Model Estimation

```python
from statsmodels.tsa.arima.model import ARIMA

model = ARIMA(df['IMPORTS'], order=(1,1,1))
results = model.fit()
print(results.summary())
```

## 5. Diagnostics

- Ljung-Box test for residual autocorrelation
- Jarque-Bera test for normality
- Plot residuals and squared residuals

## 6. Forecasting

```python
forecast = results.get_forecast(steps=5)
print(forecast.predicted_mean)
```

## 7. Key Takeaways

- ARIMA is powerful for univariate forecasting
- Proper identification (ACF/PACF + differencing) is critical
- Always check residual diagnostics
- `pmdarima` can help with automatic order selection

## Exercises

1. Identify ARIMA orders for the differenced import series.
2. Estimate an ARIMA model and generate forecasts.
3. Compare model performance using AIC/BIC.

---

**Next:** VAR Modelling or further modern topics.