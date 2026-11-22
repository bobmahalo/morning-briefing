> **Credit-section correction — November 11, 2026 (installed locally):** Legacy bond snapshots contain unverified prototype observations and are withheld by the executive renderer. They are not live TRACE evidence. YTM and Treasury spread remain explicitly unavailable pending a validated data adapter. Unknown or invalid debt is not zero debt; a zero input does not certify filing completeness. Net cash does not establish zero bankruptcy risk. A simple maturity-matched Treasury spread is not OAS. Transcript prices/yields are unverified claims, sponsor ownership is not a debt guarantee, and expected-move estimates do not establish a near-certain 25% move or touching both barriers. Credit stress warrants investigation, not automatic trades. This notice supersedes conflicting historical examples below. Historical display remains pending operator discussion. Existing generated reports and public pages have not been refreshed.

# 🎓 The Antigravity SSR v2 Executive Engine: Master Architecture & Forensic Curriculum
**Document:** Institutional Single-Stock Operating Manual & Forensic Companion  
**System:** Antigravity V3 Core — Second-Rail Executive Single Stock Engine (`SSR v2`)  
**Primary Modules:** `reporting/ssr_executive.py` | `run_ssr_v2.py` | `reporting/ssr_report.py`  
**Methodology:** Deterministic Quantitative Rules | Adversarial XBRL Accounting | 3-Tranche Limit Order Execution  

