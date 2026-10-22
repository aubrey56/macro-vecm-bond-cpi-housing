# Macro-Financial Dynamics: Modeling 10-Year Bond Yields, Inflation, and Housing Starts via VECM

This repository contains the econometrics workflow, empirical dataset, and statistical outputs for analyzing the dynamic relationships between long-term capital markets, consumer inflation, and real estate construction activity in the U.S. economy (1959M01–2013M03).

---

## 📌 Project Overview
Using monthly historical data across 648 included observations, this study investigates how macroeconomic shocks transmit between three core variables:
* **`BOND10Y`**: 10-Year Government Bond Yield (Capital Markets)
* **`LOG(CPI)`**: Natural Logarithm of Consumer Price Index (Inflation Dynamics)
* **`HSTARTS`**: Real Estate Housing Starts (Physical Construction Supply)

---

## 🔬 Methodology & Empirical Strategy

1. **Unit Root Testing:** Identified non-stationarity across raw levels $I(1)$ to ensure stationary first-differencing.
2. **Johansen Cointegration Test:** Evaluated long-run equilibrium relationships using Johansen-Hendry-Juselius Case 3 (Intercept in CE and Test VAR).
   * **Result:** Both Trace ($\text{Stat} = 44.89, p = 0.0005$) and Max-Eigenvalue ($\text{Stat} = 32.38, p = 0.0009$) tests confirmed **exactly $R = 1$ Cointegrating Equation** at the 5% level.
3. **Vector Error Correction Model (VECM):** Specified a 3-variable system at raw levels with a lag structure of $1 \to 2$ to capture both long-run equilibrium vectors and short-run dynamic momentum.

---

## 📈 Key Empirical Findings

### 1. Long-Run Equilibrium Equation ($\text{CointEq1}$)
Normalizing on the 10-Year Bond Yield yields the following long-run fair value structural relationship:

$$\text{BOND10Y} = 0.6518 \cdot \text{LOG(CPI)} + 0.000136 \cdot \text{HSTARTS} + 3.3604$$

* **Fisher Inflation Effect:** Long-term yields hold a positive long-run coefficient ($0.6518$) relative to core price levels, proving that bond markets adjust to protect real purchasing power against persistent inflation.
* **Credit Demand Anchor:** Real estate expansion ($\text{HSTARTS}$) exerts a long-run positive effect ($0.000136$) on yields, reflecting real credit market demand.

---

### 2. Speed of Adjustment ($\text{COINTEQ1}$) Vector
The error correction row explains how the system adjusts when knocked out of long-run fair value balance:

| Variable | Adjustment ($\alpha$) | $t$-statistic | Economic Interpretation |
| :--- | :---: | :---: | :--- |
| **`D(BOND10Y)`** | **`-0.009575`** | **`[-2.22130]`** | **Stabilizing Anchor (Significant at 5%):** Yields actively drift downward by ~0.95% per month to correct structural over-valuations. |
| **`D(LOG(CPI))`** | **`0.000191`** | **`[4.77996]`** | **Nominal Adjustment (Significant at 1%):** Price levels actively adjust upward to close system dislocations. |
| **`D(HSTARTS)`** | `1.093003` | `[0.61131]` | **Long-Run Exogenous (Insignificant):** Housing construction reacts to short-run cycles rather than correcting long-run macro errors. |

---

### 3. Short-Run Dynamic Cross-Market Matrix

* **Inflation Sticky Momentum (`D(LOG(CPI(-1)))` $\rightarrow$ `D(LOG(CPI))`):** Strongest short-run signal in the model ($\beta = 0.466, t = 11.66$), demonstrating heavy inflation inertia.
* **Capital Market Inflation Shock (`D(LOG(CPI(-1)))` $\rightarrow$ `D(BOND10Y)`):** Immediate positive re-pricing ($\beta = 561.16, t = 4.24$) as fixed-income traders sell bonds during inflation surges.
* **The Delayed Financing Chill (`D(BOND10Y(-2))` $\rightarrow$ `D(HSTARTS)`):** A surge in bond yields produces a delayed negative shock on housing groundbreaks by Month 2 ($\beta = -38.32, t = -2.40$), reflecting the operational lag developers face when redrawing financing plans.
* **Housing Supply Mean-Reversion (`D(HSTARTS(-1))` $\rightarrow$ `D(HSTARTS)`):** Construction activity features sharp cyclical mean-reversion ($\beta = -0.359, t = -9.23$), where building surges are immediately followed by cool-down contractions.

---

## 🛠️ Software & Tools Used
* **EViews 13 / 14** (Econometric estimation, Johansen Rank Testing, VECM system analysis)
* **LaTeX** (Mathematical typesetting)
