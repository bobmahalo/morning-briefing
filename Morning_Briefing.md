# Yield Stacker Engine: Live Allocations
**Generated:** 2026-10-02 18:45:21 UTC | **Engine:** Antigravity V3 Core (Yield Stacker)

> **Disclaimer:** *This report is for educational and informational purposes only and does not constitute financial advice. The author is not a licensed financial advisor. All investments carry risk, and you should conduct your own due diligence before making any financial decisions.*

> **Methodology:** Cash Secured Puts on Deep Value survivors, collateralized by 4.5% Treasury Yield. 
> Filtered for Absolute IV > 30% and Delta <= -0.15.

## Yield-Stacked Opportunities

| Ticker | Spot Price | Strike | DTE | Delta | Absolute IV | Bid Premium | Stacked Annual | Stacked Monthly | Mean Tested |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **`DVA`** | $177.69 | $150.00 | 49 | -0.14 | 47.6% | $1.80 | **13.44%** | **1.12%** | N/A |
| **`STT`** | $176.37 | $155.00 | 49 | -0.14 | 33.8% | $1.30 | **10.75%** | **0.90%** | N/A |
| **`TFC`** | $46.47 | $40.00 | 49 | -0.12 | 33.9% | $0.30 | **10.09%** | **0.84%** | -7.1% (S/I Accel) |
| **`DD`** | $130.51 | $115.00 | 49 | -0.15 | 35.3% | $0.85 | **10.01%** | **0.83%** | N/A |
| **`CBOE`** | $273.61 | $235.00 | 42 | -0.13 | 42.9% | $1.35 | **9.49%** | **0.79%** | -4.9% (S/I Accel) |
| **`DVN`** | $47.40 | $41.00 | 42 | -0.11 | 37.5% | $0.23 | **9.38%** | **0.78%** | N/A |
| **`JBL`** | $305.62 | $260.00 | 42 | -0.12 | 44.5% | $1.35 | **9.01%** | **0.75%** | -4.1% (S/I Accel) |
| **`NTRS`** | $171.53 | $150.00 | 49 | -0.14 | 35.1% | $0.90 | **8.97%** | **0.75%** | N/A |
| **`OKE`** | $87.48 | $75.00 | 49 | -0.11 | 33.2% | $0.45 | **8.97%** | **0.75%** | N/A |
| **`PYPL`** | $52.81 | $44.00 | 42 | -0.15 | 57.2% | $0.19 | **8.25%** | **0.69%** | N/A |
| **`COR`** | $307.87 | $270.00 | 49 | -0.13 | 32.4% | $1.05 | **7.40%** | **0.62%** | N/A |
| **`MRSH`** | $170.47 | $150.00 | 49 | -0.12 | 30.4% | $0.40 | **6.49%** | **0.54%** | -6.5% (S/I Accel) |
| **`IVZ`** | $30.79 | $26.00 | 49 | -0.12 | 40.1% | $0.05 | **5.93%** | **0.49%** | N/A |
| **`BDX`** | $176.55 | $145.00 | 49 | -0.10 | 44.7% | $0.25 | **5.78%** | **0.48%** | N/A |
| **`COF`** | $195.30 | $170.00 | 42 | -0.14 | 39.4% | $0.20 | **5.52%** | **0.46%** | N/A |
| **`FDS`** | $269.08 | $220.00 | 49 | -0.12 | 53.7% | $0.25 | **5.35%** | **0.45%** | N/A |
| **`KMI`** | $30.97 | $27.00 | 42 | -0.09 | 30.3% | $0.01 | **4.82%** | **0.40%** | N/A |
| **`RJF`** | $158.23 | $140.00 | 49 | -0.14 | 32.7% | $0.05 | **4.77%** | **0.40%** | N/A |

---
*Antigravity V3 Core | Zero Discretion | Adversarial Validation*

<details>
<summary><b>📖 Antigravity V3: Quantitative Engine Methodology (Click to Expand)</b></summary>

