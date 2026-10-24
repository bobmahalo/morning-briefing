# 🎓 The Antigravity SSR v2 Executive Engine: Master Architecture & Forensic Curriculum
**Document:** Institutional Single-Stock Operating Manual & Forensic Companion  
**System:** Antigravity V3 Core — Second-Rail Executive Single Stock Engine (`SSR v2`)  
**Primary Modules:** `reporting/ssr_executive.py` | `run_ssr_v2.py` | `reporting/ssr_report.py`  
**Methodology:** Zero Discretion | Adversarial XBRL Accounting | Deterministic 3-Tranche Execution  

[☕ Daily Morning Briefing](https://bobmahalo.github.io/morning-briefing/) | [🎓 Master Curriculum](https://bobmahalo.github.io/morning-briefing/CURRICULUM.html) | [🔬 SSR Executive Curriculum](https://bobmahalo.github.io/morning-briefing/SSR_CURRICULUM.html) | [🗂️ Single Stock Directory](https://bobmahalo.github.io/Single-Stock-Scan/)

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
│ • Asymmetric Payoff Box (Rx : 1.0 Reward-to-Risk vs. Hard Floor)        │
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
             │ Gate 1: Working Capital Liquidation OR         │
             │         Beneish M > -1.78 OR Altman Z < 1.81?  │
             └───────┬────────────────────────────────┬───────┘
                 YES │                                │ NO
                     ▼                                ▼
          🔴 TIER_QUARANTINED        ┌────────────────────────────────┐
          (Capped <= 1.0% Risk)      │ Gate 2: Share Price <= NCAV    │
                                     │         (Graham Net-Net)?      │
                                     └───────┬────────────────┬───────┘
                                         YES │                │ NO
                                             ▼                ▼
                                  🟡 TIER_2_NET_NETS   ┌──────────────────────────────┐
                                  (5% Sleeve | 1% Tgt) │ Gate 3: Piotroski >= 7 AND   │
                                                       │ FCF Yield >= 10% AND         │
                                                       │ Structural Operating Cash?   │
                                                       └──────┬───────────────┬───────┘
                                                          YES │               │ NO
                                                              ▼               ▼
                                                   🟢 TIER_1_COMPOUNDERS  🔵 TIER_3_TURNAROUNDS
                                                   (65% Sleeve | 5.5% Tgt) (If FCF >= 8% or Cluster Buy;
                                                                            20% Sleeve | 2.8% Tgt)
```

### Portfolio Sleeve & Per-Ticker Risk Budgeting (`strategies/position_sizing_and_execution.py`)

| Archetype Badge | Tier Key | Sleeve Target | Per-Stock Target ($100k Book) | Hard Risk Ceiling | Economic Rationale & Time Horizon |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **🟢 CORE STRUCTURAL OPERATING COMPOUNDER** | `TIER_1_COMPOUNDERS` | `65.0%` | `5.5%` (`$5,500`) | `7.0%` | Cash comes from genuine operating margins, net cash on the balance sheet, and share buybacks. **Time is your ally.** |
| **🔵 MICRO-TURNAROUND & VALUE CATALYST** | `TIER_3_TURNAROUNDS` | `20.0%` | `2.8%` (`$2,800`) | `3.5%` | Beaten-down cyclical or turnaround with $\ge 8\%$ FCF yield or verified C-Suite Form 4 cluster buying. |
| **🟡 BENJAMIN GRAHAM NET-NET ARBITRAGE** | `TIER_2_NET_NETS` | `5.0%` | `1.0%` (`$1,000`) | `1.5%` | Classic *cigar butt* trading below Net Current Asset Value ($\text{Price} \le \text{NCAV}$). Because operations may be shrinking, **time is your enemy**—diversify in small $1\%$ positions and sell at NCAV/TBV re-rating. |
| **🔴 QUARANTINED / ACCOUNTING MIRAGE RISK** | `TIER_QUARANTINED` | `0%` (Excluded) | `≤ 1.0%` (`≤ $1,000`) | `1.0%` | Looks optically cheap, but positive cash flow is a mirage from inventory liquidation, stretched payables, earnings manipulation ($M > -1.78$), or distress ($Z < 1.81$). |
| **💵 U.S. T-BILLS / DRY POWDER FLOOR** | `CASH_RESERVE` | `10.0%+` | Baseline + Unfilled Sleeve | `100.0%` | Under **Tobin's Separation Theorem**, any unfilled sleeve capital remains in 4.5% U.S. T-Bills rather than over-concentrating surviving picks. |

---

## 2. The Asymmetric Payoff Profile Box ($R\text{x} : 1.0$ Expectancy)

Right below the archetype pill sits the monospaced **Asymmetric Payoff Profile Box**:

```text
┌──────────────────────────────────────────────────────────────────────────────┐
│                 VERDICT: CORE STRUCTURAL OPERATING COMPOUNDER                │
├──────────────────────────────────────────────────────────────────────────────┤
│ ASYMMETRIC PAYOFF PROFILE: 3.4x : 1.0 (High Asymmetry >2.5x)*                │
│ • Downside to Net Cash Floor:        -18.2% ($22.50 vs $27.50)*              │
│ • Upside to Intrinsic Fair Value:    +61.8% ($44.50 Target 1)                │
│ • Catalytic Convergence Target:      +95.0% ($53.63 Target 2)                │
└──────────────────────────────────────────────────────────────────────────────┘
```

### A. How the Fundamental Downside Floor ($F_{\text{down}}$) Is Selected
The engine never invents arbitrary technical support levels. It selects the highest-priority **positive balance-sheet or cash-flow backstop** in this exact order:
1. **Net Cash Floor:** $\frac{\text{Total Cash} - \text{Total Debt}}{\text{Diluted Shares}}$ *(Pure bank cash minus 100% of total debt)*
2. **Graham NCAV Floor:** $\frac{\text{Current Assets} - \text{Total Liabilities} - \text{Preferred Stock}}{\text{Diluted Shares}}$ *(Strict liquidation value)*
3. **Tangible Book Floor:** $\frac{\text{Total Equity} - \text{Goodwill} - \text{Intangibles}}{\text{Diluted Shares}}$ *(Hard physical net worth)*
4. **Zero-Growth DCF Floor:** $\frac{\text{TTM FCF} / 0.10}{\text{Diluted Shares}}$ *(Perpetuity value at a 10% discount rate assuming 0% growth forever)*
5. **No Hard Balance-Sheet Floor (`N/A — Franchise Operating Moat`):** Triggered when a high-ROIC compounder carries net debt and negative tangible equity due to decades of share buybacks (e.g., AutoZone/Domino's model).

### B. The Reward-to-Risk Formula ($R\text{x} : 1.0$)
$$\text{Downside \%} = \left( \frac{F_{\text{down}} - P_{\text{spot}}}{P_{\text{spot}}} \right) \times 100$$
$$\text{Target 1 Upside \%} = \left( \frac{P_{\text{Target 1}} - P_{\text{spot}}}{P_{\text{spot}}} \right) \times 100$$
$$\text{Asymmetry Ratio } (R\text{x}) = \frac{\text{Target 1 Upside \%}}{|\text{Downside \%}|}$$

* **💎 High Asymmetry ($\ge 2.5\text{x} : 1.0$):** Upside to conservative Target 1 is at least $2.5\times$ the distance to the hard liquidation floor.
* **⚖️ Moderate Asymmetry ($1.0\text{x} - 2.5\text{x} : 1.0$):** Positive mathematical expectancy; requires strict 3-tranche sizing discipline.
* **⚠️ Unfavorable Skew ($< 1.0\text{x} : 1.0$):** Liquidation downside exceeds upside to Target 1.
* **🚨 Pure Cash Arbitrage Cushion ($\text{Downside \%} \ge 0\%$):** When spot price trades *below* the Net Cash or NCAV floor ($F_{\text{down}} \ge P_{\text{spot}}$), the ratio prints `>10.0x : 1.0` and automatically triggers an inline **Audit Check**:
  > `• AUDIT CHECK: Spot < Cash Floor. Verify debt & burn in Vault before sizing.`
  *(Why? Because in micro-caps, a stock trading below net cash is either a rare net-net anomaly or an unpopulated XBRL debt tag that must be verified in Level 3 before risking a dollar).*

---

## 3. The 3-Pillar Convergence Factor Card (`models/convergence_radar.py`)

The 3-Pillar Convergence Card condenses 10 forensic dimensions into three $0\text{–}10$ visual meters (`🟩` for $7\text{–}10$, `🟨` for $4\text{–}6$, `🟥` for $0\text{–}3$):

### Pillar 1: 🛡️ Financial Health ($0\text{ to }10\text{ Points}$)
Tests whether the balance sheet is solvent and the accounting is honest:
$$\text{Health Score} = \text{round}\Big( \underbrace{\frac{\text{Piotroski}}{9} \times 5.0}_{\text{Max } 5.0\text{ pts}} + \underbrace{\text{Altman Pts}}_{\text{Max } 3.0\text{ pts}} + \underbrace{\text{Beneish Pts}}_{\text{Max } 2.0\text{ pts}} \Big)$$

| Component | Max Points | Exact Scoring Rule |
| :--- | :---: | :--- |
| **Piotroski F-Score ($0\text{–}9$)** | `5.0 pts` | Proportional: $\left(\frac{F}{9}\right) \times 5.0$ (e.g., $8/9 = 4.44\text{ pts}$; $9/9 = 5.0\text{ pts}$). |
| **Altman Z-Score** | `3.0 pts` | `3.0 pts` if $Z \ge 3.0$ (Safe Zone)<br>`1.5 pts` if $1.81 \le Z < 3.0$ (Grey Zone)<br>`0.0 pts` if $Z < 1.81$ (Bankruptcy Distress Zone) |
| **Beneish M-Score** | `2.0 pts` | `2.0 pts` if $M \le -1.78$ (Clean Accruals)<br>`0.0 pts` if $M > -1.78$ (Earnings Manipulation Alert) |

* **⚠️ Bank / REIT Exception Gate (`is_financial_or_reit`):** If the company's SEC SIC code falls in Banking, Insurance, or Real Estate (`SIC 6000–6799`), standard manufacturing working-capital and leverage ratios ($Z$-Score and Piotroski) produce false distress signals. The card explicitly flags `⚠️ N/A (Bank/REIT Structure)*` so you never misapply industrial debt formulas to a depository bank.

### Pillar 2: 💎 Valuation Asymmetry ($0\text{ to }10\text{ Points}$)
Tests how much cash flow and liquid asset backing you receive per dollar paid:
$$\text{Valuation Score} = \text{FCF Yield Pts (0–4)} + \text{Net Cash/Price Pts (0–3)} + \text{NCAV/Price Pts (0–3)}$$

| Component | Max Points | Exact Scoring Tiers |
| :--- | :---: | :--- |
| **TTM FCF Yield ($\frac{\text{FCF}}{\text{Mkt Cap}}$)** | `4.0 pts` | $\ge 20.0\% \to \mathbf{4\text{ pts}}$<br>$12.0\%\text{–}19.9\% \to \mathbf{3\text{ pts}}$<br>$8.0\%\text{–}11.9\% \to \mathbf{2\text{ pts}}$<br>$4.0\%\text{–}7.9\% \to \mathbf{1\text{ pt}}$<br>$< 4.0\% \to \mathbf{0\text{ pts}}$ |
| **Net Cash / Share Price** | `3.0 pts` | $\ge 50.0\% \to \mathbf{3\text{ pts}}$<br>$25.0\%\text{–}49.9\% \to \mathbf{2\text{ pts}}$<br>$10.0\%\text{–}24.9\% \to \mathbf{1\text{ pt}}$<br>$\le 0\% \text{ (Net Debt)} \to \mathbf{0\text{ pts}}$ |
| **Graham NCAV / Share Price** | `3.0 pts` | $\ge 100.0\% \text{ (Net-Net)} \to \mathbf{3\text{ pts}}$<br>$70.0\%\text{–}99.9\% \to \mathbf{2\text{ pts}}$<br>$40.0\%\text{–}69.9\% \to \mathbf{1\text{ pt}}$ |

### Pillar 3: 🏛️ Capital Discipline ($0\text{ to }10\text{ Points}$)
Tests whether management treats shareholders as partners or as an ATM:
$$\text{Discipline Score} = \text{Share Change Pts (0–4)} + \text{Insider Cluster Pts (1–4)} + \text{Capex Maintenance Pts (0–2)}$$

| Component | Max Points | Exact Scoring Tiers |
| :--- | :---: | :--- |
| **1-Year Share Count Change** | `4.0 pts` | $\le -5.0\% \text{ (Aggressive Cannibal)} \to \mathbf{4\text{ pts}}$<br>$-1.0\%\text{ to }-4.9\% \text{ (Buybacks)} \to \mathbf{3\text{ pts}}$<br>$-0.9\%\text{ to }+1.0\% \text{ (Stable)} \to \mathbf{2\text{ pts}}$<br>$> +1.0\% \text{ (Dilution)} \to \mathbf{0\text{ pts}}$ |
| **C-Suite Form 4 Cluster Buying** | `4.0 pts` | `4.0 pts` if verified C-Suite open-market cluster buying (`Code P`)<br>`1.0 pt` baseline if quiet (0 cluster buys) |
| **Maintenance Capex Health** | `2.0 pts` | `2.0 pts` if $\frac{\text{CapEx}}{\text{D\&A}} \ge 0.35$<br>`0.0 pts` if Capex Starvation detected ($\frac{\text{CapEx}}{\text{D\&A}} < 0.35$) |

* **⚠️ Dilutive Burn Trap Catch (`is_dilutive_burn`):** If a company has negative or zero Operating Cash Flow ($\text{OCF} \le \$0$) while issuing positive Stock-Based Compensation ($\text{SBC} > \$0$), dividing SBC by negative OCF produces a meaningless negative percentage. The engine catches this and prints **`⚠️ Dilutive Burn (OCF ≤ $0)*`**—exposing that management is paying themselves in stock while the business burns cash.

---

## 4. Deterministic 3-Tranche Limit Order Ladder & Valuation Exits

### A. The 3-Tranche Accumulation Ladder (`build_3_tranche_ladder`)
Never market-buy 100% of an allocation on day one. Every position is split into three mathematical tranches:

| Tranche | Order Type | Entry Price Formula | Weight | Tactical Purpose |
| :---: | :---: | :---: | :---: | :--- |
| **T1** | `MARKET / LIMIT` | $P_{\text{spot}}$ | `33.3%` | **Baseline Entry:** Establishes immediate skin in the game once the forensic audit passes; eliminates FOMO if the stock runs immediately. |
| **T2** | `GTC LIMIT` | $P_{\text{spot}} \times (1 - 0.060)$ (`-6.0%`) | `33.3%` | **Support Retest Bid:** Captures normal multi-week mean-reversion pullbacks and consolidation retests. |
| **T3** | `GTC LIMIT` | $P_{\text{spot}} \times (1 - 0.125)$ (`-12.5%`) | `33.4%` | **Capitulation Wick Bid:** Sits below thin small-cap order books to scoop cheap shares when retail stop-losses get swept during market flushes. |

* **Full-Fill Blended Cost Basis:** If all three tranches fill, your average cost basis is automatically lowered by **$-6.17\%$** below your initial entry price:
  $$P_{\text{avg}} = \frac{1.000 + 0.940 + 0.875}{3} \times P_{\text{spot}} = 0.9383 \times P_{\text{spot}}$$

### B. Archetype-Specific Deterministic Exit Rules (`build_deterministic_exit_rules`)
Exit targets adapt dynamically to the stock's archetype so you don't hold a decaying Net-Net like a Compounder:
1. **For Graham Net-Nets (`TIER_2_NET_NETS`):**
   * **Target 1 (Sell 50%):** $100\%$ of **Graham NCAV** (or $+35\%$ minimum re-rating).
   * **Target 2 (Sell 50%):** $100\%$ of **Tangible Book Value (TBV)** (or $+65\%$).
   * **Hard Stop:** Immediate exit if quarterly operating burn erodes $> 20\%$ of Net Current Assets.
2. **For Compounders & Turnarounds (`TIER_1` / `TIER_3`):**
   * **Target 1 (Scale 33%):** Intrinsic fair-value re-rating (**$+30.0\%$** to **$+40.0\%$** or 12x–15x FCF).
   * **Target 2 (Scale 33%):** Full historical multiple expansion (**$+65.0\%$** to **$+80.0\%$**).
   * **Hard Stop:** Structural thesis break ($-15\%$ to $-20\%$ with 2 consecutive quarters of negative OCF).
3. **Universal Retail Exit Liquidity Trigger:**
   * If 30-day volume surges to **$\ge 3.0\times$ normal ADDV** while price spikes into overhead resistance, sell $33\%\text{–}50\%$ directly into retail breakout FOMO.

---

# MODULE 2: Level 2 — The 30-Second Plumber's Diagnosis

If a stock survives Level 1, Level 2 takes **30 seconds** to inspect the internal corporate plumbing across 7 forensic sections.

---

## Section 1: The Cash Flow Engine (`models/working_capital_audit.py`)

### Why Free Cash Flow Can Lie
Reported Operating Cash Flow ($\text{OCF}$) equals Net Income plus non-cash charges ($\text{D\&A}$, $\text{SBC}$) plus **Working Capital changes**:
$$\text{OCF} = \text{Net Income} + \text{D\&A} + \text{SBC} + \underbrace{(-\Delta\text{A/R}) + (-\Delta\text{Inventory}) + (+\Delta\text{A/P})}_{\text{Total Working Capital Cash Impact } (\Delta\text{WC}_{\text{cash}})}$$

A shrinking, dying retailer can lose money on every sale ($\text{Operating Income} < 0$), close stores, liquidate its warehouse inventory ($\Delta\text{Inventory} \ll 0$), stop paying suppliers ($\Delta\text{A/P} \gg 0$), and report a massive one-time spike in "Free Cash Flow."

### The 5 Deterministic Cash Origin Classifications

| Classification | Mathematical Trigger | Forensic Meaning |
| :--- | :--- | :--- |
| **`STRUCTURAL_OPERATING_EARNINGS`** | $\text{OCF} > 0, \text{EBIT} > 0, \text{NI} > 0$ **AND** $\Delta\text{WC}_{\text{cash}} < 0.50 \times \text{OCF}$ | **True Compounder Engine:** Cash flow is generated by profitable customer sales, not balance-sheet liquidation. |
| **`MIXED_EARNINGS_AND_WORKING_CAPITAL`** | $\text{OCF} > 0, \text{EBIT} > 0, \text{NI} > 0$ **AND** $\Delta\text{WC}_{\text{cash}} \ge 0.50 \times \text{OCF}$ | Core operations are profitable, but more than half of trailing cash flow came from temporary working capital release. |
| **`WORKING_CAPITAL_LIQUIDATION`** | $\text{OCF} > 0$ **WHILE** ($\text{EBIT} \le 0$ or $\text{NI} \le 0$) **AND** $\Delta\text{WC}_{\text{cash}} > 0$ | **🚨 The Liquidation Mirage Trap:** The business is unprofitable; positive cash flow is purely an artifact of destocking inventory, collecting old receivables, or stretching payables. Automatically triggers `TIER_QUARANTINED`. |
| **`DEPRECIATION_SHIELD_CASH_FLOW`** | $\text{OCF} > 0$ **WHILE** ($\text{EBIT} \le 0$ or $\text{NI} \le 0$) **AND** $\Delta\text{WC}_{\text{cash}} \le 0$ | GAAP earnings are negative due to heavy non-cash depreciation/amortization charges, keeping cash flow positive. |
| **`OPERATING_CASH_BURN`** | $\text{OCF} \le 0$ | Active cash drain from core operations. |

### The Maintenance Capex Starvation Check
$$\text{Capex-to-D\&A Ratio} = \frac{|\text{Capital Expenditures}|}{\text{Depreciation \& Amortization}}$$
* **Gate:** If $\frac{|\text{CapEx}|}{\text{D\&A}} < 0.35$, the engine flags **`⚠️ WARNING: Capex starved under 35% of D&A`**. Management is cannibalizing physical plant and equipment to artificially inflate short-term Free Cash Flow.

---

## Section 2: Balance Sheet Health & Debt Extinguishment Clock (`models/valuation.py`)

Instead of relying on static debt-to-equity ratios, the engine models **Synthetic Deleveraging**:
1. **Excess Cash Application:** First, apply 100% of balance-sheet cash and short-term investments against total short- and long-term debt:
   $$\text{Remaining Net Debt} = \max(0, \text{Total Debt} - \text{Total Cash})$$
2. **The Debt Extinguishment Clock:** How many years of current Trailing Twelve Month Free Cash Flow would it take to retire 100% of remaining net debt?
   $$\text{Debt Extinguishment Clock (Years)} = \frac{\text{Remaining Net Debt}}{\text{TTM Free Cash Flow}}$$
   * **$0.0\text{ Years}$ (Net Cash Surplus):** Total Cash exceeds Total Debt. Financial bankruptcy risk is near zero.
   * **$\le 3.0\text{ Years}$:** Rapid deleveraging capacity; interest-rate shock resistant.
   * **$> 5.0\text{ Years}$ (or `Infinite` when $\text{FCF} \le 0$):** High refinancing and credit-spread vulnerability.

---

## Section 3: 5-Year Cumulative Capital Allocation & Share Cannibalization

Single-year cash flows are noisy. Section 3 sums **5 full fiscal years of Operating Cash Flow ($\sum_{t=1}^5 \text{OCF}_t$)** and tracks every dollar management spent across five buckets:

$$\sum \text{OCF}_{5\text{Y}} = \text{CapEx}_{5\text{Y}} + \text{Buybacks}_{5\text{Y}} + \text{Dividends}_{5\text{Y}} + \text{Acquisitions}_{5\text{Y}} + \text{Retained Surplus}_{5\text{Y}}$$

### The 5 Capital Allocation Postures
* **💰 Cannibal & Cash Return Engine:** $\frac{\text{Buybacks}_{5\text{Y}} + \text{Dividends}_{5\text{Y}}}{\text{OCF}_{5\text{Y}}} \ge 50.0\%$. Management returns the majority of organic cash flow directly to owners.
* **🏰 Organic Fortress Builder:** $\frac{\text{Retained Surplus}_{5\text{Y}}}{\text{OCF}_{5\text{Y}}} \ge 40.0\%$. Management stockpiles cash on the balance sheet and pays down debt.
* **⚙️ Heavy Capital Reinvestment:** $\frac{\text{CapEx}_{5\text{Y}}}{\text{OCF}_{5\text{Y}}} \ge 50.0\%$. Heavy physical reinvestment into factories, fleet, or infrastructure.
* **⚖️ Balanced Capital Deployment:** Balanced split across CapEx, buybacks/dividends, and balance-sheet retention.
* **⚠️ Dilutive Cash Burn:** $\sum \text{OCF}_{5\text{Y}} \le 0$. Operations are cash-flow negative and subsidized by selling new stock (`Equity Issuance`) or borrowing (`Net Debt Flow`).

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
   * **💎 Deep Value Compression ($< 25\text{th %-tile}$):** Multiple is compressed into the bottom quartile of its 5-year history. Mean reversion to the 5-year median multiple provides significant upside without requiring heroic earnings growth.
   * **⚖️ Historical Fair Value ($25\text{th–}75\text{th %-tile}$):** Trading within normal historical bands.
   * **⚠️ Multiple Expansion ($> 75\text{th %-tile}$):** Historically expensive relative to its own 5-year baseline.

---

## Section 5: SIC Industry Peer Benchmarking & Relative Scale

Queries `master_universe.sqlite` (5,349 SEC operating companies) for the **top 3 competitors by Market Cap** sharing the exact same **4-digit SEC Standard Industrial Classification (`SIC`) code** (falling back to the 2-digit SIC group only if fewer than 3 companies exist in the 4-digit niche):
* Assigns relative scale badges:
  * `[Industry Leader: Nx larger]` (Peer is $\ge 2.5\times$ the subject company's market cap)
  * `[Direct Peer: ~Nx]` ($0.4\times \text{ to } 2.5\times$ market cap)
  * `[Smaller Peer: Nx]` ($< 0.4\times$ market cap)
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

Compares the recent 20-trading-day average volume against the 90-trading-day baseline:
$$\text{Volume Ratio} = \frac{\text{Mean Volume}_{20\text{d}}}{\text{Mean Volume}_{90\text{d}}}$$
* **$\le 1.10\times$ (`PASS — Silent Accumulation Bonus +1`):** Volume is dry and quiet. Institutions can accumulate via passive limit orders without retail mania.
* **$1.11\times \text{ to } 2.49\times$ (`NEUTRAL`):** Normal two-way turnover.
* **$\ge 2.50\times$ (`CAUTION — Retail Exit Liquidity Warning -1`):** Volume has spiked $\ge 2.5\times$ above normal. High risk of chasing a retail hype spike; do not initiate fresh market buys.

---

# MODULE 3: Level 3 — Complete SEC EDGAR Financial Statements & Audit Vault

Hidden behind a collapsible `<details>` drawer at the bottom of every Executive Card is the complete, unedited **10-Section SSR v1 Forensic Audit Vault** (`reporting/ssr_report.py`). Whenever a number in Level 1 or Level 2 looks too good to be true, open Level 3 to verify the raw SEC receipts:

| Vault Section | What It Contains & How to Use It |
| :--- | :--- |
| **Sections 1–3: Income Statement, Balance Sheet & Cash Flow Statement** | Rolling **5-Year Annual History + TTM** alongside the **6 Most Recent Discrete Quarters** (`Q1/Q2/Q3/Q4`). Every cell carries a data-integrity badge: clean number = `VERIFIED` direct XBRL tag; `*` = `DERIVED` via accounting identity (e.g., $\text{Q4} = \text{FY} - (\text{Q1}+\text{Q2}+\text{Q3})$); `NR` = Not Reported in filing. |
| **Section 4: Share Count & Tangible Book Value** | Tracks `Cover_Page_Shares_Outstanding` (`dei:EntityCommonStockSharesOutstanding` printed on Page 1 of the 10-K/10-Q) vs. `Diluted_Shares_Outstanding` to expose employee option overhang, plus exact Goodwill and Intangible deductions. |
| **Section 5: Multi-Horizon Growth (`5Y/10Y/15Y CAGR`) & Common-Size Statements** | Computes 5-year, 10-year, and 15-year CAGRs across Revenue, EBIT, Net Income, OCF, FCF, TBV, and Diluted Shares, followed by **Common-Size Income Statement (`% of Revenue`)** and **Common-Size Balance Sheet (`% of Total Assets`)** to spot margin expansion or inventory/receivables bloat at a glance. |
| **Section 6: Financial Ratios & `5Y/10Y` Return on Capital Consistency** | Tracks Gross, Operating, Net, and FCF margins, Current/Quick ratios, Debt/Equity, Net Debt/EBITDA, and **`5Y/10Y Median vs. Min (Trough)`** for `ROIC`, `ROCE`, and `ROE`—showing how the business performed in its worst historical year. |
| **Section 7: Quantitative Forensics & Serial Roll-Up Dilution Audit** | Full breakdown of Piotroski ($0\text{–}9$), Altman $Z$, Beneish $M$, SBC % of OCF, and the **Serial Acquirer Roll-Up Trap Audit** (flags companies where 5-year M&A spending exceeds $50\%$ of 5-year FCF while Goodwill + Intangibles bloat above $40\%$ of Total Assets). |
| **Section 8: Roaring Kitty Inverted Yields, Synthetic Deleveraging & Reverse DCF** | Displays valuation multiples as **Inverted Yields** (`FCF/P`, `E/P`, `TBV/P`, `Sales/P`, `EBIT/EV`, `FCF/EV` — where higher % = cheaper stock), the Synthetic Deleveraging table, and a **Reverse DCF** ($r = 10\%, g_{\text{term}} = 2.5\%$) solving for the **Implied 10-Year FCF CAGR** currently priced into the stock. |
| **Section 9: Plain-English Metric Guide & Ownership Tables** | Multi-year `10-K Item 5` transfer agent record holder table (with verbatim sentences from each 10-K) and the complete `Form 4` insider transaction log. |
| **Section 10: SEC EDGAR Provenance Appendix** | Line-by-line audit table listing every canonical field, its latest period end date, status (`VERIFIED` / `DERIVED`), the **exact US-GAAP XBRL tag**, the **SEC Accession Number**, and the **Filing Date**. |

---

## 🛠️ Quick Operator Commands for SSR v2

| Task | Command / Shortcut |
| :--- | :--- |
| **Interactive Double-Click Launcher** | Double-click [`Run_Executive_Card.command`](file:///Users/robertjenkins/.gemini/antigravity/scratch/logic-engines/Run_Executive_Card.command) and type one or more tickers (e.g., `STRT NRDS GME`). |
| **CLI Single or Multi-Ticker Run + Web Publish** | `python3 run_ssr_v2.py STRT UEIC --publish` |
| **Custom Position Size Override** | `python3 run_ssr_v2.py STRT --position-usd 5000` |
| **Batch Refresh All 26 Published Cards** | `python3 scripts/batch_refresh_all_cards.py` |

---

*Antigravity V3 Core | SSR v2 Executive Engine Master Curriculum*
