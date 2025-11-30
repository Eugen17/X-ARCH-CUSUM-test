# Residual-based CUSUM Test in X-ARCH Models

This repository contains simulation code and a short real-data application for the **residual-based CUSUM test** in regression models with ARCH errors (X-ARCH models). It accompanies the master’s thesis:

> *On residual-based CUSUM test in X-ARCH models* – Yevhen Perehuda, 2023.

The code is written in Python (Jupyter notebook) and uses the `arch` library to simulate and estimate ARCH/X-ARCH models.

> ⚠️ This code is for **research and educational purposes only** and is **not** intended for production use.

---

## Contents

- `X_ARCH_CUSUM_test_simulation.ipynb`  
  Main notebook that:
  - Implements several versions of residual-based CUSUM statistics for ARCH and X-ARCH models.
  - Runs Monte Carlo simulations to study **empirical size and power** in different scenarios.
  - Approximates critical values for CUSUM statistics via simulation.
  - Applies the test to real financial data (yen/dollar exchange rate) and plots the CUSUM process.

- `On_residual_based_CUSUM_test_in_X_ARCH_models_Master_Thesis_Yevhen_Perehuda.pdf`  
  Full thesis with the theoretical background, simulation design, and detailed discussion of the results.

---

## Implemented Models and Tests

The notebook implements and studies residual-based CUSUM tests in the following settings:

1. **Constant mean model with ARCH(1) errors**  
   \[
   y_t = \mu + u_t,\quad
   u_t = \sigma_t \varepsilon_t,\quad
   \sigma_t^2 = \omega + \alpha u_{t-1}^2
   \]
   - Tests for a structural break in the **mean**.
   - Uses average-corrected residuals to obtain pivotal CUSUM statistics.
   - Monte Carlo simulations compute empirical size and power over different sample sizes, break fractions, and mean shifts.

2. **Change-point covariate model (indicator regressor)**  
   \[
   y_t = \lambda \mathbf{1}_{\{t \leq pT\}} + u_t
   \]
   with both:
   - IID errors, and  
   - ARCH(1) errors.

   Here the CUSUM statistic is adapted to known change-point covariates. The notebook:
   - Simulates data with a known first change-point in the covariate.
   - Tests for an additional unknown change in the mean or in the indicator coefficient.
   - Estimates empirical size and power of the test.

3. **Seasonal dummy X-ARCH model**  
   \[
   y_t = \mu + \sum_{k=1}^d \lambda_k \mathbf{1}_{\{t \equiv k \ (\mathrm{mod}\ d)\}} + u_t,
   \quad u_t = \sigma_t \varepsilon_t,\quad \sigma_t^2 = \omega + \alpha u_{t-1}^2
   \]
   - Uses seasonal dummies as covariates (e.g. \(d = 3\)).
   - Tests both for changes in the **mean** and in one of the seasonal coefficients.
   - Investigates how seasonality and multiple covariates affect the test’s power and size.

4. **Limiting distribution and critical values**

   The notebook also simulates:
   - The supremum of Brownian-motion-based functionals that appear as limiting distributions of certain CUSUM statistics.
   - Approximate **critical values** for different parameters \(p\), sample sizes \(T\), and significance levels, stored in a Python dictionary for later use.

---

## Real Data Example

The notebook includes a small empirical application:

- **Data:** Yen/dollar exchange rate returns (1998–2003), as in Lee et al. (2004).
- **Model:** ARCH(1) model with constant mean.
- **Steps:**
  - Fit the X-ARCH model to the data using `arch_model` from the `arch` package.
  - Compute the residual-based CUSUM statistic over time.
  - Plot the CUSUM process and identify a potential structural break date.
  - Compare with historical events and monetary policy changes.

The corresponding analysis and interpretation are presented in the thesis.

---

## Requirements

The notebook was developed in Python 3.10 and uses:

- `arch`
- `numpy`
- `pandas`
- `scipy`
- `matplotlib`
- `statsmodels`
- `scikit-learn`
- `tqdm`
- `jupyter`

You can install the main dependencies via:

```bash
pip install arch numpy pandas scipy matplotlib statsmodels scikit-learn tqdm jupyter
