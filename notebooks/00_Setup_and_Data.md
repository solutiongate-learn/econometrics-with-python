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

Run the following cell to install the required packages: