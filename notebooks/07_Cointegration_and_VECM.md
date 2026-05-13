# Notebook 07: Cointegration and Vector Error Correction Models (VECM)

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand the concept of cointegration
- Apply the Engle-Granger two-step procedure
- Perform the Johansen cointegration test
- Estimate and interpret a Vector Error Correction Model (VECM)
- Distinguish between short-run and long-run relationships

## 1. Why Cointegration Matters

Many economic time series are non-stationary (I(1)). Regressing one I(1) series on another can lead to **spurious regression**.

However, if two or more I(1) series are **cointegrated**, they share a long-run equilibrium relationship. This is extremely useful in economics and finance.

## 2. Engle-Granger Two-Step Procedure

1. Estimate the long-run relationship using OLS
2. Test if the residuals are stationary (using ADF test)
3. If cointegrated, estimate the short-run ECM

```python
# Step 1: Long-run relationship
long_run_model = sm.OLS(y, X).fit()
residuals = long_run_model.resid

# Step 2: Test residuals for stationarity
adf_result = adfuller(residuals)
```

## 3. Johansen Cointegration Test

More powerful multivariate test.

```python
from statsmodels.tsa.vector_ar.vecm import coint_johansen

result = coint_johansen(df, det_order=0, k_ar_diff=1)
print(result.lr1)   # Trace statistic
print(result.cvt) # Critical values
```

## 4. Vector Error Correction Model (VECM)

If cointegration exists, we estimate a VECM:

```python
from statsmodels.tsa.vector_ar.vecm import VECM

vecm = VECM(df, k_ar_diff=1, coint_rank=1)
vecm_fit = vecm.fit()
print(vecm_fit.summary())
```

**Key Output**: The error correction term shows the speed of adjustment toward long-run equilibrium.

## 5. Interpretation

- **Long-run coefficients**: Equilibrium relationship
- **Error correction term**: How fast disequilibrium is corrected
- **Short-run coefficients**: Immediate dynamic effects

## 6. Practical Recommendations

- Always test for unit roots first
- Use Johansen test for multiple variables
- VECM is preferred when cointegration is present
- Combine with impulse response analysis for richer insights

## Exercises

1. Test two series for cointegration using Engle-Granger.
2. Estimate a VECM and interpret the error correction coefficient.
3. Compare results from Engle-Granger vs Johansen.

---

**Next:** We can create notebooks on Unit Roots, ARIMA, or VAR.