[☕ Daily Morning Briefing](https://bobmahalo.github.io/morning-briefing/) | [📈 $100K Model Portfolio](https://bobmahalo.github.io/morning-briefing/PORTFOLIO.html) | [🗄️ Open SEC Data Lake](https://bobmahalo.github.io/morning-briefing/DATA_LAKE.html) | [🏛️ S&P 1500 Screen](https://bobmahalo.github.io/morning-briefing/SP1500_SCREEN.html) | [🎓 Master Curriculum](https://bobmahalo.github.io/morning-briefing/CURRICULUM.html) | [🔬 SSR Executive Curriculum](https://bobmahalo.github.io/morning-briefing/SSR_CURRICULUM.html) | [🗂️ Single Stock Directory](https://bobmahalo.github.io/Single-Stock-Scan/)

> **🏛️ True Stock Ownership & Custody Education:** Holding shares in broker "Street Name" means you only hold a beneficial entitlement while Cede & Co. holds legal title. Learn how Direct Registration (DRS) protects your shares from broker insolvency and short-lending at **[WhyDRS.org](https://www.whydrs.org)** ([Advocacy](https://www.whydrs.org/advocacy) | [Free Resources](https://www.whydrs.org/free-resources)).

> **Disclaimer:** *This curriculum is for educational and quantitative research purposes only and does not constitute financial advice. The author is not a licensed financial advisor. All investments carry risk, and you should conduct your own due diligence before making any financial decisions.*

---

## 🏛️ Executive Philosophy: The Inverted Pyramid of Forensic Truth
> *"Rule No. 1: Never lose money. Rule No. 2: Never forget Rule No. 1."* — Warren Buffett  
> *"All I want to know is where I'm going to die, so I'll never go there."* — Charlie Munger

Wall Street equity research is designed to sell stories: analysts project 10-year revenue growth into the stratosphere, apply arbitrary terminal multiples, and bury balance-sheet decay in footnotes.

The **Antigravity SSR v2 Executive Card** inverts that process. It ingests raw SEC EDGAR XBRL filings (`10-K`, `10-Q`), insider `Form 4` transactions, and `10-K Item 5` transfer-agent shareholder records, and structures the output into a **3-Level Inverted Pyramid**:

```
                     ANTIGRAVITY SSR v2 ARCHITECTURE
┌─────────────────────────────────────────────────────────────────────────┐
│ LEVEL 1: THE 10-SECOND DECISION CARD                                    │
│ • Shaded Archetype Pill Badge (Compounder / Net-Net / Turnaround / Trap)│
│ • Asymmetric Payoff Box (Rx : 1.0 Reward-to-Risk vs. Asset Floor)       │
│ • 3-Pillar Convergence Factor Card (Health, Asymmetry, Discipline 0-10) │
│ • Margin of Safety Floor Table (Net Cash, NCAV, TBV, Zero-Growth DCF)   │
│ • Deterministic 3-Tranche Limit Order Ladder & Valuation Exits          │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ LEVEL 2: THE 30-SECOND PLUMBER'S DIAGNOSIS                              │
│ • Section 1: Cash Flow Engine (Structural Profits vs. Destocking Mirage)│
│ • Section 2: Balance Sheet Health & Debt Extinguishment Clock           │
│ • Section 3: 5-Year Cumulative Capital Allocation & Cannibal Ledger     │
│ • Section 4: 5-Year Historical Valuation Corridor & Mean Reversion      │
│ • Section 5: SIC Industry Peer Benchmarking (Top 3 Competitors)         │
│ • Section 6: Smart Money (Form 4 Cluster Buys & 10-K Item 5 DRS Census) │
│ • Section 7: Volume & Social Quiet (Silent Accumulation Zone)           │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ LEVEL 3: COMPLETE SEC EDGAR FINANCIAL STATEMENTS & AUDIT VAULT          │
│ • Collapsible 10-Section Forensic Proof Vault (20Y Annual + 6Q Discrete)│
│ • Common-Size Statements, ROIC/ROCE Trough Consistency, Roll-Up Audit   │
│ • Roaring Kitty Inverted Yields, Synthetic Deleveraging & Reverse DCF   │
│ • Line-by-Line SEC XBRL Tag & Accession Number Provenance Appendix      │
└─────────────────────────────────────────────────────────────────────────┘
```

---

# MODULE 1: Level 1 — The 10-Second Decision Card

Level 1 is engineered so you can tell within **10 seconds** whether a stock is a compounding machine, a deep liquidation bargain, or an accounting trap—and exactly where to place your limit orders if it passes.

---

## 1. The 4 Investment Archetypes & Deterministic Classification (`_classify_archetype`)

Every stock is classified through a strict **top-down veto cascade** (`reporting/ssr_executive.py`). A company is tested against the trap gate *first* before it can ever qualify for a bullish archetype:

```
                      ARCHETYPE CLASSIFICATION CASCADE
             ┌────────────────────────────────────────────────┐
             │ Gate 0: Regulatory & SEC Audit Red Flag        │
             │ (NT 10-K/Q Late Filing, 8-K 4.02, Delisting)?  │
             └───────┬────────────────────────────────┬───────┘
                 YES │                                │ NO
                     ▼                                ▼
          🔴 TIER_QUARANTINED        ┌────────────────────────────────┐
          (Capped <= 1.0% Risk)      │ Gate 1: Accounting Mirage      │
                                     │ (Beneish M > -1.78 OR WC Liq)? │
                                     └───────┬────────────────┬───────┘
                                         YES │                │ NO
                                             ▼                ▼
                                  🔴 TIER_QUARANTINED ┌──────────────────────────────┐
                                                      │ Gate 2: P <= 0.67 * NCAV     │
                                                      │ (Graham 33% Margin Safety)?  │
                                                      └──────┬───────────────┬───────┘
                                                         YES │               │ NO
                                                             ▼               ▼
                                                  🟡 TIER_2_NET_NETS ┌──────────────────────────────┐
                                                  (5% Sleeve | 1% Tgt│ Gate 3: Altman Z < 1.81      │
                                                                     │ (Operating Distress Trap)?   │
                                                                     └──────┬───────────────┬───────┘
                                                                        YES │               │ NO
                                                                            ▼               ▼
                                                                 🔴 TIER_QUARANTINED ┌──────────────────────────────┐
                                                                                     │ Gate 4: Compounder vs Cash   │
                                                                                     │ Cow (Piot>=7, FCF Yield>=10%,│
                                                                                     │ SBC Yield>=5%, Structural)?  │
                                                                                     └──────┬───────────────┬───────┘
                                                                                        YES │               │ NO
                                                                                            │               ▼
                                                                                            │      ┌──────────────────────────────┐
                                                                                            │      │ Gate 5: Turnaround/Activist  │
                                                                                            │      │ (FCF >= 8% or Cluster Buy)?  │
                                                                                            │      └──────┬───────────────┬───────┘
                                                                                            │         YES │               │ NO
                                                                                            │             ▼               ▼
                                                                                            │  🔵 TIER_3_TURNAROUNDS  ⚪ TIER_UNSUITABLE_PASS
                                                                                            │  (20% Sleeve|2.8% Tgt) (0% Allocation / PASS)
                                                                                            ▼
                                                                             ┌──────────────────────────────┐
                                                                             │ ROIC >= 15% AND Reinvest > 0?│
                                                                             └──────┬───────────────┬───────┘
                                                                                YES │               │ NO
                                                                                    ▼               ▼
                                                                    🟢 TIER_1_COMPOUNDERS  🪙 TIER_DEEP_VALUE_CASH_COW
                                                                    (65% Sleeve | 5.5% Tgt)(3.5% Target / 5.0% Cap)
```

### Portfolio Sleeve & Per-Ticker Risk Budgeting (`strategies/position_sizing_and_execution.py`)

| Archetype Badge | Tier Key | Sleeve Target | Per-Stock Target ($100k Book) | Hard Risk Ceiling | Economic Rationale & Time Horizon |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **🟢 CORE STRUCTURAL OPERATING COMPOUNDER** | `TIER_1_COMPOUNDERS` | `65.0%` | `5.5%` (`$5,500`) | `7.0%` | Cash comes from genuine operating margins, 3-year median ROIC ≥ 15%, positive reinvestment, net cash, and share buybacks. **Time is your ally.** |
| **🪙 CASH COW / DEEP VALUE PLAY** | `TIER_DEEP_VALUE_CASH_COW` | `7.0%` | `3.5%` (`$3,500`) | `5.0%` | High FCF yield (≥ 10.0%) and structural profits, but mature operations with lower ROIC (< 15%) or limited reinvestment. Held for multiple mean reversion. |
| **🔵 MICRO-TURNAROUND & VALUE CATALYST** | `TIER_3_TURNAROUNDS` | `20.0%` | `2.8%` (`$2,800`) | `3.5%` | Beaten-down cyclical or turnaround with ≥ 8% FCF yield or verified C-Suite Form 4 cluster buying. |
| **🟡 BENJAMIN GRAHAM NET-NET ARBITRAGE** | `TIER_2_NET_NETS` | `5.0%` | `1.0%` (`$1,000`) | `1.5%` | Classic *cigar butt* trading at a strict 33% discount to Net Current Asset Value (Price ≤ 0.67 × NCAV). Because operations may be shrinking, **time is your enemy**—diversify in small 1% positions and sell at NCAV/TBV re-rating. |
| **🔴 QUARANTINED / ACCOUNTING MIRAGE RISK** | `TIER_QUARANTINED` | `0%` (Excluded) | `≤ 1.0%` (`≤ $1,000`) | `1.0%` | Triggered by SEC regulatory red flags (NT filings, 8-K restatements), accounting manipulation (M > -1.78), material working capital liquidation (> 20% of OCF), or operational insolvency (Z < 1.81). |
| **⚪ UNSUITABLE / PASS** | `TIER_UNSUITABLE_PASS` | `0%` | `$0.00` (`0.0%`) | `0.0%` | Fails minimum liquidation floor, structural earnings power, or return-on-capital hurdle criteria. Zero allocation; capital preserved in Treasury T-Bills. |
| **💵 U.S. T-BILLS / DRY POWDER FLOOR** | `CASH_RESERVE` | `10.0%+` | Baseline + Unfilled Sleeve | `100.0%` | Under **Tobin's Separation Theorem**, any unfilled sleeve capital remains in U.S. T-Bills rather than over-concentrating surviving picks. |

---

## 2. The Asymmetric Payoff Profile Box (Rx : 1.0 Expectancy)

Right below the archetype pill sits the monospaced **Asymmetric Payoff Profile Box** *(Illustrative Arithmetic Example)*:

```text
┌──────────────────────────────────────────────────────────────────────────────┐
│                 VERDICT: CORE STRUCTURAL OPERATING COMPOUNDER                │
├──────────────────────────────────────────────────────────────────────────────┤
│ ASYMMETRIC PAYOFF PROFILE: 1.6x : 1.0 (Moderate Asymmetry)*                  │
│ • Downside to Net Cash Floor:        -18.2% ($22.50 vs $27.50)*              │
│ • Upside to Intrinsic Fair Value:    +30.0% ($35.75 Target 1)                │
│ • Catalytic Convergence Target:      +65.0% ($45.38 Target 2)                │
└──────────────────────────────────────────────────────────────────────────────┘
```

### A. How the Fundamental Downside Floor (F_down) Is Selected
The engine never invents arbitrary technical support levels. It selects the highest-priority **positive balance-sheet or cash-flow backstop** in this exact order:
1. **Net Cash Floor:** `(Total Cash - Total Debt) / Diluted Shares` *(Pure bank cash minus verified total debt, fully incorporating ASC 842 operating lease liabilities and convertible notes; fails closed if debt tags are unpopulated)*
2. **Graham NCAV Floor:** `(Current Assets - Total Liabilities - Preferred Stock) / Diluted Shares` *(Strict liquidation value)*
3. **Tangible Book Floor:** `(Total Equity - Goodwill - Intangibles) / Diluted Shares` *(Tangible physical net worth)*
4. **Zero-Growth DCF Benchmark:** `(TTM FCF / 0.10) / Diluted Shares` *(Perpetuity intrinsic value assuming 0% future growth at a 10% discount rate; if spot price trades at or below DCF benchmark, it is labeled **DCF Parity** rather than an artificial cash cushion)*
5. **No Structural Balance-Sheet Floor (`N/A — Franchise Operating Moat`):** Triggered when a high-ROIC compounder carries net debt and negative tangible equity due to decades of share buybacks (e.g., AutoZone/Domino's model).

### B. The Reward-to-Risk Formula (Rx : 1.0)
$$\text{Downside \%} = \left( \frac{F_{\text{down}} - P_{\text{spot}}}{P_{\text{spot}}} \right) \times 100$$
$$\text{Target 1 Upside \%} = \left( \frac{P_{\text{Target 1}} - P_{\text{spot}}}{P_{\text{spot}}} \right) \times 100$$
$$\text{Asymmetry Ratio } (R\text{x}) = \frac{\text{Target 1 Upside \%}}{|\text{Downside \%}|}$$

* **💎 High Asymmetry (≥ 2.5x : 1.0):** Upside to conservative Target 1 is at least 2.5× the distance to the structural liquidation benchmark.
* **⚖️ Moderate Asymmetry (1.0x – 2.5x : 1.0):** Positive mathematical expectancy; requires strict 3-tranche sizing discipline.
* **⚠️ Unfavorable Skew (< 1.0x : 1.0):** Downside to structural asset floor exceeds upside to Target 1.
* **🚨 Pure Cash Arbitrage Cushion (Downside % ≥ 0%):** When spot price trades *below* the Net Cash or NCAV floor (F_down ≥ Spot Price), the ratio prints `>10.0x : 1.0` and automatically triggers an inline **Audit Check**:
  > `• AUDIT CHECK: Spot < Cash Floor. Verify debt & burn in Vault before sizing.`
  *(Why? Because in micro-caps, a stock trading below net cash is either a rare net-net anomaly or an unpopulated XBRL debt tag that must be verified in Level 3 before risking a dollar).*

---

## 3. The 3-Pillar Convergence Factor Card (`models/convergence_radar.py`)

> **Governing Architectural Principle (Task 4.3):**  
> Convergence Scores (0–10) serve strictly as a non-parametric rank-ordering filter to prioritize candidates within an archetype hunting sleeve when eligible candidates exceed sleeve capacity. Convergence Scores **must never** be used as an arbitrary position sizing scalar (e.g., allocating more capital to a 9/10 score than a 7/10 score). Position sizing is governed strictly by the Archetype Risk Budget (5.5% target / 7.0% hard cap for Compounders, 2.8% / 3.5% for Turnarounds, 1.0% / 1.5% for Net-Nets) calibrated against 30-day ADDV liquidity limits (1%–2%) and GICS sector concentration caps (20.0%), adhering to Tobin's Separation Theorem.

The 3-Pillar Convergence Card condenses 10 forensic dimensions into three 0–10 visual meters (`🟩` for 7–10, `🟨` for 4–6, `🟥` for 0–3):

### Pillar 1: 🛡️ Financial Health (0 to 10 Points)
Tests whether the balance sheet is solvent and the accounting is honest:
$$\text{Health Score} = \text{round}\Big( \underbrace{\frac{\text{Piotroski}}{9} \times 5.0}_{\text{Max } 5.0\text{ pts}} + \underbrace{\text{Altman Pts}}_{\text{Max } 3.0\text{ pts}} + \underbrace{\text{Beneish Pts}}_{\text{Max } 2.0\text{ pts}} \Big)$$

| Component | Max Points | Exact Scoring Rule |
| :--- | :---: | :--- |
| **Piotroski F-Score (0–9)** | `5.0 pts` | Proportional: (F / 9) × 5.0 (e.g., 8/9 = 4.44 pts; 9/9 = 5.0 pts). |
| **Altman Z-Score** | `3.0 pts` | `3.0 pts` if Z ≥ 3.0 (Safe Zone)<br>`1.5 pts` if 1.81 ≤ Z < 3.0 (Grey Zone)<br>`0.0 pts` if Z < 1.81 (Bankruptcy Distress Zone) |
| **Beneish M-Score** | `2.0 pts` | `2.0 pts` if M ≤ -1.78 (Clean Accruals)<br>`0.0 pts` if M > -1.78 (Earnings Manipulation Alert) |

* **⚠️ Bank / REIT Exception Gate (`is_financial_or_reit`):** If the company's SEC SIC code falls in Banking, Insurance, or Real Estate (`SIC 6000–6799`), standard manufacturing working-capital and leverage ratios (Z-Score and Piotroski) produce false distress signals. The card explicitly flags `⚠️ N/A (Bank/REIT Structure)*` so you never misapply industrial debt formulas to a depository bank.

### Pillar 2: 💎 Valuation Asymmetry (0 to 10 Points)
Tests how much cash flow and liquid asset backing you receive per dollar paid:
$$\text{Valuation Score} = \text{FCF Yield Pts (0–4)} + \text{Net Cash/Price Pts (0–3)} + \text{NCAV/Price Pts (0–3)}$$

| Component | Max Points | Exact Scoring Tiers |
| :--- | :---: | :--- |
| **TTM FCF Yield (FCF / Market Cap)** | `4.0 pts` | ≥ 20.0% → **4 pts**<br>12.0%–19.9% → **3 pts**<br>8.0%–11.9% → **2 pts**<br>4.0%–7.9% → **1 pt**<br>< 4.0% → **0 pts** |
| **Net Cash / Share Price** | `3.0 pts` | ≥ 50.0% → **3 pts**<br>25.0%–49.9% → **2 pts**<br>10.0%–24.9% → **1 pt**<br>≤ 0% (Net Debt) → **0 pts** |
| **Graham NCAV / Share Price** | `3.0 pts` | P ≤ 0.67 × NCAV (Graham 33% Haircut) → **3 pts**<br>100.0%–149.2% of Price → **2.5 pts**<br>70.0%–99.9% → **2 pts**<br>40.0%–69.9% → **1 pt** |

### Pillar 3: 🏛️ Capital Discipline (0 to 10 Points)
Tests whether management treats shareholders as partners or as an ATM:
$$\text{Discipline Score} = \text{Share Change Pts (0–4)} + \text{Insider Cluster Pts (1–4)} + \text{Capex Maintenance Pts (0–2)}$$

| Component | Max Points | Exact Scoring Tiers |
| :--- | :---: | :--- |
| **1-Year Share Count Change** | `4.0 pts` | ≤ -5.0% (Aggressive Cannibal) → **4 pts**<br>-1.0% to -4.9% (Buybacks) → **3 pts**<br>-0.9% to +1.0% (Stable) → **2 pts**<br>> +1.0% (Dilution) → **0 pts**<br>`None` → `0 pts` (`Share Change NR`) |
| **C-Suite Form 4 Cluster Buying** | `4.0 pts` | `4.0 pts` if verified C-Suite open-market cluster buying (`Code P`)<br>`1.0 pt` baseline if verified quiet (`False`)<br>`0.0 pts` (`Insider Data NR`) when `None` |
| **Maintenance Capex Health** | `2.0 pts` | `2.0 pts` if CapEx / D&A ≥ 0.35<br>`0.0 pts` if Capex Starvation detected (`True`) or `Capex NR` (`None`) |

* **Fail-Closed Zero-Midpoint Rule (`models/convergence_radar.py`):** Unpopulated metrics across all three pillars (`Piotroski`, `Altman Z`, `Beneish M`, `FCF Yield`, `Share Change`, `CapEx/D&A`, `Insider Data`, or unavailable `Share Price`) contribute **`0` points** and emit explicit `... NR` detail labels rather than fabricating synthetic neutral midpoints. Missing Form 4 insider net flow likewise renders `NR / Unavailable` instead of `$0`.
* **⚠️ Dilutive Burn Trap Catch (`is_dilutive_burn`):** If a company has negative or zero Operating Cash Flow (OCF ≤ $0) while issuing positive Stock-Based Compensation (SBC > $0), dividing SBC by negative OCF produces a meaningless negative percentage. The engine catches this and prints **`⚠️ Dilutive Burn (OCF ≤ $0)*`**—exposing that management is paying themselves in stock while the business burns cash.

---

## 4. Deterministic 3-Tranche Limit Order Ladder & Valuation Exits

### A. The 3-Tranche Accumulation Ladder (`build_3_tranche_ladder`)
Avoid market-buying 100% of an allocation on day one. Every position is split into three mathematical tranches with a **maximum 1 tranche fill per trading day** and **`T2`/`T3` limit targets re-anchored proportionally to the actual `T1` fill price**:

| Tranche | Order Type | Entry Price Formula | Weight | Tactical Purpose |
| :---: | :---: | :---: | :---: | :--- |
| **T1** | `MARKET / LIMIT` | Spot Price | `33.3%` | **Baseline Entry:** Establishes immediate exposure once the forensic audit passes and sets the entry anchor for `T2`/`T3`. |
| **T2** | `GTC LIMIT` | `T1_Fill × (1 - Discount_retest)` | `33.3%` | **Support Retest Bid:** Scaled dynamically to 1.0× ATR or 30-day Implied Volatility (minimum -6.0% baseline default), eligible on Day 2+ after `T1`. |
| **T3** | `GTC LIMIT` | `T1_Fill × (1 - Discount_flush)` | `33.4%` | **Capitulation Wick Bid:** Scaled dynamically to 2.0× ATR or 30-day Implied Volatility (minimum -12.5% baseline default), eligible on Day 3+ after `T2`. |

* **Full-Fill Blended Cost Basis (VWAP):** Computed strictly from integer-share planned/filled cost so small allocations on high-priced equities cannot inflate VWAP above spot via fractional-share truncation:
  $$\text{VWAP}_{\text{ladder}} = \frac{\sum (\text{Target Shares}_i \times \text{Target Price}_i)}{\sum \text{Target Shares}_i}$$

### B. Archetype-Specific Deterministic Exit Rules (`build_deterministic_exit_rules`)
Exit targets adapt dynamically to the stock's archetype so you don't hold a decaying Net-Net like a Compounder:
1. **For Graham Net-Nets (`TIER_2_NET_NETS`):**
   * **Target 1 (Sell 50%):** 100% of **Graham NCAV** (or +35.0% minimum re-rating fallback).
   * **Target 2 (Sell 50%):** 100% of **Tangible Book Value (TBV)** (or +65.0% re-rating fallback).
   * **Hard Stop:** -20.0% anchored to blended VWAP. Immediate exit if quarterly operational burn erodes > 20% of Net Current Assets.
   * **Catastrophic Stop:** Non-negotiable liquidation at -25.0% from VWAP.
2. **For Compounders (`TIER_1_COMPOUNDERS` — Formula-Driven Anchors, Zero Hardcoded Targets):**
   * **Target 1 (Scale 50%):** Formula-anchored to the **10.0% Ex-Cash FCF Yield boundary**:
     $$P_{\text{Target 1}} = \frac{\text{FCF}_{\text{TTM/Sh}}}{0.10} + \max(0, \text{Net Cash/Sh})$$
     *(Note: `+30.0%` fair-value re-rating serves strictly as an unverified fallback).*
   * **Target 2 (Scale remaining 50%):** Formula-anchored to the **8.0% FCF Yield exit trigger or Zero-Growth Intrinsic Value**:
     $$P_{\text{Target 2}} = \max\left(P_{\text{Zero-Growth DCF}},\; \frac{\text{FCF}_{\text{TTM/Sh}}}{0.08} + \max(0, \text{Net Cash/Sh})\right)$$
     *(Note: `+65.0%` zero-growth convergence serves strictly as an unverified fallback).*
   * **Trailing FCF Hold:** Maintain remainder as long as TTM FCF Yield ≥ 10.0% and shares decline; exit if FCF yield < 8.0%.
   * **Safety Stop Loss:** -15.0% anchored strictly to blended VWAP.
   * **Catastrophic Stop:** Non-negotiable immediate market liquidation at -25.0% from VWAP, strictly overriding any delay for quarterly SEC filings.
3. **For Turnarounds (`TIER_3_TURNAROUNDS`):**
   * **Target 1 (Scale 50%):** Tangible Asset / C-Suite Turnaround Target (**+35.0%**).
   * **Target 2 (Full Exit 50%):** Catalyst Exuberance Target (**+75.0%**).
   * **Safety Stop Loss:** -20.0% anchored strictly to blended VWAP.
   * **Catastrophic Stop:** Non-negotiable liquidation at -25.0% from VWAP.
4. **For Cash Cows / Deep Value (`TIER_DEEP_VALUE_CASH_COW`):**
   * **Target 1 (Scale 50%):** Cash Multiple Re-Rating Target (**+25.0%**).
   * **Target 2 (Scale 50%):** Full Historical Valuation Exit (**+50.0%**).
   * **Safety Stop Loss:** -15.0% anchored strictly to blended VWAP.
5. **Universal Elevated Volume Exit Trigger:**
   * If 30-day volume surges to **≥ 3.0× normal ADDV** while price reaches historical valuation corridor upper bounds, scale 33%–50% directly into elevated market liquidity.
6. **The Strength vs. Weakness Exit Asymmetry (Mean-Reversion Integrity):**
   * **The Empirical Reality:** Quantitative testing across 17,700+ equities and 152 exit rules demonstrates that selling single stocks on technical weakness (e.g., 200-day moving average breakdowns, 20-day lows, Donchian channel breaks) generates an average **`-0.34%` drag per trade** across 7 of 9 operating years due to short-term single-stock mean reversion. Conversely, scaling into technical and valuation strength captures **`+0.38%` excess return per trade**.
   * **The Rule:** Single-stock exits are governed strictly by deterministic valuation targets ($P_{\text{T1}}$ and $P_{\text{T2}}$) and the structural thesis stop loss. **Never exit fundamental operating survivors based on technical moving average breakdowns in isolation.** Moving average breakdowns are reserved strictly as macro regime gates on broad market indexes (`VOO`/`SPY`) when confirmed by the **Three Credit Tripwires** (`VIX > 23`, `HYG < $76`, `10Y > 5.24%`).

---

# MODULE 2: Level 2 — The 30-Second Plumber's Diagnosis

If a stock survives Level 1, Level 2 takes **30 seconds** to inspect the internal corporate plumbing across 7 forensic sections.

> **⚡ Kramdown Tabular Dropdown Architecture:**  
> All 7 Level 2 diagnostic sections feature collapsed-by-default `<details markdown="1">` drawers containing clean Markdown tables (`| :--- |`). This keeps the 10-Second Decision Card in Level 1 instantly actionable without visual clutter, while allowing institutional allocators to inspect 5-year capital allocation ledgers, historical valuation corridors, contractual debt maturity schedules, secondary bond tapes, and insider Form 4 transaction receipts with a single click.

---

## Section 1: The Cash Flow Engine (`models/working_capital_audit.py`)

### Why Free Cash Flow Can Lie
Reported Operating Cash Flow (OCF) equals Net Income plus non-cash charges (D&A, SBC) plus **Working Capital changes**:
$$\text{OCF} = \text{Net Income} + \text{D\&A} + \text{SBC} + \underbrace{(-\Delta\text{A/R}) + (-\Delta\text{Inventory}) + (+\Delta\text{A/P}) + (+\Delta\text{Deferred Revenue})}_{\text{Total Working Capital Cash Impact } (\Delta\text{WC}_{\text{cash}})}$$

A shrinking retailer can lose money on every sale (Operating Income < 0), close stores, liquidate inventory, stretch supplier payables, and report a massive one-time spike in "Free Cash Flow."

### The 5 Deterministic Cash Origin Classifications

| Classification | Mathematical Trigger | Forensic Meaning |
| :--- | :--- | :--- |
| **`STRUCTURAL_OPERATING_EARNINGS`** | $\text{OCF} > 0, \text{EBIT} > 0$ **AND** $\Delta\text{WC}_{\text{cash}} < 0.50 \times \text{OCF}$ | **True Compounder Engine:** Cash flow is generated by profitable customer sales, not balance-sheet liquidation. Non-cash goodwill/intangibles impairment write-downs that cause Net Income ≤ 0 while EBIT > 0 and OCF > 0 are explicitly excluded from distress triggers. |
| **`MIXED_EARNINGS_AND_WORKING_CAPITAL`** | $\text{OCF} > 0, \text{EBIT} > 0, \text{NI} > 0$ **AND** $\Delta\text{WC}_{\text{cash}} \ge 0.50 \times \text{OCF}$ | Core operations are profitable, but more than half of trailing cash flow came from temporary working capital release. |
| **`WORKING_CAPITAL_LIQUIDATION`** | $\text{OCF} > 0$ **WHILE** $\text{EBIT} \le 0$ **AND** $\Delta\text{WC}_{\text{cash}} > 0.20 \times \text{OCF}$ | **🚨 The Liquidation Mirage Trap:** The business is operating at a loss; positive cash flow is driven by material working capital runoff (> 20% of OCF: destocking inventory, collecting receivables, or stretching payables). Automatically triggers `TIER_QUARANTINED`. Immaterial WC runoff (≤ 20%) does not trigger distress. |
| **`DEPRECIATION_SHIELD_CASH_FLOW`** | $\text{OCF} > 0$ **WHILE** ($\text{EBIT} \le 0$ or $\text{NI} \le 0$) **AND** $\Delta\text{WC}_{\text{cash}} \le 0$ | GAAP earnings are negative due to heavy non-cash depreciation/amortization charges, keeping cash flow positive. |
| **`OPERATING_CASH_BURN`** | $\text{OCF} \le 0$ | Active cash drain from core operations. |

### The Maintenance Capex Starvation Check
$$\text{Capex-to-D\&A Ratio} = \frac{|\text{Capital Expenditures}|}{\text{Depreciation \& Amortization}}$$
* **Gate:** If $|\text{CapEx}| / \text{D\&A} < 0.35$, the engine flags **`⚠️ WARNING: Capex starved under 35% of D&A`**. Management is cannibalizing physical plant and equipment to artificially inflate short-term Free Cash Flow.
* **Fail-Closed & 1-Fiscal-Year Recency Cap:** When canonical `OCF`, `EBIT`, `CapEx`, or `D&A` is missing—or when the latest annual fact exceeds the `1`-fiscal-year recency cap—both cash origin classification (`UNAVAILABLE`) and CapEx starvation (`None` / `Unknown`) fail closed. Missing `CapEx` is never coerced to `$0.0` to trigger a false starvation warning, and missing shares are never defaulted to `1.0`.

---

## Section 2: Balance Sheet Health & Debt Extinguishment Clock (`models/valuation.py` & `models/debt_maturity.py`)

Instead of relying on static debt-to-equity ratios, the engine models **Synthetic Deleveraging** and **Contractual Maturity Walls**:
1. **Excess Cash Application:** First, apply 100% of balance-sheet cash and short-term investments against total short- and long-term debt:
   $$\text{Remaining Net Debt} = \max(0, \text{Total Debt} - \text{Total Cash})$$
2. **The Debt Extinguishment Clock:** How many years of current Trailing Twelve Month Free Cash Flow would it take to retire 100% of remaining net debt?
   $$\text{Debt Extinguishment Clock (Years)} = \frac{\text{Remaining Net Debt}}{\text{TTM Free Cash Flow}}$$
   * **0.0 Years (Net Cash Surplus):** Reported cash exceeds reported debt; liquidity availability, off-balance-sheet commitments, and subsidiary debt structure still require review (net cash does not establish zero default risk).
   * **≤ 3.0 Years:** Rapid deleveraging capacity; interest-rate shock resistant.
   * **> 5.0 Years (or Infinite when FCF ≤ 0):** High refinancing and credit-spread vulnerability.
3. **The 12–24 Month+ Contractual Debt Maturity Wall & Revolver Headroom (`models/debt_maturity.py`):**
   Static debt ratios ignore *when* principal payments must be made. The engine extracts contractual debt maturity schedules from the latest qualifying `10-K`, `10-K/A`, `10-Q`, or `10-Q/A` footnote disclosure anchored strictly to a **single filing snapshot** (preventing outer buckets such as Year 5 from leaking across shifted fiscal periods). Rolling 12-month tags (`InNextRollingTwelveMonths` + `InRollingYearTwo`) form an exact 24M window, whereas fiscal-calendar `10-Q` disclosures sum `RemainderOfFiscalYear` + `Year 1 (FY+1)` + `Year 2 (FY+2)` across the exact covered horizon (`24M + months remaining in FY`):
   $$\text{Near-Term Debt Wall}_{\text{Fiscal}} = \text{Remainder of FY} + \text{FY}_{+1} \text{ Principal Due} + \text{FY}_{+2} \text{ Principal Due}$$
   This maturity wall is stressed against liquid cash reserves and 2-year cumulative organic FCF capacity (while undrawn revolving credit capacity from `LineOfCreditFacilityRemainingBorrowingCapacity` is reported separately and **never** folded into cash coverage ratios):
   $$\text{Total 24M Internal Liquidity} = \text{Cash} + (2 \times \max(0, \text{Annual FCF}))$$
   * **`NO_DEBT_RISK`:** Zero funded debt obligations.
   * **`FULLY_COVERED_BY_CASH`:** Available cash alone covers ≥ 100% of near-term maturities.
   * **`COVERED_BY_ORGANIC_FCF`:** Cash + 2-year FCF capacity covers ≥ 100% of near-term maturities.
   * **`REFINANCING_DEPENDENCY_WARNING`:** Positive FCF, but internal liquidity leaves a deficit against maturities. Company must refinance or roll credit facilities.
   * **`ACUTE_MATURITY_WALL_DISTRESS`:** Negative FCF / cash burn with debt maturities exceeding liquid cash reserves. High risk of distress or dilution.
   * **Primary iXBRL Context Reconciliation (`ingestion/stock_vault.py`, `run_ssr_v2.py`):** `ensure_periodic_filing_htmls()` caches the latest `10-K` and `10-Q` primary `.htm` filings under `dossier/filings/` so `normalize_xbrl_facts()` runs `filing_context_validator` balance-sheet and income-statement checks (recovering current/noncurrent debt components such as `ShortTermBorrowings`, `LongTermDebtCurrent`, `LongTermDebtAndCapitalLeaseObligations`, and `InterestExpenseDebt` without unsafe blanket YAML aliases).
4. **Secondary Corporate Bond Market Intelligence, Macro Credit Context & Credit Containment (`scripts/test_bond_pull.py` [RETIRED] & `data_lake/bonds/`):**
   Contractual SEC 10-K/10-Q footnote schedules tell us what management *owes*; broad U.S. Treasury (`1M`–`30Y`) and FRED ICE BofA credit-tier curves (`AAA`–`CCC` Effective Yields and OAS from `ingestion/macro_vitals.py`) provide macro regime borrowing context explicitly distinct from issuer-specific secondary quotes. Pending a sourced, observation-level bond adapter, **`scripts/test_bond_pull.py` is disabled**, legacy unvalidated `data_lake/bonds/` snapshots are withheld (`N/A`), and no credit monitoring verdict is assigned by the executive renderer:
   * **Weighted Yield-to-Maturity (YTM, in percent):**
     $$\text{Weighted YTM (\%)} = \sum_{i=1}^{N} \left( \frac{\text{Principal}_i}{\sum \text{Principal}} \times \text{YTM}_i \right)$$
   * **Simple Maturity-Matched Treasury Spread (bps over Treasuries — NOT OAS):**
     $$\text{Treasury Spread (bps)} = \left(\text{Bond YTM (\%)} - \text{Maturity-Matched Treasury Yield (\%)}\right) \times 100$$
     *(Callable, make-whole, and convertible issues require separate option-adjusted handling and are not equivalent to a simple bullet Treasury spread.)*
   * **Duration vs. Credit Stress Concept (Requires Validated Adapter Output):**
     Once populated from verified execution observations (with issuer/CUSIP identity, call schedule, trade timestamp, and settlement date), tight spreads with investment-grade ratings reflect rate-duration discounting rather than distress, whereas deep discounts paired with wide spreads indicate bondholder restructuring expectations.
   * **Missing or Zero Debt Input Handling:**
     Missing or invalid debt is **never** treated as zero debt (`Debt data unavailable or invalid; absence of debt is not established.`). A zero upstream debt input emits `Reported debt input is zero; filing coverage is not verified.` and still requires primary filing verification rather than claiming zero default risk.

---

## Section 3: 5-Year Cumulative Capital Allocation & Share Cannibalization

Single-year cash flows are noisy. Section 3 sums **5 full fiscal years of Operating Cash Flow (5-Year OCF)** and tracks every dollar management spent across five buckets:

$$\sum \text{OCF}_{5\text{Y}} = \text{CapEx}_{5\text{Y}} + \text{Buybacks}_{5\text{Y}} + \text{Dividends}_{5\text{Y}} + \text{Acquisitions}_{5\text{Y}} + \text{Retained Surplus}_{5\text{Y}}$$

### The 5 Capital Allocation Postures
* **💰 Cannibal & Cash Return Engine:** (Buybacks_5Y + Dividends_5Y) / OCF_5Y ≥ 50.0%. Management returns the majority of organic cash flow directly to owners.
* **🏰 Organic Fortress Builder:** Retained Surplus_5Y / OCF_5Y ≥ 40.0%. Management stockpiles cash on the balance sheet and pays down debt.
* **⚙️ Heavy Capital Reinvestment:** CapEx_5Y / OCF_5Y ≥ 50.0%. Heavy physical reinvestment into factories, fleet, or infrastructure.
* **⚖️ Balanced Capital Deployment:** Balanced split across CapEx, buybacks/dividends, and balance-sheet retention.
* **⚠️ Dilutive Cash Burn:** 5-Year Cumulative OCF verified `≤ 0`. Operations are cash-flow negative and subsidized by selling new stock (Equity Issuance) or borrowing (Net Debt Flow).
* **`NR` (Unpopulated Multi-Year OCF):** When cumulative 5-year Operating Cash Flow is missing (`None`), the posture renders `NR` instead of defaulting to `$0` / `Dilutive Cash Burn`, and unpopulated cash-flow buckets render `N/A`.

---

## Section 4: 5-Year Historical Valuation Corridor & Multiple Mean Reversion (`models/valuation_corridor.py`)

Rather than guessing what a stock's P/E "should" be using theoretical formulas, Section 4 maps where the stock trades today against **its own verified 5-year weekly empirical history** (`ingestion/price_history.py`, up to `260 weekly candles`). When live or non-synthetic cached weekly candles are unavailable (or when only synthetic fallback baselines exist), derived corridor metrics are **explicitly withheld (`N/A` — Price History Unavailable)** and never fabricated:

1. **The Visual 5-Year Price Corridor Bar:**
   ```text
   [$18.40 ────●─────────────── $64.80] (21st %-tile)
   ```
   * `< 20th %-tile`: `💎 Deep Cycle Bottom (Bottom Quintile)`
   * `20th–40th %-tile`: `Accumulation Zone (Below Median)`
   * `40th–60th %-tile`: `⚖️ Historical Midpoint`
   * `60th–80th %-tile`: `Elevated Cycle Range`
   * `> 80th %-tile`: `⚠️ Late Cycle / Momentum Zone (Top Quintile)`

2. **5-Year Fundamental Multiple Corridors (`P/FCF`, `P/EBIT`, `P/TBV`, `P/S`):**
   For every weekly candle over the past 5 years, the engine matches the weekly close price against the prevailing fiscal year's per-share fundamentals ($\text{FCF/sh}$, $\text{EBIT/sh}$, $\text{TBV/sh}$, $\text{Sales/sh}$) to build the empirical distribution ($\text{Min}, \text{25th}, \text{Median}, \text{75th}, \text{Max}$):
   $$\text{Mean Reversion Target Price} = \text{Current Per-Share Metric} \times \text{5-Year Historical Median Multiple}$$
   * **💎 Deep Value Compression (< 25th %-tile):** Multiple is compressed into the bottom quartile of its 5-year history. Mean reversion to the 5-year median multiple provides significant upside without requiring heroic earnings growth.
   * **⚖️ Historical Fair Value (25th–75th %-tile):** Trading within normal historical bands.
   * **⚠️ Multiple Expansion (> 75th %-tile):** Historically expensive relative to its own 5-year baseline.

---

## Section 5: SIC Industry Peer Benchmarking & Relative Scale

Queries `master_universe.sqlite` (the active SEC operating universe, queried dynamically at runtime) for the **top 3 competitors by Market Cap** sharing the exact same **4-digit SEC Standard Industrial Classification (`SIC`) code** (falling back to the 2-digit SIC group only if fewer than 3 companies exist in the 4-digit niche):
* Assigns relative scale badges:
  * `[Industry Leader: Nx larger]` (Peer is ≥ 2.5× the subject company's market cap)
  * `[Direct Peer: ~Nx]` (0.4× to 2.5× market cap)
  * `[Smaller Peer: Nx]` (< 0.4× market cap)
* **What to look for:** When a `$150M` small-cap subject company commands a `16%` FCF Yield, `+$12/sh` Net Cash, and an `8/9` Piotroski score while its `$10B` SIC industry leader trades at a `4%` FCF Yield with heavy net debt, you have identified structural small-cap mispricing.

---

## Section 6: Smart Money & Insider Conviction Signals (`ingestion/insider_feed.py` & `item5_record_holders.py`)

1. **Form 4 Open-Market Purchase Surveillance:**
   * Filters strictly for **Transaction Code `P` (Open-Market Purchase)** paid out of an insider's personal after-tax cash.
   * Automatically strips out noisy option grants (`Code A`), option exercises (`Code M`), tax withholding dispositions (`Code F`), and scheduled 10b5-1 sales.
   * **🔥 C-Suite Cluster Buy Alert:** Triggered when multiple senior officers (CEO, CFO, COO, President, Chairman) buy shares on the open market within the trailing window, or when net open-market buying crosses institutional conviction thresholds.
2. **10-K Item 5 Direct Registered Holders (DRS Transfer Agent Census):**
   * Scans the verbatim text of Item 5 (*"Market for Registrant's Common Equity"*) across multi-year 10-K filings to extract the exact count of **registered shareholders of record** at the company's transfer agent and normalizes it as `Holders per 1M Shares`.

---

## Section 7: Volume & Social Quiet (`Silent Accumulation Zone`)

Compares the recent 20-trading-day average volume against the 90-trading-day baseline and mandates a minimum dollar volume hurdle:

### A. Mandatory Minimum ADDV Liquidity Filter (Task 4.2)
Before evaluating volume ratios, the engine calculates the 30-day Average Daily Dollar Volume (ADDV = Mean Volume_20d × Spot Price):
* **ADDV < $250k (`FAIL — Illiquid Order Book`):** Disqualifies the stock from receiving any silent accumulation bonus. Illiquid order books lack institutional exit liquidity and cannot be conflated with genuine quiet accumulation.
* **ADDV ≥ $250k (`PASS — Sufficient Liquidity`):** Order book possesses institutional depth to proceed to volume ratio evaluation.

### B. Volume Turnover Ratio
$$\text{Volume Ratio} = \frac{\text{Mean Volume}_{20\text{d}}}{\text{Mean Volume}_{90\text{d}}}$$
* **≤ 1.10× (`PASS — Silent Accumulation Bonus +1`):** Volume is dry and quiet with verified ADDV ≥ $250k. Institutions can accumulate via passive limit orders without retail mania.
* **1.11× to 2.49× (`NEUTRAL`):** Normal two-way turnover.
* **≥ 2.50× (`CAUTION — Elevated Volume Exit Warning -1`):** Volume has surged ≥ 2.5× above normal. High risk of retail chasing; do not initiate fresh market buys. Exit rules scale sales into this liquidity.
* **`N/A` (Volume / Price Unavailable):** When verified non-synthetic volume history or spot price is unavailable, `Volume Ratio` and `30d ADDV` remain explicitly `N/A` with zero fabricated baseline volume.

---

# MODULE 3: Level 3 — Complete SEC EDGAR Financial Statements & Audit Vault

Hidden behind a collapsible `<details markdown="1">` drawer at the bottom of every Executive Card is the complete, unedited **10-Section SSR v1 Forensic Audit Vault** (`reporting/ssr_report.py`). Whenever a number in Level 1 or Level 2 looks too good to be true, open Level 3 to verify the raw SEC receipts:

| Vault Section | What It Contains & How to Use It |
| :--- | :--- |
| **Sections 1–3: Income Statement, Balance Sheet & Cash Flow Statement** | Rolling **5-Year Annual History + TTM** alongside the **6 Most Recent Discrete Quarters** (`Q1/Q2/Q3/Q4`). Every cell carries a data-integrity badge: clean number = `VERIFIED` direct XBRL tag; `*` = `DERIVED` via accounting identity (e.g., Q4 = FY - (Q1 + Q2 + Q3)); `NR` = Not Reported in filing. |
| **Section 4: Share Count & Tangible Book Value** | Tracks `Cover_Page_Shares_Outstanding` (`dei:EntityCommonStockSharesOutstanding` printed on Page 1 of the 10-K/10-Q/A, preserving raw `source_period_end` separately while aligning balance-sheet `period_end` strictly within `[-7, +75]` days and `<= filed`) vs. `Diluted_Shares_Outstanding` to expose employee option overhang, plus exact Goodwill and Intangible deductions. |
| **Section 5: Multi-Horizon Growth (`5Y/10Y/15Y CAGR`) & Common-Size Statements** | Computes 5-year, 10-year, and 15-year CAGRs across Revenue, EBIT, Net Income, OCF, FCF, TBV, and Diluted Shares, followed by **Common-Size Income Statement (`% of Revenue`)** and **Common-Size Balance Sheet (`% of Total Assets`)** to spot margin expansion or inventory/receivables bloat at a glance. |
| **Section 6: Financial Ratios & `5Y/10Y` Return on Capital Consistency** | Tracks Gross, Operating, Net, and FCF margins, Current/Quick ratios, Debt/Equity, Net Debt/EBITDA, and **`5Y/10Y Median vs. Min (Trough)`** for `ROIC`, `ROCE`, and `ROE`—showing how the business performed in its worst historical year. |
| **Section 7: Quantitative Forensics & Serial Roll-Up Dilution Audit** | Full breakdown of Piotroski (0–9), Altman Z, Beneish M, SBC % of OCF, and the **Serial Acquirer Roll-Up Trap Audit** (flags companies where 5-year M&A spending exceeds 50% of 5-year FCF while Goodwill + Intangibles bloat above 40% of Total Assets). |
| **Section 8: Roaring Kitty Inverted Yields, Synthetic Deleveraging & Reverse DCF** | Displays valuation multiples as **Inverted Yields** (`FCF/P`, `E/P`, `TBV/P`, `Sales/P`, `EBIT/EV`, `FCF/EV` — where higher % = cheaper stock), the Synthetic Deleveraging table, and a **Reverse DCF** (r = 10%, Terminal Growth = 2.5%) solving for the **Implied 10-Year FCF CAGR** currently priced into the stock. |
| **Section 9: Plain-English Metric Guide & Ownership Tables** | Multi-year `10-K Item 5` transfer agent record holder table (with verbatim sentences from each 10-K) and the complete `Form 4` insider transaction log. |
| **Section 10: SEC EDGAR Provenance Appendix** | Line-by-line audit table listing every canonical field, its latest period end date, status (`VERIFIED` / `DERIVED`), the **exact US-GAAP XBRL tag**, the **SEC Accession Number**, and the **Filing Date**. |

---

# MODULE 4: Portfolio Microstructure, Sector Caps & Forward Ledger Rig

## 1. GICS 20.0% Sector Concentration Ceiling (`strategies/position_sizing_and_execution.py`)
Quantitative value screens frequently suffer from unintended sector crowding (e.g. screening cheap cyclicals during an industry down-cycle). The engine enforces a strict concentration constraint:
$$\sum_{i \in \text{Sector } S} \text{Weight}_i \le 20.0\%$$
* If candidate allocations in any single GICS sector exceed 20.0% of total capital, allocations within that sector are scaled down pro-rata.
* All trimmed capital is routed directly to the **Treasury Yield / Cash Reserve Floor** (Tobin's Separation Theorem) rather than forced into lower-quality names.

---

## 2. Persistent SQLite Forward Ledger (`reporting/forward_ledger.py`)
To prevent survivorship bias and measure forward performance rigorously, every published investment card is automatically logged at publication time into `data_lake/forward_execution_ledger.sqlite`:
* **Logged Parameters:** Entry date, spot price, blended VWAP basis, target 1/2 prices, hard stop, catastrophic stop (-25% from VWAP), allocated capital, tranches, and GICS sector.
* **Forward Horizon Tracking:** Evaluates forward 3-Month, 6-Month, and 12-Month point-in-time returns against subsequent weekly price candles.
* **Milestone Triggers:** Automatically records whether positions reach `TARGET_1_HIT`, `TARGET_2_HIT`, `STOPPED_OUT`, or `CATASTROPHIC_STOP`.
* **Execution Analytics:** Continuously tracks aggregate win-rate, profit factor, average return, and maximum adverse excursion (drawdown) across all archetype tiers.

---

## 3. Point-in-Time Statement Lag Rig (`models/statement_builder.py`)
To eliminate lookahead bias in historical backtesting:
* **Full Ledger & Selection Modes:** `build_observation_ledger_from_dict()` preserves all original (`10-K`, `10-Q`), comparative, and amended (`10-K/A`, `10-Q/A`) XBRL observations, while `select_point_in_time_observations()` and `build_statements(facts_df, as_of_date="2024-06-30", selection_mode="latest_revised")` switch cleanly between field-level `"latest_revised"` amendment overlays and raw `"original"` filings.
* **Causal Pre-Derivation Filtering:** Historical XBRL records are filtered by verified SEC filing date (`filed <= as_of_date`) **before** deduplication, YTD discrete-quarter subtraction, and cross-field derivations (`Free_Cash_Flow = Operating_Cash_Flow - Capital_Expenditures`), and every derived metric inherits `filed = max(input_filed_dates)` so no derived value can surface before its newest underlying filing.
* **Context-Validated XBRL Extraction & Reconciliation (`ingestion/filing_context_validator.py`):** Conditional aliases across `Revenue` (`RevenueFromContractWithCustomerExcludingAssessedTax`, `SalesRevenueNet`, `SalesRevenueGoodsNet`), `Interest_Expense` (`InterestExpenseNonoperating`, `InterestExpenseDebt`, `InterestAndDebtExpense`), and `Cost_of_Revenue` (`CostOfGoodsSold`) are never blanket-promoted across companies; offline validation across both iXBRL `.htm` and legacy `FilingSummary.xml`/`R*.htm` statements verifies consolidated primary statement membership (or verified nonoperating financing-cost note tables), undimensioned entity-wide context, exact period/unit/CIK/`companyfacts` agreement, positive debit interest expense (`InterestPaidNet` strictly excluded), sole consolidated cost-of-sales without ex-D&A exclusions, and statement-bounded BS/IS reconciliations for missing `Total_Liabilities`, `Gross_Profit`, `Short_Term_Debt`, and `Long_Term_Debt` via `reconcile_missing_observation()`, routing uncertain cases to `NEEDS_REVIEW`.

---

---

# MODULE 5: Capital Discipline, Filer Integrity & Execution Calibration

## 1. The Dry Powder Mandate & Tobin's Separation Theorem (`strategies/position_sizing_and_execution.py`)
Quantitative stock selection models often fall into the trap of forced capital deployment—forcing an arbitrary sleeve allocation (e.g. 65% for Compounders) to be divided among whatever few candidates survive the screening gate.
* **The Mathematical Correction:** Individual candidate allocations are strictly bounded by:
  $$\text{Target Weight}_i = \min(\text{target\_ticker\_pct}, \text{max\_ticker\_cap\_pct})$$
  (5.5% for Compounders, 1.0% for Net-Nets, 2.8% for Turnarounds, 1.0% for Quarantined).
* **The Dry Powder Floor:** If only 3 compounders qualify (3 × 5.5% = 16.5%), the unallocated 48.5% of the sleeve is NOT crammed into those 3 names. It defaults automatically to `plan.cash_reserve_usd` (Treasury Dry Powder earning live T-Bill yields).
* **Concentration Capping:** Likewise, excess capital trimmed by the 2.0% ADDV liquidity limit or the 20.0% GICS sector ceiling flows directly into Treasury Dry Powder rather than being re-allocated to risk assets (Tobin's Separation Theorem).
* **Fail-Closed Finalist Withholding:** Finalists missing a verified spot price (Stage 1 shortlist / quote / manifest) or verified 30-day volume (`volume_cache.json` / `quotes_cache.json` / live feed) are withheld in `plan.unverified_finalists` rather than filled with static price/volume tables, retaining 100% of withheld capacity in Treasury Dry Powder.

---

## 2. Active Filer Integrity & Acquisition Remapping (`antigravity_v3_core/strategies/thematic_mapper.py`)
In automated supply-chain NLP extraction (Item 1 parsing), 10-K text frequently references defunct, acquired, or private partners (e.g. "SanDisk", "Xilinx", "Twitter").
* **Active Filer Validation:** `validate_active_filer()` cross-references all anchors and extracted candidates against `master_universe.sqlite`.
* **Automatic Remapping:** Acquired entities are automatically mapped to their active public parent (`SNDK` → `WDC`, `ATVI` → `MSFT`, `XLNX` → `AMD`, `ALXN` → `AZN`).
* **Fail-Closed Ejection:** Defunct, delisted, or private companies without an active SEC CIK entry (`TWTR`) are immediately ejected from the scan queue with an explicit rejection record in the tailings log (`[EJECTED: INACTIVE/DELISTED]`).

---

## 3. Stage 3 Limit Ladder Paper Execution Engine (`strategies/execution_simulator.py`)
Provides deterministic paper execution of Stage 3 limit order ladders against historical daily/weekly candles ([Open, High, Low, Close]):
* **Tranche Fills:** Tranche 1 (Market) executes at candle open; Tranches 2 and 3 (Limits) execute when candle lows touch or breach limit targets.
* **Dynamic VWAP Recalibration:** Each time a limit order triggers, the filled blended entry VWAP is recomputed across all accumulated shares.
* **Dynamic Catastrophic Stop Adjustment:** The non-negotiable -25.0% catastrophic stop is recalibrated downward from the updated blended VWAP (VWAP × 0.75), preventing false stop-outs when accumulating at deeper discounts.

---

## 4. Automated Forward Ledger Batch Calibration Runner (`scripts/audit_forward_ledger.py`)
Continuously audits forward point-in-time performance and hit rates without lookahead bias:
* Sweeps all issued cards in `data_lake/forward_execution_ledger.sqlite`.
* Computes forward 3M, 6M, and 12M point-in-time returns and maximum adverse excursions (drawdowns).
* Outputs an institutional calibration dossier at `reports/Forward_Ledger_Calibration_Audit.md`.

---

## 5. Market Volatility & Liquidity Advisory Guidance (`models/macro_regime.py`)
Evaluates CBOE VIX levels to surface institutional advisory guidance without programmatic order disallowance:
* **Complacent / Frothy (VIX < 15):** Valuation multiples are elevated; caution against chasing momentum; keep dry powder intact.
* **Normal Volatility (15 ≤ VIX ≤ 23.0):** Aligned to the `VIX > 23.0` structural skew tripwire; standard 3-tranche ladder execution is appropriate.
* **Elevated Volatility Caution (23.0 < VIX ≤ 35):** Triggered once `VIX` crosses the `23.0` skew tripwire. Options market makers typically operate in negative gamma positioning (though modern electronic retail-to-retail facilitation often dampens directional hedging flow). Bid-ask spreads widen and slippage increases; caution advised on market orders, recommending patient discount limit bids. At **`VIX ≥ 25.0`**, option convexity shifts into a **Vega-as-a-Flow** regime where dealer spreads widen dynamically and wingy put demand accelerates.
* **Crisis / Dislocation (VIX > 35):** Severe market panic creates asymmetric deep-value opportunities (Buffett: "Be greedy when others are fearful"); deploy strictly via deep limit order ladders beneath the tape.
* **Volatility Data Unavailable (`VIX is None` or `≤ 0`):** Returns `VOLATILITY_DATA_UNAVAILABLE` rather than defaulting to `VIX 18.5` (`NORMAL_VOLATILITY`).

---

## 6. V3 Options Gamma Exposure (GEX) Surface & Zero-Gamma Flip (`models/gex_engine.py` & `!gex [TICKER]`)
Complements fundamental limit order ladders with real-time dealer option-hedging microstructure (`!gex [TICKER]` on Discord or Option 3 in `Run_Antigravity_V3.command`) under the explicitly labeled **Naive GEX (`+Call OI`, `-Put OI`)** dealer assumption:
* **Multi-Horizon Windowing (Strictly `OI > 0` Settled Anchors) & Standard OPRA Filtering:** Splits liquid `openInterest > 0` standard `100`-share contracts into **Tactical (`0–14 DTE`)**, **Structural (`15–45 DTE`)**, and **Quarterly (`46–120 DTE`)**, omitting zero-OI intraday `0DTE` noise from structural anchors, flagging Schwab `isChainTruncated` truncation, and excluding adjusted non-standard OPRA contracts (`models/option_contract_utils.py`). ATM walls right at spot (`strike >= spot` for Calls, `strike <= spot` for Puts) are preserved cleanly alongside exact expiration bid metadata (`support_bid_exp` / `resistance_bid_exp`).
* **Scale-Invariant Dollar GEX ($1\%$ Move), Analytical Vanna/Charm & Fail-Closed $\Gamma$:**
  $$\text{Share GEX}_K = (\text{OI}_{\text{call}} \cdot \Gamma_{\text{call}} - \text{OI}_{\text{put}} \cdot \Gamma_{\text{put}}) \times 100, \qquad \text{Dollar GEX}_{1\%} = \text{Share GEX}_K \times S \times (0.01 \cdot S)$$
  $$\text{Vanna} = -\phi(d_1)\frac{d_2}{\sigma}, \qquad \text{Charm} = -\phi(d_1)\frac{2rT - d_2\sigma\sqrt{T}}{2T\sigma\sqrt{T}}$$
  Parameterized to `get_live_tbill_yield()`, the solver computes analytical BSM Greeks whenever after-hours OPRA feeds return `-999.0` **only from verified `volatility` or valid two-sided quotes (`bid > 0`, `ask >= bid`)**—never `theoreticalVolatility`, `closePrice`, or synthetic `35%` IV. Reports also surface `-1% IV` Vanna hedge flows, `+1d` Charm decay flows, Next-OpEx gross `|GEX|` release %, and Expiring Call-Delta Mix (`<50%` put saturation vs. `>60%` constructive).
* **Spot-Grid Portfolio Zero-Gamma Flip (`ZGL`), Gross vs. Net Walls & `25Δ` Skew Polarity:** Evaluates aggregate portfolio Net Gamma across a hypothetical $\pm 20\%$ spot grid $S^\ast$ (`None` / `N/A` when strictly single-signed, never inventing a minimum-$|\text{Net GEX}|$ strike), separates Gross Call/Put OI Walls from Net Positive (`+GEX`) / Net Negative (`-GEX`) Walls, prefers liquid `DTE >= 2` `OI > 0` contracts for `Near-Term ATM IV`, optionally compares local daily `RV(20D)` (`IV - RV`), and computes `25Δ` Put-minus-Call IV skew to flag probable `LIKELY_INVERTED_CALL_BIDDING` on call-chased single stocks. Single-stock runners check `data_lake/earnings_calendar_cache.json` before `yfinance` and surface `quote_source` / `is_stale_quote` flags.

---

## 🛠️ Quick Operator Commands for SSR v2

| Task | Command / Shortcut |
| :--- | :--- |
| **Interactive Double-Click Launcher** | Double-click [`Run_Executive_Card.command`](file:///Users/robertjenkins/.gemini/antigravity/scratch/logic-engines/Run_Executive_Card.command) and type one or more tickers (e.g., `STRT NRDS GME`). |
| **CLI Single or Multi-Ticker Run + Web Publish** | `python3 run_ssr_v2.py STRT UEIC --publish` |
| **Custom Position Size Override** | `python3 run_ssr_v2.py STRT --position-usd 5000` |
| **Batch Refresh All Published Cards (Dynamic Discovery)** | `python3 scripts/batch_refresh_all_cards.py --push` (dynamically discovers `*.md` cards in `Single_Stock_Web` and refreshes from live/verified feeds with zero static price fallbacks) |
| **Single-Ticker GEX Surface Radar** | Double-click `Discord_Bot/Run_Single_Ticker_GEX.command`, run Option 3 in `Run_Antigravity_V3.command`, or type `!gex [TICKER]` in Discord |

---

*Antigravity V3 Core | SSR v2 Executive Engine Master Curriculum*


## XBRL concept integrity — November 9, 2026

<details markdown="1">
<summary>A=A mappings, units, and missing data</summary>

Canonical financial fields now select one explicitly defined XBRL concept. Alternate concepts are retained as separate `Reported_...` fields, not substituted for totals or differently scoped measures. The dictionary records source definitions and labels. USD monetary facts and share units are selected explicitly; no implicit currency conversion occurs. Missing values remain NR.

Unqualified gross-profit, operating-income, pretax-income and liabilities arithmetic fallbacks are removed. Project-defined free cash flow is operating cash flow minus payments to acquire PP&E, requiring matching periods and units. YTD subtraction requires matching fiscal starts, source concepts and units. Weighted-average share counts require direct quarterly disclosures rather than equal-quarter approximations.

This mapping change reduces some canonical coverage. Supplemental fields are present in normalized facts and statement tables; the fixed master-universe export has not been expanded. Existing caches and published reports have not been regenerated. Downstream zero defaults, display labels and company-specific reconciliation must be checked before publishing a rebuilt lake. Dossier-specific extraction remains a separate repair scope.

</details>


### Superseding clarification: fixed columns and alias review inventory

The data lake retains its original canonical columns. Alternate concepts are stored in `config/xbrl_alias_review_inventory.yaml`, not emitted as additional statement/data-lake columns. Candidates require definition, unit, period, scope and primary-filing evidence before approval. Earlier references to supplemental `Reported_...` output fields describe an interim implementation that has now been removed. Raw source data remains unchanged. Downstream formula and dossier work is deferred until the data-lake mapping review is settled.


### Missing-cell audit queue — November 10, 2026

The mapping audit separates candidates requiring filing evidence from alternatives already known to have incompatible accounting scope. Cash interest paid cannot substitute for accrual interest expense. A broad payable/accrual balance cannot substitute for trade payables. These rejected alternatives remain in the terms inventory for traceability, but are not counted as prospective direct aliases. Financial/REIT exclusions and unknown-SIC companies are reported separately. Snapshot cells retain periods and missing-value reasons; the current review snapshot is annual/instant, not TTM.


### Source retention and contextual revenue mappings

SEC source refreshes preserve prior and new content-addressed versions before replacing live caches. Existing baseline captures retain unknown original retrieval dates. Retaining bytes is distinct from implementing correct as-of observation selection, which remains separate work. Contract-revenue terminology is accepted only where verified as the total/sole consolidated operating-revenue line with matching period, unit and source observation. Sample validation does not authorize a universal alias. Evidence and missing-value states remain explicit.


### Fail-closed reporting & lookback hygiene — November 15, 2026

Legacy synthetic defaults and multi-year staleness leaks have been excised across models, strategies, and report renderers:

* **No Synthetic Defaults (`NR` / `UNAVAILABLE`):** Static price and volume fallback tables (`BASELINE_VOLUME_PARAMS`, `ALL_TICKER_PRICES`), `or 1.0` share-count fallbacks, `or 0.0` cash-flow/capex defaults, `$10.00` placeholder prices, `50,000`-share volume stubs, and `VIX 18.5` assumptions are removed. Unpopulated canonical metrics render `NR` or `UNAVAILABLE`, and SSR v2 withholds limit-order ladders and forward ledger writes whenever verified spot price is missing.
* **Recency Cap on Latest Extractions:** Current annual flow and balance-sheet extractions in `reporting/ssr_executive.py` enforce a `max_lookback_fys=1` cap (`max_lookback_fys=2` for share-count fallbacks) so decade-old unpopulated rows cannot leak into current valuation floors or CapEx starvation checks.
* **Zero-Midpoint Scoring & Fail-Closed Stage 3:** `models/convergence_radar.py` awards `0` points with `NR` status tags for missing inputs rather than neutral midpoints. `strategies/position_sizing_and_execution.py` withholds finalists missing verified price or 30-day volume in `unverified_finalists` (retaining capacity in Treasury Dry Powder) and dynamically interpolates specialized exit bullets strictly from active positions.


### Candidate historical lake validation & archive boundaries — November 15, 2026

Backlog Task 4 validates the full archived SEC bulk universe in an isolated staging area (`data_lake/candidate/historical_lake.sqlite` and `data_lake/candidate/master_universe.sqlite`) without overwriting production `data_lake/bulk/master_universe.sqlite`:

* **Universe Separation & Survivorship Boundaries:** Audits active listed (`_cik_map.json`) vs. delisted/inactive (`companyfacts.zip`-only) issuers, financial/REIT exclusions (`SIC 6000–6799`), unknown-SIC entities, and non-`10-K`/`10-Q` filers separately; pre-2009 SGML/HTML filings fall outside `companyfacts.zip` (`Pre-XBRL` floor), and context-gated tags (`RevenueFromContractWithCustomerExcludingAssessedTax`, `InterestExpenseNonoperating`, `CostOfGoodsSold`, Batch 4 HTML reconciliations) execute strictly on locally cached HTML/XML (`unknown_unavailable:filing_review_required` when uncached).
* **Overflow Submissions & Future-Date Typo Guard:** Merges `submissions.zip` overflow arrays (`CIK*-submissions-*.json`) prior to `/A` amendment resolution and cover-page share alignment (`[-7, +75]` days, `<= filed`), and rejects corrupted future `period_end > filed + 7` days (across both GAAP and DEI cover-page facts) or GAAP `> reportDate + 14` days (`date_anomaly_end_after_filed`).
* **Lossless Period Views & Tri-State Applicability:** Stores separate `FY`, `Q`, `YTD2`/`YTD3`, `I`, `TTM` (requiring 4 contiguous quarters within `240..315` days via `inspect_ttm_contiguity()`), `is_latest_revised`, `is_original`, and `restatement_diffs` tables, preserving `evidenced_non_applicable` states (`pre_asc842_operating_lease`, `single_step_income_statement`, `zero_total_liabilities_debt_free`, `non_operating_or_non_10kq`) separately from `unknown_unavailable` gaps.

### Incremental maintenance, share-count & cohort hygiene (Backlog Task 5) — November 16, 2026

* **Incremental Refresh & Indexed SQLite Speed:** `ingestion/candidate_lake.py` (`incremental_update_candidate_lake`, `scripts/rebuild_candidate_lake.py --incremental`) fingerprints ZIP `(CRC, file_size)` / file SHA-256 metadata per CIK in `issuer_maintenance_state`, separates XBRL changes from quote/insider snapshot refreshes, reuses validated HTML/XML mappings in `verified_context_cache` under explicit `(cik, accession, source_sha256, aliases_sha256, validator_version)` invalidation (`VALIDATOR_VERSION = "2026-11-16.v1"`), logs taxonomy/restatement/presentation/regime-shift deltas in `maintenance_events`, and adds composite `(cik, is_latest_revised, ...)` and `(ticker, is_latest_revised, ...)` indexes + `ANALYZE;` (reducing unchanged `21,573`-CIK refreshes from `359.25s` to `14.22s`, `25.3x` faster).
* **Share-Count, Scale & Cohort Hygiene:** `_pick_latest_shares()` in `models/valuation.py` requires `>= 10,000` shares across `TTM` + `fy_cols[-2:]` before falling back to sub-10k stubs (`VTIX`/`QVCG`), while `models/wide_net_scoreboard.py` reconciles `1,000x` XBRL share overstatements / `< 10k` stubs against Nasdaq implied shares, sets `Latest_Period_End = max(TTM, FY, Q)`, excludes Financials/REITs (`SIC 6000–6799`) and stale/regime-shifted filers (`STALE_FILER_MAX_AGE_DAYS = 550` or superseding `15-12G`/`15-15D`/`40-8F-2`/`20-F`/`NPORT-P`) from operating buckets and Stage 1 (`select_operating_hunting_buckets_df()`, `select_stage1_convergence_df()`), and surfaces non-stale Fin/REIT buyback/insider signals separately in `Financial_REIT_Signals.csv` via `select_financial_reit_signals_df()`.
* **Master Workbook Refresh:** `scripts/build_master_spreadsheet.py` builds `Logic_Engines_Master_Review.xlsx` directly from structured `data_lake/candidate/` exports and `SSR v2` stock vaults across 4 sheets (`Executive Watchlist`, `Stage 1 Shortlist`, `Hunting Buckets`, `Financials & REITs`), preserving `None` without `or 0.0` cash coercions.

### Weekend Scans & Pre-Publication Integrity Gate (Backlog Task 7) — November 16, 2026

* **Atomic Candidate Promotion & Bulk Quote Freshness:** `promote_candidate_snapshot()` (`scripts/rebuild_candidate_lake.py --promote-only`) verifies `PRAGMA integrity_check = ok`, 68-column completeness, and Stage 1 operating/dilution hygiene before backing up `.backups/pre_promote_*` and atomically replacing `data_lake/bulk/master_universe.sqlite` and `reports/*.csv` (zero reconciliation diffs). `inspect_bulk_quotes_freshness()` (`ingestion/bulk_universe.py`) reads internal `updated_at` timestamps inside `quotes_cache.json`, warns on stale fallback, and surfaces `STALE` status when quotes exceed $72\text{h}$.
* **Pre-Publication Gate & Test/Prod Isolation:** `reporting/pre_pub_gate.py` (`validate_kramdown_markdown`, `validate_single_stock_card`, `validate_publication_bundle`) gates `data_lake_publisher.py`, `web_publisher.py`, `batch_refresh_all_cards.py`, `upgrade_morning_briefing.py`, and `reconcile_portfolio.py` against Kramdown violations, synthetic test artifacts (`EX0`), Fin/REIT Stage 1 leaks, row mismatches, and stale quotes prior to any `git push`, while keeping test runs strictly isolated from production `reports/Hunting_Buckets_Report.md`.

### Standalone Deep Dossier Engine & Offline Vault Integrity (Backlog Task 8) — November 16, 2026

* **Offline Period Alignment & Future-Date Guard:** `ingestion/dossier_ingestor.py` aligns `companyfacts.json` (`extract_xbrl_forward_and_inventory_stages(..., as_of_period_end=...)`) strictly to the latest cached filing's `period_end`, applies SEC form and future-date anomaly guards (`end <= filed + 7d`), computes discrete quarterly cash flows/CapEx via `compute_discrete_quarterly_flow_series()`, detects `dei:DocumentType` (`10-K` vs. `10-Q`), and loads local market state (`load_dossier_market_context()`) exclusively from verified offline vault artifacts (`price_history.json`, `quote.json`, `master_universe.sqlite` fallback, `benchmark_snapshot.json`), leaving uncached candles/peers explicitly `None`/`Unavailable` rather than fabricating synthetic drawdowns.
* **Issuer-Matched Form 4, Dual Runway & Archetype Routing:** `parse_form4_24m_with_option_context()` enforces strict `<issuerCik>`/`<issuerTradingSymbol>` verification and share-capped `[-1, +5]` day `Code M -> Code S` pairing; `compute_pre_revenue_runway_forensics()` separates restricted cash, prevents `abs(+profit)` burn inversion, and reports CapEx-adjusted Free Cash Flow runway alongside GAAP operating burn runway; `strategies/dossier_strategy.py` and `reporting/dossier_report.py` enforce zero hardcoded figures, OMR probabilistic prose, empty-table omission, and full Kramdown compliance across all 5 accounting archetypes.

### GEX v2 Spot-Grid Zero-Gamma, Gross-vs.-Net Walls & Analytical Vanna/Charm — November 19, 2026

* **Strict `OI > 0` Anchoring & Multi-Horizon `46–120 DTE` Quarterly Window:** `models/gex_engine.py`, `reporting/gex_report.py`, and `scripts/run_gex_ticker.py` extend option-chain coverage to `120` days (`strike_count=150`, surfacing `isChainTruncated`) in a single request, keep `openInterest > 0` as the sole wall/flow anchor (excluding intraday `0DTE` `OI=0` noise, `theoreticalVolatility`, and `closePrice` leaks), and prefer liquid `DTE >= 2` contracts for `Near-Term ATM IV`.
* **Spot-Grid ZGL, Net Walls, Vanna/Charm & `25Δ` Skew:** Evaluates Portfolio `ZGL` across a $\pm 20\%$ spot grid returning `None` when strictly single-signed, separates Gross Call/Put OI Walls from Net `+GEX`/`-GEX` Walls, computes analytical Vanna (`-1% IV`), Charm (`+1d`), Next-OpEx `|GEX|` roll-off %, Expiring Call-Delta Mix, and `25Δ` skew polarity (`LIKELY_INVERTED_CALL_BIDDING` vs. `NORMAL_PUT_SKEW`).

### `10-Q` Maturity Walls, Primary iXBRL Debt Reconciliation & Macro Credit Context — November 19, 2026

* **Atomic `10-Q` / `10-K` Maturity Schedules & Revolver Separation (`models/debt_maturity.py`):** Anchors every debt maturity schedule to one periodic filing (`10-K`, `10-K/A`, `10-Q`, `10-Q/A`), separates fiscal-calendar schedules (`RemainderOfFiscalYear + FY+1 + FY+2`) from rolling `12M` tags, and surfaces `LineOfCreditFacilityRemainingBorrowingCapacity` separately from bank cash.
* **Primary `.htm` Filing Cache & Macro Benchmarks (`ingestion/stock_vault.py`, `reporting/ssr_executive.py`):** `ensure_periodic_filing_htmls()` caches latest `10-K`/`10-Q` `.htm` files under `dossier/filings/` so `normalize_xbrl_facts()` runs `filing_context_validator` balance-sheet and income-statement checks (`ShortTermBorrowings`, `LongTermDebtCurrent`, `LongTermDebtAndCapitalLeaseObligations`, `InterestExpenseDebt`), while `Credit & Refinancing Watch` displays broad Treasury/FRED `BBB`/`HY` benchmark context without relaxing issuer-level secondary bond withholding (`tests/test_bond_safety.py`).

### Purr Baseline Repairs: Zero Ticker Pinning, Math-Gap Ejection & 1-Tranche/Day Ladder — November 20, 2026

* **Zero Hardcoded Ticker Bypass & Math-Gap Ejection:** Excised `BASKET_TIERS["tickers"]`, `DEFAULT_FINALISTS`, and `DEFAULT_SECTOR_MAP` from `strategies/position_sizing_and_execution.py` and `reporting/ssr_executive.py`, plus static finalist prose in `reporting/stage2_triage.py` and `scripts/refresh_finalists_data.py`. Stage 1 (`select_stage1_convergence_df`), Stage 3 (`classify_stage3_tier`), and `SSR v2` (`_classify_archetype`) require complete unfabricated math (`Share_Price > 0`, `Piotroski_F_Score`, `Altman_Z_Score`, `FCF_to_Price_Yield_Pct`, `Revenue_TTM_M`), ejecting incomplete-math tickers into `unverified_finalists` (`MISSING_FORENSIC_MATH`) or `UNSUITABLE / INCOMPLETE FORENSIC MATH` (`$0.00` allocation, withheld from `forward_execution_ledger.sqlite`), and bumping `run_ssr_v2.py` to `max_filings_per_form=3` for YoY `10-K` context validation.
* **1-Tranche-Per-Day Guard & Share-Exact VWAP:** `strategies/portfolio_tracker.py` and `strategies/execution_simulator.py` enforce at most **1 buy tranche fill per trading day** and re-anchor `T2`/`T3` limits to the actual `T1` fill price; `calculate_tranche_vwap()` weights by actual integer-share cost (`target_shares * target_price`).
* **Unified Calibration Telemetry (`Option 7 -> 3`):** `antigravity_v3_core/scripts/performance_review.py` unifies `v1.0` + `v1.1` CSP ledgers with deduplication and local `price_history.json` fallback alongside `scripts/audit_forward_ledger.py` in `Run_Antigravity_V3.command`.

### Telemetry Integrity, Schwab Batch Quotes & Tranche-Unified Forward Audits — November 20, 2026

* **Schwab Batch Quotes, Freshness Gate & Batch Rebuild Isolation (`run_ssr.py`, `run_ssr_v2.py`, `reporting/ssr_executive.py`, `scripts/batch_refresh_all_cards.py`):** Spot quote resolution queries authenticated `SchwabClient.get_quotes()` first (batched at 50 symbols in `batch_refresh_all_cards.py`) with Yahoo v8 fallback and explicit `> 72h` staleness metadata (`quote_is_stale`), blocking stale quotes and routine batch rebuilds (`log_to_ledger=False` default) from writing duplicate or stale entries into `forward_execution_ledger.sqlite`.
* **Tranche-Unified Forward Ledger, Active-Lifecycle Dedup & `TIER_2_NET_NETS` Exit Guard (`reporting/forward_ledger.py`, `strategies/execution_simulator.py`, `strategies/position_sizing_and_execution.py`):** `update_forward_outcomes()` routes directly through `simulate_position_execution()` with catastrophic gap-down liquidation prior to averaging down and dynamic proportional hard-stop recalibration; `log_card_to_ledger()` prevents overlapping duplicate `ACTIVE` cards per ticker; `clean_forward_ledger()` backs up to `.backups/` and excises corrupted/stale/duplicate rows cleanly; and `TIER_2_NET_NETS` exit rules enforce `graham_ncav > price` and `tangible_book > price`.
* **Non-Interactive Publishing & Option 4 Batch Submenu (`reporting/web_publisher.py`, `Run_Antigravity_V3.command`):** Shared `run_git_push()` enforces `GIT_TERMINAL_PROMPT=0` with explicit timeout across all GitHub Pages publishers, and Option `4 -> 3` invokes `scripts/batch_refresh_all_cards.py` directly from the operator console.

### Two-Tier SSR Roster Lifecycle, Accession-Locked Statement Cache & Weekly Learning Retro — November 22, 2026

* **Two-Tier SSR Directory & 30-Day Cold Archive Drawer (`reporting/web_publisher.py`, `scripts/batch_refresh_all_cards.py`):** `classify_published_roster()` and `update_index_catalog()` partition published `Single_Stock_Web` cards into an **Active Surveillance Roster** (top viewport: active/queued `$100K` portfolio holdings, Stage 1 convergence shortlist survivors, and `<= 30`-day operating-sleeve cards) and a collapsible Kramdown **Cold Archive Drawer** (`<details markdown="1">`: `Quarantined` passes without active portfolio holdings, closed/stopped lifecycles, and aged `> 30`-day snapshots). Routine `batch_refresh_all_cards.py` runs refresh only the Active Surveillance Roster by default (preserving Cold Archive snapshots frozen at their last snapshot date unless re-qualified or run with `--include-cold`).
* **Accession-Locked 75-Quarter Statement Cache (`run_ssr_v2.py`):** `_load_or_build_accession_locked_statements()` locks normalized 20-year / 75-quarter `facts_df` and `StatementBundle` caches (`statements/_accession_bundle.pkl`) to `manifest.json::latest_periodic_accession` and `raw/companyfacts.json` size so price/insider refreshes skip redundant XBRL re-parsing whenever no new `10-K` or `10-Q` filing has dropped.
* **Daily-Bar Forward Ledger & Weekly Learning Counterfactual Lab (`strategies/learning_retro.py`, `reporting/learning_retro_report.py`, `scripts/run_weekly_learning_retro.py`):** `reporting/forward_ledger.py::update_forward_outcomes()` prefers dedicated daily (`1d`) `daily_price_history.json` bars over weekly (`1wk`) corridor caches so 3-tranche multi-day limit fills evaluate on true daily sessions. `run_weekly_learning_retro.py` (wired into `Run_Antigravity_V3.command` Option `7 -> 3`) generates `reports/Weekly_Learning_and_Calibration_Retro.md` (standalone local review report) comparing **Track 1 (Actual Fixed Price Stops)**, **Track 2 ("Dead Investor (`*`)" Fundamental Hold)**, and **Track 3 (Market-Benchmark-Adjusted Idiosyncratic Stops)** alongside matched-window `^RUT`/`^GSPC` benchmark alpha, Engine 1 safest-strike/DTE cohort matrices, and the Anti-Whiplash Human + Agent Decision Docket.




