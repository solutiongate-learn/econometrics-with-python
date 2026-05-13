# Notebook 13: Forecasting Evaluation

## Learning Objectives

By the end of this notebook, you will be able to:

- Evaluate forecast accuracy using multiple metrics
- Understand the strengths and limitations of different error measures
- Compare competing forecasting models properly
- Apply basic forecast encompassing and Diebold-Mariano tests

## 1. Why Forecast Evaluation Matters

A model that fits historical data well may not forecast well. Proper out-of-sample evaluation is essential.

## 2. Common Forecast Error Metrics

### Scale-dependent measures
- **RMSE** (Root Mean Squared Error)
- **MAE** (Mean Absolute Error)

### Scale-independent measures
- **MAPE** (Mean Absolute Percentage Error)
- **sMAPE** (Symmetric MAPE)

### Theil’s Inequality Coefficient

```python
# Example calculation
from sklearn.metrics import mean_squared_error, mean_absolute_error

rmse = np.sqrt(mean_squared_error(actual, forecast))
mae = mean_absolute_error(actual, forecast)
```

## 3. Comparing Models

- Use the same out-of-sample period
- Consider both point forecasts and interval forecasts
- Use statistical tests for comparing predictive accuracy (Diebold-Mariano test)

## 4. Best Practices

- Always reserve a hold-out sample for evaluation
- Report multiple metrics
- Consider both statistical and economic significance of forecast improvements
- Re-estimate models as new data becomes available (expanding or rolling windows)

## 5. Key Takeaways

- No single metric is perfect
- RMSE penalizes large errors more heavily
- Always evaluate forecasts on unseen data
- Combine statistical metrics with economic judgment

## Exercises

1. Generate forecasts from ARIMA and VAR models and compare their RMSE and MAE.
2. Calculate Theil’s U coefficient.
3. Discuss when MAPE can be misleading.

---

**Next:** Best Practices notebook or other specialized topics.