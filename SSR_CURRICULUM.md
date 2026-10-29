# 🎓 The Antigravity SSR v2 Executive Engine: Master Architecture & Forensic Curriculum
**Document:** Institutional Single-Stock Operating Manual & Forensic Companion  
**System:** Antigravity V3 Core — Second-Rail Executive Single Stock Engine (`SSR v2`)  
**Primary Modules:** `reporting/ssr_executive.py` | `run_ssr_v2.py` | `reporting/ssr_report.py`  
**Methodology:** Deterministic Quantitative Rules | Adversarial XBRL Accounting | 3-Tranche Limit Order Execution  

[☕ Daily Morning Briefing](https://bobmahalo.github.io/morning-briefing/) | [📈 $100K Model Portfolio](https://bobmahalo.github.io/morning-briefing/PORTFOLIO.html) | [🎓 Master Curriculum](https://bobmahalo.github.io/morning-briefing/CURRICULUM.html) | [🔬 SSR Executive Curriculum](https://bobmahalo.github.io/morning-briefing/SSR_CURRICULUM.html) | [🗂️ Single Stock Directory](https://bobmahalo.github.io/Single-Stock-Scan/)

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
| **🪙 CASH COW / DEEP VALUE PLAY** | `TIER_DEEP_VALUE_CASH_COW` | Unallocated Sleeve | `3.5%` (`$3,500`) | `5.0%` | High FCF yield (≥ 10.0%) and structural profits, but mature operations with lower ROIC (< 15%) or limited reinvestment. Held for multiple mean reversion. |
| **🔵 MICRO-TURNAROUND & VALUE CATALYST** | `TIER_3_TURNAROUNDS` | `20.0%` | `2.8%` (`$2,800`) | `3.5%` | Beaten-down cyclical or turnaround with ≥ 8% FCF yield or verified C-Suite Form 4 cluster buying. |
| **🟡 BENJAMIN GRAHAM NET-NET ARBITRAGE** | `TIER_2_NET_NETS` | `5.0%` | `1.0%` (`$1,000`) | `1.5%` | Classic *cigar butt* trading at a strict 33% discount to Net Current Asset Value (Price ≤ 0.67 × NCAV). Because operations may be shrinking, **time is your enemy**—diversify in small 1% positions and sell at NCAV/TBV re-rating. |
| **🔴 QUARANTINED / ACCOUNTING MIRAGE RISK** | `TIER_QUARANTINED` | `0%` (Excluded) | `≤ 1.0%` (`≤ $1,000`) | `1.0%` | Triggered by SEC regulatory red flags (NT filings, 8-K restatements), accounting manipulation (M > -1.78), material working capital liquidation (> 20% of OCF), or operational insolvency (Z < 1.81). |
| **⚪ UNSUITABLE / PASS** | `TIER_UNSUITABLE_PASS` | `0%` | `$0.00` (`0.0%`) | `0.0%` | Fails minimum liquidation floor, structural earnings power, or return-on-capital hurdle criteria. Zero allocation; capital preserved in Treasury T-Bills. |
| **💵 U.S. T-BILLS / DRY POWDER FLOOR** | `CASH_RESERVE` | `10.0%+` | Baseline + Unfilled Sleeve | `100.0%` | Under **Tobin's Separation Theorem**, any unfilled sleeve capital remains in U.S. T-Bills rather than over-concentrating surviving picks. |

---

## 2. The Asymmetric Payoff Profile Box (Rx : 1.0 Expectancy)

Right below the archetype pill sits the monospaced **Asymmetric Payoff Profile Box**:

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
| **1-Year Share Count Change** | `4.0 pts` | ≤ -5.0% (Aggressive Cannibal) → **4 pts**<br>-1.0% to -4.9% (Buybacks) → **3 pts**<br>-0.9% to +1.0% (Stable) → **2 pts**<br>> +1.0% (Dilution) → **0 pts** |
| **C-Suite Form 4 Cluster Buying** | `4.0 pts` | `4.0 pts` if verified C-Suite open-market cluster buying (`Code P`)<br>`1.0 pt` baseline if quiet (0 cluster buys) |
| **Maintenance Capex Health** | `2.0 pts` | `2.0 pts` if CapEx / D&A ≥ 0.35<br>`0.0 pts` if Capex Starvation detected (CapEx / D&A < 0.35) |

* **⚠️ Dilutive Burn Trap Catch (`is_dilutive_burn`):** If a company has negative or zero Operating Cash Flow (OCF ≤ $0) while issuing positive Stock-Based Compensation (SBC > $0), dividing SBC by negative OCF produces a meaningless negative percentage. The engine catches this and prints **`⚠️ Dilutive Burn (OCF ≤ $0)*`**—exposing that management is paying themselves in stock while the business burns cash.

---

## 4. Deterministic 3-Tranche Limit Order Ladder & Valuation Exits

### A. The 3-Tranche Accumulation Ladder (`build_3_tranche_ladder`)
Never market-buy 100% of an allocation on day one. Every position is split into three mathematical tranches:

| Tranche | Order Type | Entry Price Formula | Weight | Tactical Purpose |
| :---: | :---: | :---: | :---: | :--- |
| **T1** | `MARKET / LIMIT` | Spot Price | `33.3%` | **Baseline Entry:** Establishes immediate exposure once the forensic audit passes; eliminates FOMO if the stock trends higher immediately. |
| **T2** | `GTC LIMIT` | Spot Price × (1 - Discount_retest) | `33.3%` | **Support Retest Bid:** Scaled dynamically to 1.0× ATR or 30-day Implied Volatility (minimum -6.0% baseline default) to capture multi-week consolidation pullbacks. |
| **T3** | `GTC LIMIT` | Spot Price × (1 - Discount_flush) | `33.4%` | **Capitulation Wick Bid:** Scaled dynamically to 2.0× ATR or 30-day Implied Volatility (minimum -12.5% baseline default) to capture deep liquidity sweeps. |

* **Full-Fill Blended Cost Basis (VWAP):** If all three tranches fill, your average cost basis is automatically lowered below your initial entry price:
  $$\text{VWAP}_{\text{ladder}} = \frac{\sum \text{Dollar Allocation}_i}{\sum \text{Target Shares}_i}$$

### B. Archetype-Specific Deterministic Exit Rules (`build_deterministic_exit_rules`)
Exit targets adapt dynamically to the stock's archetype so you don't hold a decaying Net-Net like a Compounder:
1. **For Graham Net-Nets (`TIER_2_NET_NETS`):**
   * **Target 1 (Sell 50%):** 100% of **Graham NCAV** (or +35.0% minimum re-rating fallback).
   * **Target 2 (Sell 50%):** 100% of **Tangible Book Value (TBV)** (or +65.0% re-rating fallback).
   * **Hard Stop:** -20.0% anchored to blended VWAP. Immediate exit if quarterly operational burn erodes > 20% of Net Current Assets.
   * **Catastrophic Stop:** Non-negotiable liquidation at -25.0% from VWAP.
2. **For Compounders (`TIER_1_COMPOUNDERS`):**
   * **Target 1 (Scale 33%):** Intrinsic fair-value re-rating (**+30.0%** or 12x–15x FCF).
   * **Target 2 (Scale 33%):** Full multiple expansion (**+65.0%** zero-growth convergence).
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

---

## Section 2: Balance Sheet Health & Debt Extinguishment Clock (`models/valuation.py` & `models/debt_maturity.py`)

Instead of relying on static debt-to-equity ratios, the engine models **Synthetic Deleveraging** and **Contractual Maturity Walls**:
1. **Excess Cash Application:** First, apply 100% of balance-sheet cash and short-term investments against total short- and long-term debt:
   $$\text{Remaining Net Debt} = \max(0, \text{Total Debt} - \text{Total Cash})$$
2. **The Debt Extinguishment Clock:** How many years of current Trailing Twelve Month Free Cash Flow would it take to retire 100% of remaining net debt?
   $$\text{Debt Extinguishment Clock (Years)} = \frac{\text{Remaining Net Debt}}{\text{TTM Free Cash Flow}}$$
   * **0.0 Years (Net Cash Surplus):** Total Cash exceeds Total Debt. Financial bankruptcy risk is near zero.
   * **≤ 3.0 Years:** Rapid deleveraging capacity; interest-rate shock resistant.
   * **> 5.0 Years (or Infinite when FCF ≤ 0):** High refinancing and credit-spread vulnerability.
3. **The 12–24 Month Contractual Debt Maturity Wall (`models/debt_maturity.py`):**
   Static debt ratios ignore *when* principal payments must be made. The engine extracts contractual debt maturity schedules directly from 10-K footnote disclosures (`us-gaap:LongTermDebtMaturitiesRepaymentsOfPrincipalInNextTwelveMonths` and `InYearTwo`):
   $$\text{Debt Due}_{\text{24M}} = \text{Year 1 Principal Due} + \text{Year 2 Principal Due}$$
   This maturity wall is stressed against liquid cash reserves and 2-year cumulative organic FCF capacity:
   $$\text{Total 24M Internal Liquidity} = \text{Cash} + (2 \times \max(0, \text{Annual FCF}))$$
   * **`NO_DEBT_RISK`:** Zero funded debt obligations.
   * **`FULLY_COVERED_BY_CASH`:** Available cash alone covers ≥ 100% of 24M maturities. Near-term debt can be retired without touching operational cash.
   * **`COVERED_BY_ORGANIC_FCF`:** Cash + 2-year FCF capacity covers ≥ 100% of maturities. Zero refinancing dependency.
   * **`REFINANCING_DEPENDENCY_WARNING`:** Positive FCF, but internal liquidity leaves a deficit against maturities. Company must refinance or roll credit facilities.
   * **`ACUTE_MATURITY_WALL_DISTRESS`:** Negative FCF / cash burn with debt maturities exceeding liquid cash reserves. High risk of distress or dilution.
4. **Secondary Corporate Bond Market Intelligence & The Credit Canary Engine (`scripts/test_bond_pull.py` & `data_lake/bonds/`):**
   Contractual SEC 10-K footnote schedules tell us what management *owes*; the secondary corporate bond market reveals what institutional credit investors *believe* about management's ability to refinance. The engine integrates live public bond issues across CUSIPs, coupons, maturities, secondary trade prices, and yields:
   * **Weighted Yield-to-Maturity (YTM):**
     $$\text{Weighted YTM} = \sum_{i=1}^{N} \left( \frac{\text{Principal}_i}{\sum \text{Principal}} \times \text{YTM}_i \right)$$
   * **Credit Spread / Option-Adjusted Spread (OAS in bps over Duration-Matched Treasuries):**
     $$\text{Credit Spread (bps)} = (\text{Weighted YTM} - \text{Benchmark Treasury Yield}) \times 10,000$$
   * **The Duration Discount vs. Credit Distress Canary Rule:**
     * **Duration Discount (Benign):** When interest rates rise, long-duration corporate bonds naturally trade at discounts to par ($70\text{–}85\text{ cents on the dollar}$) simply due to interest rate duration math. If the credit spread remains tight ($< 150\text{ bps}$) and credit ratings remain prime investment grade (`A` / `BBB`), the discount is benign duration repricing—not insolvency risk.
     * **Credit Canary (Distressed):** If secondary bond prices collapse into the $40\text{–}60\text{ cent}$ range while yields spike above $10\text{–}15\%$ and credit spreads blow out beyond $+500\text{ bps}$, institutional bondholders are pricing in severe default or restructuring probability. This acts as an unyielding **Credit Canary** that invalidates any optical "cheapness" in the equity.
   * **Zero-Debt Equity Fallback (Cash Fortress):**
     Companies operating with zero funded debt obligations (`CRUS`, `NRDS`) bypass bond tables gracefully. The engine renders an **Equity Shield & Cash Fortress** badge, confirming zero debt refinancing dependency and eliminating empty or broken report sections.

---

## Section 3: 5-Year Cumulative Capital Allocation & Share Cannibalization

Single-year cash flows are noisy. Section 3 sums **5 full fiscal years of Operating Cash Flow (5-Year OCF)** and tracks every dollar management spent across five buckets:

$$\sum \text{OCF}_{5\text{Y}} = \text{CapEx}_{5\text{Y}} + \text{Buybacks}_{5\text{Y}} + \text{Dividends}_{5\text{Y}} + \text{Acquisitions}_{5\text{Y}} + \text{Retained Surplus}_{5\text{Y}}$$

### The 5 Capital Allocation Postures
* **💰 Cannibal & Cash Return Engine:** (Buybacks_5Y + Dividends_5Y) / OCF_5Y ≥ 50.0%. Management returns the majority of organic cash flow directly to owners.
* **🏰 Organic Fortress Builder:** Retained Surplus_5Y / OCF_5Y ≥ 40.0%. Management stockpiles cash on the balance sheet and pays down debt.
* **⚙️ Heavy Capital Reinvestment:** CapEx_5Y / OCF_5Y ≥ 50.0%. Heavy physical reinvestment into factories, fleet, or infrastructure.
* **⚖️ Balanced Capital Deployment:** Balanced split across CapEx, buybacks/dividends, and balance-sheet retention.
* **⚠️ Dilutive Cash Burn:** 5-Year Cumulative OCF ≤ 0. Operations are cash-flow negative and subsidized by selling new stock (Equity Issuance) or borrowing (Net Debt Flow).

---

## Section 4: 5-Year Historical Valuation Corridor & Multiple Mean Reversion (`models/valuation_corridor.py`)

Rather than guessing what a stock's P/E "should" be using theoretical formulas, Section 4 maps where the stock trades today against **its own 5-year weekly empirical history** (`260 weekly candles`):

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

Queries `master_universe.sqlite` (5,349 SEC operating companies) for the **top 3 competitors by Market Cap** sharing the exact same **4-digit SEC Standard Industrial Classification (`SIC`) code** (falling back to the 2-digit SIC group only if fewer than 3 companies exist in the 4-digit niche):
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

---

# MODULE 3: Level 3 — Complete SEC EDGAR Financial Statements & Audit Vault

Hidden behind a collapsible `<details markdown="1">` drawer at the bottom of every Executive Card is the complete, unedited **10-Section SSR v1 Forensic Audit Vault** (`reporting/ssr_report.py`). Whenever a number in Level 1 or Level 2 looks too good to be true, open Level 3 to verify the raw SEC receipts:

| Vault Section | What It Contains & How to Use It |
| :--- | :--- |
| **Sections 1–3: Income Statement, Balance Sheet & Cash Flow Statement** | Rolling **5-Year Annual History + TTM** alongside the **6 Most Recent Discrete Quarters** (`Q1/Q2/Q3/Q4`). Every cell carries a data-integrity badge: clean number = `VERIFIED` direct XBRL tag; `*` = `DERIVED` via accounting identity (e.g., Q4 = FY - (Q1 + Q2 + Q3)); `NR` = Not Reported in filing. |
| **Section 4: Share Count & Tangible Book Value** | Tracks `Cover_Page_Shares_Outstanding` (`dei:EntityCommonStockSharesOutstanding` printed on Page 1 of the 10-K/10-Q) vs. `Diluted_Shares_Outstanding` to expose employee option overhang, plus exact Goodwill and Intangible deductions. |
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
* The engine accepts an `as_of_date` parameter (e.g. `build_statements(facts_df, as_of_date="2024-06-30")`).
* Historical XBRL records are strictly lagged by their verified SEC filing date (`filed <= as_of_date`), rather than the fiscal period end date. Financial data that had not yet been filed with the SEC as of the test date is completely excluded.

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
* **Normal Volatility (15 ≤ VIX ≤ 25):** Standard 3-tranche ladder execution is appropriate.
* **Elevated Volatility Caution (25 < VIX ≤ 35):** Options market makers typically operate in negative gamma positioning (though modern electronic retail-to-retail facilitation often dampens directional hedging flow). Bid-ask spreads widen and slippage increases; caution advised on market orders, recommending patient discount limit bids.
* **Crisis / Dislocation (VIX > 35):** Severe market panic creates asymmetric deep-value opportunities (Buffett: "Be greedy when others are fearful"); deploy strictly via deep limit order ladders beneath the tape.

---

## 🛠️ Quick Operator Commands for SSR v2

| Task | Command / Shortcut |
| :--- | :--- |
| **Interactive Double-Click Launcher** | Double-click [`Run_Executive_Card.command`](file:///Users/robertjenkins/.gemini/antigravity/scratch/logic-engines/Run_Executive_Card.command) and type one or more tickers (e.g., `STRT NRDS GME`). |
| **CLI Single or Multi-Ticker Run + Web Publish** | `python3 run_ssr_v2.py STRT UEIC --publish` |
| **Custom Position Size Override** | `python3 run_ssr_v2.py STRT --position-usd 5000` |
| **Batch Refresh All Published Cards (Dynamic Discovery)** | `python3 scripts/batch_refresh_all_cards.py --push` (automatically discovers & updates all 34+ `{TICKER}.md` cards in `Single_Stock_Web`, including ad-hoc single stock scans) |

---

*Antigravity V3 Core | SSR v2 Executive Engine Master Curriculum*
