# portfolio-optimization-mpt

Implementation of **Modern Portfolio Theory (MPT)** to determine the optimal asset allocation 

## Overview
This project applies the classical mean–variance framework to approximate the efficient frontier and identify the tangency portfolio (i.e., the portfolio with the maximum Sharpe ratio).

The method is based on Monte Carlo simulation: we generate $10,000$ admissible weight vectors and evaluate the corresponding return–risk pairs.

The objective is to maximize the Sharpe ratio:

$$S_p = \frac{E[R_p]-R_f}{\sigma_p}$$

where we assume $R_f = 0$

## Mathematical Foundation
Let $\mathbf{w} \in \mathbb{R}^n$ denote the portfolio weight vector satisfying:

$$\sum_{i=1}^{n} w_i = 1, \quad w_i \ge 0$$

**Expected portfolio return**

$$E[R_p] = \mathbf{w}^T E[\mathbf{R}]$$

**Portfolio variance**

$$\sigma_p^2 = \mathbf{w}^T \Sigma\mathbf{w}$$

**Portfolio volatility**

$$\sigma_p = \sqrt{\mathbf{w}^T \Sigma\mathbf{w}}$$

**Sharpe ratio**

$$S_p = \frac{E[R_p]-R_f}{\sigma_p}$$

**Parametric 95% daily VaR (normal approximation)**

$$\text{VaR}_{95} = \mu_p - 1.645 \, \sigma_p^{\text{daily}}$$

*(95% confidence level)*

Note: For the VaR calculation, $\mu_p$ and $\sigma_p^{\text{daily}}$ represent values on a daily basis, reflecting the potential loss over a 24-hour trading horizon.

## Implementation details
* Historical adjusted closing prices are obtained using `yfinance`.
* Log-returns are used to estimate expected returns and the covariance matrix.
* Matrix operations are implemented in a vectorized form using `NumPy`.
* The efficient frontier is approximated via Monte Carlo sampling.
* The tangency portfolio is selected as the portfolio with the highest Sharpe ratio among simulated portfolios.

## Benchmark Comparison
The optimized portfolio is compared to the S&P 500 ETF (SPY). Performance is evaluated primarily using the Sharpe ratio.

## Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Matplotlib, yfinance
* **Environment:** Jupyter Notebook
