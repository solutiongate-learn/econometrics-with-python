# Notebook 05: Dynamic Models and Error Correction

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand why dynamic models are important
- Apply different lag structures (Almon, Koyck)
- Estimate Partial Adjustment and Adaptive Expectations models
- Build and interpret Error Correction Models (ECM)
- Distinguish between short-run and long-run effects

## 1. Why Dynamic Models?

Economic behavior often depends on the past. Lags arise due to adjustment costs, habits, contracts, or expectation formation.

## 2. Common Dynamic Specifications

### Almon Polynomial Distributed Lags

Allows flexible lag structures with fewer parameters.

### Koyck Transformation

Converts infinite geometric lags into a model with a lagged dependent variable.

### Partial Adjustment Model

```python
model_pa = smf.ols('y ~ x + y_lag', data=df).fit()
```

### Adaptive Expectations

Expectations are revised based on past forecast errors.

## 3. Error Correction Model (ECM)

The ECM is powerful because it combines:
- Short-run dynamics
- Long-run equilibrium relationship

```python
# Conceptual form
# Δy_t = α + βΔx_t + γ(y_{t-1} - δ x_{t-1}) + error
```

The coefficient **γ** (error correction term) shows how fast the system returns to equilibrium after a shock.

## 4. Key Takeaways

- Dynamic models capture how variables adjust over time
- ECM is especially useful when variables are cointegrated
- Always interpret both short-run and long-run coefficients
- Check for cointegration before estimating an ECM

## 5. Exercises

1. Estimate a simple Partial Adjustment model.
2. Interpret the speed of adjustment in an ECM.
3. Compare Almon lags vs Koyck transformation.

---

**Next:** Notebook 06 – Instrumental Variables