### Overview
Antigravity V3 is built on a strict, adversarial quantitative framework designed to eliminate emotional trading, "vibe-based" investments, and manual screening fatigue. The core philosophy is absolute mathematical rigor: if a thesis cannot be mathematically proven against historical and current SEC/market data, the trade is rejected.

---

### 1. The Architectural Philosophy: 4-Layer Separation

To ensure the purity of the data and the math, the system enforces a strict 4-layer separation. This prevents "data bleed" (where a model might subconsciously favor an asset due to biased fetching) and ensures scalability.

1. **Ingestion (The Oracles):** Pure data fetching and normalization. Connects to SEC EDGAR, market feeds, and options clearing houses. No math happens here.
2. **Quantitative Models (The Brain):** Pure mathematical functions. Data goes in; objective scores, ratios, and risk metrics come out.
3. **Strategy Desk (The Rules):** Takes the mathematical outputs and applies strict risk-management and contract-selection rules.
4. **Reporting (The Eyes):** Formats the outputs into actionable intelligence (markdown reports, tables) without manipulating the underlying data.

---

### 2. Core Evaluation Engines

At the heart of the system are distinct quantitative models that evaluate equities from different philosophical angles. An asset must survive these engines to even be considered for capital allocation.

#### Engine A: The Deep Value Model
This model hunts for statistically underpriced companies with fortress-like balance sheets. It uses a weighted scoring system based on classic quantitative value investing:
* **Altman Z-Score:** Evaluates the probability of bankruptcy. Companies that don't pass a baseline threshold are immediately discarded.
* **Piotroski F-Score:** A 9-point scale measuring the trend of a company's financial health (profitability, leverage, liquidity, and operating efficiency).
* **Return on Invested Capital (ROIC):** Measures how efficiently management uses capital to generate profits.
* **Shareholder Yield:** Looks beyond just dividends, combining dividend yield, share buybacks, and debt paydown.

#### Engine B: The "Munger" Reality Check
Forked from the Deep Value model, this engine represents a hyper-strict, no-nonsense approach to capital allocation. It completely strips out any "momentum" rewards and focuses entirely on undeniable cash generation and durability.
* **The Strict Gate:** Demands a Free Cash Flow (FCF) Yield of **>= 4.0%**. If a company isn't generating real cash relative to its valuation, it fails.
* **Durability Over Hype:** Reallocates weight heavily toward the Piotroski F-Score and multi-year fundamental durability, ignoring short-term price action.

---

### 3. The Filter Process & Execution Strategies

Once the universe of equities is scored by the engines, they are passed through specific filters depending on the overarching strategy.

#### The Multibagger Equity Filter (Growth + Fortress)
This filter hunts for long-term equity holds by finding the rare intersection of Growth at a Reasonable Price (GARP) and extreme financial safety.
* **Growth Requirement:** Minimum 3-Year Revenue CAGR > 15%. The business must be actively expanding.
* **Safety Requirement:** Debt-to-Equity Ratio < 0.20. Growth cannot be fueled by reckless leverage.
* **Result:** A highly curated list of companies that can weather macroeconomic storms while compounding aggressively.

#### The Options Strategy Desk (Income & Acquisition)
Antigravity doesn't treat options as speculative bets; it treats them as mathematical tools for yield generation or discounted asset acquisition.
* **Mathematical Pre-Verification:** No contract is selected without first proving the mathematical edge (e.g., verifying the yield against the risk profile).
* **Market Plumbing Integration:** Utilizes Net Gamma Exposure (GEX) and Expected Move metrics to place strikes intelligently. We avoid placing strikes inside high-gravity zones where market makers are likely to pin the price.
* **Bid/Ask Discipline:** Strict enforcement of liquidity rules—sales are always calculated at the `bid`, and buys at the `ask`. No optimistic "mid-price" assumptions.

---

### Conclusion
The Antigravity V3 methodology is not about predicting the future; it is about exploiting mathematical certainty in the present. By forcing every asset through these adversarial models and unforgiving filters, the system guarantees that capital is only deployed when the quantitative odds are overwhelmingly in our favor.

</details>