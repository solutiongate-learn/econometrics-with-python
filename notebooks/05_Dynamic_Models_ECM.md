# Notebook 05: Dynamic Models and Error Correction

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand different types of dynamic models
- Implement Almon Polynomial Distributed Lags
- Apply the Koyck transformation
- Estimate Partial Adjustment and Adaptive Expectations models
- Build and interpret Error Correction Models (ECM)

## 1. Why Dynamic Models?

Economic relationships often involve **lags**. Current behavior depends on past values of variables.

Common reasons for lags:
- Adjustment costs
- Expectation formation
- Habit persistence
- Contracts and institutional delays

## 2. Types of Dynamic Models

### Almon Polynomial Distributed Lag (PDL)

```python
# Using statsmodels for distributed lags (simplified example)
from statsmodels.tsa.deterministic import DeterministicProcess

# For full Almon lag implementation, consider using the `pydynpd` package or custom design
```

### Koyck Transformation

Transforms infinite geometric lag into a model with lagged dependent variable.

### Partial Adjustment Model

```python
# Partial Adjustment
model_pa = smf.ols('y ~ x + y_lag1', data=df).fit()
```

### Adaptive Expectations

Expectations are updated based on past errors.

## 3. Error Correction Model (ECM)

The ECM is one of the most important dynamic specifications. It combines short-run dynamics with long-run equilibrium.

```python
# Simple ECM representation
# Δy_t = α + βΔx_t + γ(y_{t-1} - δx_{t-1}) + error

# In practice, we often estimate using the Engle-Granger two-step method or directly
```

**Key Concept**: The error correction term (γ) measures how fast the system returns to equilibrium after a shock.

## 4. Autoregressive Distributed Lag (ADL) Models

General and flexible framework that nests many other models.

## 5. Key Takeaways from Chapter 5

- Dynamic models are essential for time series data
- ECM is particularly powerful because it separates short-run and long-run effects
- Always check for cointegration before estimating an ECM
- The Durbin h-test is used when lagged dependent variables are present

## Exercises

1. Estimate a simple Partial Adjustment model.
2. Interpret the speed of adjustment coefficient in an ECM.
3. Compare Almon lag vs Koyck transformation.

---

**Next:** We can move to modern time series topics (Unit Roots, ARIMA, VAR, or Cointegration).