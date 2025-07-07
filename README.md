## 🧠 Project Overview

This project provides a comprehensive analysis of the VIX index and its related derivatives, with a focus on mathematical modeling, financial interpretation, and numerical implementation. Our work is grounded in the Carr-Madan framework and explores futures pricing in stochastic volatility settings, particularly through Heston-like dynamics.

---

## 🧾 Contents

1. [`derivatives_project.pdf`](./derivatives_project.pdf): Full analytical and mathematical report.
2. [`vix_and_var.ipynb`](./vix_and_var.ipynb): Jupyter notebook containing Python code for simulations, pricing, and calibration.
3. [`Fin404-2025-VIXNCO-Data.xlsx`](./Fin404-2025-VIXNCO-Data.xlsx): Market data used for calibration (e.g., SPX options, VIX futures).
5. [`README.md`](./README.md): You are here.

---

## 📘 Theoretical Foundations

Our analysis is structured in four main parts:

### 1. Volatility and Variance Derivatives Market

- History and motivations behind variance swaps and VIX.
- Comparison of VIX, variance swaps, and variance futures.
- Use cases and investor strategies (hedging, speculation, volatility arbitrage).

### 2. Carr-Madan Formula

We derive the Carr-Madan static replication formula:

\[
V_0 = a_0 + n_0 S_0 e^{-\delta T} + \int_0^{x_0} w(k) \cdot \text{Put}(k) \,dk + \int_{x_0}^{\infty} w(k) \cdot \text{Call}(k) \,dk
\]

Where \( w(k) = H''(k) \) and \( H \) is the desired payoff function (e.g., \( H(S_T) = \log S_T \) or \( S_T^p \)).

- Includes numerical limitations in implementation due to strike discretization.

### 3. VIX Construction and Interpretation

We show that under no-arbitrage and stochastic volatility assumptions, the squared VIX approximates the **risk-neutral expected variance** over the next 30 days:

\[
\left( \frac{VIX_t}{100} \right)^2 \approx \frac{1}{\eta} \mathbb{E}_t^Q \left[ \int_t^{t+\eta} V_s \, ds \right]
\]

- Derived from model-free option pricing.
- Includes log-return identities and their expectations under the risk-neutral measure.

### 4. Futures Pricing and Model Calibration

Assuming an affine stochastic process for \( V_t \):

\[
dV_t = \lambda(\theta - V_t)dt + \xi \sqrt{V_t} \left( \rho \, dB_t^Q + \sqrt{1 - \rho^2} dZ_t^Q \right)
\]

We derive closed-form expressions for:

- **Variance Futures Price**:
  \[
  f_t^{\text{VA}}(T) = \frac{10,000}{T - t_0} \left( \int_{t_0}^t V_u \, du + a^*(T-t) + b^*(T-t) V_t \right)
  \]

- **VIX Futures Price** using Laplace transform identity:
  \[
  f_t^{\text{VIX}}(T) = \frac{50}{\sqrt{\pi \eta}} \int_0^{\infty} \left( 1 - e^{-\ell(s, T-t, V_t)} \right) \frac{ds}{s^{3/2}}
  \]

We calibrate parameters \( (\lambda, \theta, \xi, V_t) \) using RMSE minimization and analyze sensitivity.

---

## 💻 How to Run

### 🛠️ Requirements

Install the necessary packages using:

```bash
pip install -r requirements.txt
