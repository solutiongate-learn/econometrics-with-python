# Notebook 01: OLS Fundamentals

**The General Linear Regression Model**

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand the structure of the General Linear Regression Model
- Derive and apply Ordinary Least Squares (OLS) estimation
- Use `statsmodels` to estimate and interpret regression models
- Interpret coefficients in an economic context
- Replicate the import function example from Chapter 1 of the book

## 1. Introduction

This notebook introduces the core of classical econometrics: the **General Linear Regression Model** and **Ordinary Least Squares (OLS)** estimation.

The book begins with a simple but powerful Keynesian open-economy model. We focus on the **import function** as our main example:

$$
M_t = \beta_1 + \beta_2 Y_t + \beta_3 \frac{p_m}{p_d} + u_t
$$

Where:
- $M_t$ = Imports
- $Y_t$ = Income
- $p_m / p_d$ = Relative price ratio

## 2. The General Linear Regression Model

In matrix form:

$$
y = X\beta + u$$

**Assumptions (Classical Linear Regression Model):**

1. $E(u) = 0$
2. $Var(u) = \sigma^2 I$ (Homoscedasticity + no autocorrelation)
3. $X$ is non-stochastic (fixed in repeated samples)

## 3. Ordinary Least Squares (OLS)

OLS finds $\hat{\beta}$ that minimizes the sum of squared residuals:

$$
\hat{\beta} = (X'X)^{-1} X'y
$$

## 4. Application: Import Function (Trinidad & Tobago)

We replicate the example from Chapter 1 using our prepared dataset.

```python
url = "https://raw.githubusercontent.com/solutiongate-learn/econometrics-with-python/main/data/trinidad_tobago_core.csv"
df = pd.read_csv(url)

# Define dependent and independent variables
y = df['IMPORTS']
X = df[['INCOME', 'RATIO']]
X = sm.add_constant(X)  # Add intercept

model = sm.OLS(y, X).fit()
print(model.summary())
```

## 5. Interpreting the Results

Key outputs to focus on:

- **Coefficients**: Economic interpretation (marginal propensity to import, price elasticity)
- **Standard Errors & t-statistics**: Statistical significance
- **R-squared**: Goodness of fit
- **F-statistic**: Overall significance

Compare these results with the EViews output shown in the book (Exhibit 1.1).

## 6. Key Takeaways from Chapter 1

- OLS is BLUE under the classical assumptions (Gauss-Markov Theorem)
- Always check economic plausibility of coefficients
- Interpretation matters more than just statistical significance
- The constant term often has limited economic meaning

## Exercises

1. Change the model specification and compare results.
2. Interpret the coefficient on `RATIO` in economic terms.
3. What happens to the model if we remove the constant term?

---

**Next:** Notebook 02 – Evaluating OLS Fit and Inference