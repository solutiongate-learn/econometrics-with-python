# Notebook 00: Setup and Data

**Project:** Python Notebooks for *A Practical Introduction to Econometric Methods* (Watson & Teelucksingh, 2002)

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand the purpose and structure of this notebook series
- Set up your Google Colab environment correctly
- Load and explore the Trinidad and Tobago macroeconomic data used in the book
- Follow best practices for reproducible econometric analysis in Python

## 1. Project Overview

This series of notebooks converts the key concepts from the excellent textbook *A Practical Introduction to Econometric Methods: Classical and Modern* by Patrick K. Watson and Sonja S. Teelucksingh into modern Python.

**Why Python?**

- `statsmodels` provides output very close to classical econometrics software (EViews, Stata)
- `linearmodels` extends capabilities for IV, robust inference, etc.
- Excellent visualization and reproducibility
- Free and widely used in academia and industry

We aim to explain not just *how* to run regressions, but *why* we do certain things, how to interpret results, and how to diagnose problems.

## 2. How to Use These Notebooks

### Recommended Workflow

1. Open the notebook directly in Google Colab
2. Run cells from top to bottom
3. Each notebook is designed to be **mostly self-contained**
4. Data is loaded from this repository via raw GitHub URLs

### Google Colab Tips

- Use **GPU/TPU runtime** only if needed (not required for most notebooks)
- Enable **high-RAM** if working with larger datasets later
- Always run the Setup cell first

## 3. Environment Setup

```python
# ==================== COLAB SETUP ====================
!pip install -q statsmodels linearmodels pmdarima seaborn

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import statsmodels.formula.api as smf
from linearmodels.iv import IV2SLS

import warnings
warnings.filterwarnings('ignore')

sns.set_style("whitegrid")
plt.rcParams['figure.figsize'] = (10, 6)
print("Packages loaded successfully!")
```

## 4. Data Philosophy

The original book uses time series data from Trinidad and Tobago (1967–1991). The full dataset is referenced in Appendix 1.2 and `WT_DATA.XLS`.

In this project:

- We use cleaned versions of the key variables
- Data is hosted in the repository under `/data/`
- Notebooks load data directly via raw GitHub URL (no manual upload needed)
- We prioritize **reproducibility** and **clarity**

## 5. Loading Data

```python
# Load data from repository (raw GitHub URL)
url = "https://raw.githubusercontent.com/solutiongate-learn/econometrics-with-python/main/data/trinidad_tobago_core.csv"
df = pd.read_csv(url)

df.head()
```

## 6. Quick Data Exploration

```python
print("Shape:", df.shape)
print("\nColumns:", df.columns.tolist())
print("\nInfo:")
df.info()

df.describe().T
```

## 7. Next Steps

In the following notebooks, we will:

- Replicate and extend the examples from the book
- Focus heavily on **interpretation** and **diagnostics**
- Compare classical approaches with modern Python implementations

---

**Next Notebook:** `01_OLS_Fundamentals.md`