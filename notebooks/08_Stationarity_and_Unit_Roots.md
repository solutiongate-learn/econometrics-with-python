# Notebook 08: Stationarity and Unit Roots

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand the concept of stationarity
- Recognize the problems caused by non-stationary data
- Define and identify unit roots
- Apply formal unit root tests (ADF and KPSS)
- Determine the order of integration of a series

## 1. What is Stationarity?

A time series is (weakly) stationary if its statistical properties (mean, variance, autocovariance) do not change over time.

**Non-stationary series** can lead to **spurious regressions** — relationships that appear significant but are actually meaningless.

## 2. Unit Root Process

A process has a unit root if it can be written as:

$$ y_t = y_{t-1} + \epsilon_t $$

This is a random walk. Such series are integrated of order 1, I(1).

## 3. Visual Inspection

Always start by plotting the series:
```python
df['IMPORTS'].plot(title='Imports over time')
plt.show()
```

Look for trends, changing variance, or persistent behavior.

## 4. Formal Unit Root Tests

### Augmented Dickey-Fuller (ADF) Test

Most commonly used test.

```python
from statsmodels.tsa.stattools import adfuller

result = adfuller(df['IMPORTS'])
print('ADF Statistic:', result[0])
print('p-value:', result[1])
```

**Decision Rule**:
- p-value < 0.05 → Reject null → Series is stationary
- p-value > 0.05 → Fail to reject → Series has a unit root

### KPSS Test

Complementary test (tests stationarity around a trend).
```python
from statsmodels.tsa.stattools import kpss
```

## 5. Practical Workflow

1. Plot the series
2. Run ADF test
3. Run KPSS test (for confirmation)
4. If non-stationary, take first difference and re-test
5. Determine order of integration I(d)

## 6. Key Takeaways

- Most macroeconomic series are I(1)
- Never regress two I(1) series without checking for cointegration
- Always difference non-stationary series before modeling (unless cointegrated)
- Use both ADF and KPSS for robust conclusions

## Exercises

1. Test the `INCOME` and `IMPORTS` series for stationarity.
2. Difference a non-stationary series and verify it becomes stationary.
3. Compare ADF and KPSS conclusions.

---

**Next:** ARIMA Modelling or VAR.