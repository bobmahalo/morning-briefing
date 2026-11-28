# 📘 The Antigravity Tactical Dip & Pullback Radar: Master Architecture & Regime Curriculum
**Document:** Institutional Operating Manual & Dry-Powder Deployment Companion  
**System:** Antigravity V3 Core — Read-Only Macro Pullback & Liquidity Firewall Overlay  
**Primary Modules:** `ingestion/tactical_dip_data.py` | `models/tactical_dip_model.py` | `strategies/tactical_dip_engine.py` | `reporting/tactical_dip_report.py`  
**Methodology:** Strict Read-Only Liquidity Firewall | Confirmation-Heavy Scaling | Credit-First Vetoes | Zero Synthetic Fallbacks  

[☕ Daily Morning Briefing](https://bobmahalo.github.io/morning-briefing/) | [📈 $100K Model Portfolio](https://bobmahalo.github.io/morning-briefing/PORTFOLIO.html) | [🎯 Tactical Dip Radar](https://bobmahalo.github.io/morning-briefing/TACTICAL_DIP.html) | [🗂️ Single Stock Directory](https://bobmahalo.github.io/Single-Stock-Scan/)  
[🎓 Master Curriculum](https://bobmahalo.github.io/morning-briefing/CURRICULUM.html) | [🔬 SSR Executive Curriculum](https://bobmahalo.github.io/morning-briefing/SSR_CURRICULUM.html) | [📘 Tactical Dip Curriculum](https://bobmahalo.github.io/morning-briefing/TACTICAL_CURRICULUM.html) | [🗄️ Open SEC Data Lake](https://bobmahalo.github.io/morning-briefing/DATA_LAKE.html)

> **🏛️ True Stock Ownership & Custody Education:** Holding shares in broker "Street Name" means you only hold a beneficial entitlement while Cede & Co. holds legal title. Learn how Direct Registration (DRS) protects your shares from broker insolvency and short-lending at **[WhyDRS.org](https://www.whydrs.org)** ([Advocacy](https://www.whydrs.org/advocacy) | [Free Resources](https://www.whydrs.org/free-resources)).

> **Disclaimer:** *This curriculum is for educational and quantitative research purposes only and does not constitute financial advice. The author is not a licensed financial advisor. All investments carry risk, and you should conduct your own due diligence before making any financial decisions.*

---

## 🏛️ Executive Philosophy: Solving Dry-Powder Paralysis Without Contaminating Single-Stock Alpha

When disciplined deep-value screens find only a handful of operating businesses trading at wide margins of safety, a systematic portfolio naturally accumulates substantial Treasury money-market dry powder. During broad market air-pockets, volatility spikes, or sovereign-debt scares, two opposite behavioral errors tend to dominate:

1. **Premature Heroism (Catching Wave 1):** Deploying excess cash on the first sharp red candle or initial `VIX` spike, only to absorb a deeper Wave 2 liquidation once credit spreads widen or dealer option hedges unpin.
2. **Perpetual Paralysis (Missing Structural Reclaims):** Keeping `100%` of unencumbered excess liquidity idle through the entire repair cycle because no deterministic pre-committed rules exist for broad index (`SPY`) or monetary metal (`GLDM` / `GLD`) pullbacks.

The **Antigravity Tactical Dip & Pullback Radar** addresses both failure modes as a **strictly read-only overlay** (`mode=ro` against `portfolio_tracker.sqlite`). It enforces two structural boundaries:

- **Zero Accounting Contamination:** Engine 1 (`Yield Stacker` CSPs) and Engine 3 (`$100K` Deep-Value Single-Stock Ledger) remain untouched. Single-stock telemetry, sleeve caps, and pending `T2`/`T3` limit orders are protected first before a single dollar is budgeted to tactical sleeves.
- **Probabilistic Restraint (`Practitioner_Front_Man` Leads, `Formal_Backstop` Vetoes):** Every deployment directive (`READY`, `LOCKED`, `VETOED`, `TRIM_ALERT`) is anchored to observable volatility term structure, corporate credit spreads, weekly institutional moving averages, and session liquidity — expressed in base-rate probabilities rather than bottom-calling certainty.

```text
                    TACTICAL DIP & PULLBACK RADAR TOPOLOGY
┌────────────────────────────────────────────────────────────────────────────┐
│ LAYER 1: READ-ONLY INGESTION (ingestion/tactical_dip_data.py)              │
│ • portfolio_tracker.sqlite (SQLite URI mode=ro — zero write permission)    │
│ • 10 Yahoo Finance OHLCV series (SPY, QQQ, IWM, GLD, GLDM, GC=F, GDX,      │
│   DX-Y.NYB, ^VIX, ^VIX3M) + local cache fallback (zero synthetic bars)     │
│ • Macro Vitals (HY OAS, CCC OAS, 10Y TIPS Real Yield, Fed Dir, FINRA Debt) │
└─────────────────────────────────────┬──────────────────────────────────────┘
                                      │
                                      ▼
┌────────────────────────────────────────────────────────────────────────────┐
│ LAYER 2: PURE QUANT MODELS (models/tactical_dip_model.py)                  │
│ • Unencumbered Cash Waterfall (Cash - Tobin Floor - Pending Engine 3 Buys) │
│ • Daily/Weekly Technicals (200D SMA, 100W SMA, 200W SMA, Fast 200D Break)  │
│ • Vol/Credit/OpEx Calendar (VIX/VIX3M, Holiday Half-Days, Dec→Jan Unpin)   │
│ • Gold Microstructure (100W SMA, DXY/TIPS/GDX Dual-Ratio, 2013 Trap Check) │
└─────────────────────────────────────┬──────────────────────────────────────┘
                                      │
                                      ▼
┌────────────────────────────────────────────────────────────────────────────┐
│ LAYER 3: DETERMINISTIC STATE MACHINE (strategies/tactical_dip_engine.py)   │
│ • Formal Backstop Vetoes: Missing Data, Holiday/Thin Book, HY >= 400 bps,  │
│   VIX/VIX3M >= 1.05 Backwardation                                          │
│ • Sleeve 1: SPY Patient Confirmation-Heavy (20% T1 / 50% T2 / 30% T3)      │
│ • Sleeve 2: Gold Regime-Gated 2-Step (25% Scout / 75% Confirmed Scale)     │
│ • Sleeve 3: Volatility, Credit & Cross-Index Regime Monitor (Indicator)    │
└─────────────────────────────────────┬──────────────────────────────────────┘
                                      │
                                      ▼
┌────────────────────────────────────────────────────────────────────────────┐
│ LAYER 4: ATOMIC REPORTING & WEB SYNC (reporting/tactical_dip_report.py)    │
│ • Auto-refreshed & dual-published by Option 2 (reconcile_portfolio.py)     │
│ • Embedded Dry-Powder Waterfall Bridge in PORTFOLIO.html                   │
│ • Full standalone dashboard at TACTICAL_DIP.html (fault-isolated)          │
└────────────────────────────────────────────────────────────────────────────┘
```

---

# MODULE 1: The Unencumbered Liquidity Firewall & `50 / 35 / 15` Capital Stack

## 1. Preventing Double-Counting of Dry Powder

A common portfolio-accounting error is treating raw brokerage cash as freely deployable when open Good-Til-Canceled (`GTC`) limit orders already have a claim on that liquidity. If Engine 3 holds pending `T2` retest and `T3` flush limit orders on single-stock positions, spending that cash on an index pullback risks starving the core single-stock ladders precisely when volatility triggers their fills.

The radar therefore computes **Truly Unencumbered Cash** via a strict read-only waterfall:

$$\text{Hard Floor} = \max\!\left(\$10{,}000.00,\; 0.10 \times \text{Total NAV}\right)$$

$$\text{Pending Engine 3 Encumbrance} = \sum_{i \in \text{PENDING BUY}} \left(\text{Target Price}_i \times \text{Target Shares}_i\right)$$

$$\text{Unencumbered Cash} = \max\!\left(0,\; \text{Live Cash Balance} - \text{Hard Floor} - \text{Pending Engine 3 Encumbrance}\right)$$

Only `PENDING` orders on the `BUY` side encumber cash (`FILLED` orders are already deducted from cash, and `PENDING SELL` targets generate liquidity rather than consuming it).

## 2. The Toe-Dip Capital Split (`50% / 35% / 15%`)

Once truly unencumbered cash is isolated, it is partitioned into three non-overlapping pools:

| Pool | Share of Unencumbered Cash | Deployment Structure | Economic Purpose |
| :--- | :---: | :--- | :--- |
| **Shopping-Spree Dry Powder Reserve** | **`50.0%`** | Held strictly liquid in Treasury / MMF sweep | Optionality reserve for severe single-stock dislocations or systemic washouts (`^VIX >= 40` / `HY OAS > 500 bps`) |
| **Sleeve 1: Broad Index (`SPY`)** | **`35.0%`** | `20%` `T1` Scout / `50%` `T2` Core Confirmation / `30%` `T3` Reserve | Captures broad equity drawdowns while weighting core capital toward confirmed trend repair |
| **Sleeve 2: Hard Assets (`GLDM` / `GLD`)** | **`15.0%`** | `25%` Scout Cap below `100W SMA` / `75%` Confirmed Scale above `100W SMA` | Hedge against real-yield compression, sovereign fiscal stress, or dollar trend breaks |

Keeping `50%` of even the *unencumbered* excess pool untouched ensures that an investor maintains meaningful buying power if an orderly `-7%` pullback evolves into a deeper credit-cycle liquidation.

---

# MODULE 2: Sleeve 1 — Broad Index (`SPY`) Patient Confirmation-Heavy (`20% / 50% / 30%`)

## 1. Historical Base Rates Behind Confirmation-Heavy Scaling

Buying aggressively on the first day volatility spikes has a historically skewed risk profile:

- **First `^VIX > 35` Closes (`n = 15` episodes since `1990`):** Immediate entry carried a median subsequent drawdown of roughly `-8.0%`, with severe left-tail regimes extending much further (`-24.9%` in `2020`; `-41.5%` in `2008`). Waiting for volatility de-escalation (`^VIX < 30` and at least `-40%` off its trailing 60-day spike peak) materially reduced drawdown severity at an approximate `7.7%–9.0%` opportunity cost during sharp V-shaped rebounds.
- **Fast `> 5.5%` Breaks Below the `200D SMA` (`<= 5` Trading Sessions):** When broad indexes slice more than `5.5%` below their `200`-day simple moving average within five sessions (e.g., `1987`, `1998`, `2011`), historical repair back above the `200D SMA` required `18` to `161` trading days. The model flags this condition (`fast_200d_break_flagged`) as a patience reminder against assuming instant recovery.
- **Confirmation Drag vs. Wave 2 Survival:** Requiring a full-liquidity weekly close back above the `200D SMA` for the bulk `50%` core tranche introduces an estimated `~2%` entry lag on broad indexes, in exchange for filtering out counter-trend bear-market rallies that fail at moving-average resistance.

## 2. Tranche Unlock Rules (`T1 / T2 / T3`)

| Tranche | Weight | Reference Price | Unlock Conditions (`READY`) | Active Vetoes (`VETOED`) |
| :--- | :---: | :---: | :--- | :--- |
| **`T1` Scout** | **`20%`** | Spot `SPY` | Full-liquidity session **AND** (`^VIX` de-escalation confirmed: 60D peak `>= 35`, spot `< 30`, `>= 40%` off peak **OR** Friday weekly close defending `>= 100W SMA` within `+3.0%`) | Missing core data, holiday half-day / `< 0.60x` vol, `HY OAS >= 400 bps`, or `VIX/VIX3M >= 1.05` |
| **`T2` Core Confirmation** | **`50%`** | `200D SMA` | Full-liquidity **Friday weekly close** strictly above `SPY` `200D SMA` (`weekly_close > sma_200d`) | Missing core/SMA data, holiday half-day / `< 0.60x` vol, or `HY OAS >= 400 bps` |
| **`T3` Wave-2 / Backtest** | **`30%`** | `100W SMA` (below `200D`) or `200D SMA` (reclaimed) | **Either** Wave-2 capitulation flush (`^VIX >= 35` with `SPY <= 1.01 × 100W SMA`) **OR** post-reclaim backtest holding `+0%` to `+2.0%` above `200D SMA` (with benign credit & full liquidity) | Missing core data (Note: Wave-2 flush is intentionally allowed to surface during high vol near `100W SMA` as a capitulation watch) |

## 3. Structural `T1` Invalidation (Avoiding Daily Whipsaws)

Broad index ETFs exhibit substantial intraday noise during elevated-volatility regimes, making tight daily stop-losses structurally prone to whipsaw exits. Accordingly, the `20%` `T1` scout carries **no tight daily stop**. Structural invalidation triggers **only** when both trend and credit confirm systemic deterioration simultaneously:

$$\text{T1 Invalidation} \iff \left(\text{SPY Weekly Close} < \text{100W SMA}\right) \;\land\; \left(\text{US HY OAS} > 450\text{ bps}\right)$$

Once `SPY` reclaims its `200D SMA` on a weekly basis, the sleeve transitions to a long-horizon core hold posture.

---

# MODULE 3: Sleeve 2 — Hard Assets & Gold (`GLDM` / `GLD`) Regime-Gated 2-Step (`25% / 75%`)

## 1. The `100`-Week SMA Institutional Cost Basis

Gold frequently experiences multi-month or multi-year digestion cycles after strong parabolic advances. The **`100`-week simple moving average** (~2 years of weekly closes) approximates the rolling medium-term institutional cost basis:

- **Step 1 Scout (`25%` Cap below `100W SMA`):** Permits a disciplined starter allocation beneath the `100W SMA`, netting out any locally supplied existing scout value (`--gold-held-usd` in local Option `8` runs; strictly `$0.00` on public `$100K` web publishes).
- **Step 2 Confirmed Scale (`75%` Remainder):** Remains `LOCKED` until **both** conditions are satisfied simultaneously:
  1. Weekly close strictly above the `100W SMA` (`GLD` primary, `GC=F` fallback), **AND**
  2. At least **`2` of `3`** independent macro and miner-leadership confirmations pass.

## 2. The `2-of-3` Macro & Dual-Ratio Confirmation Gate

| Confirmation Check | Quantitative Threshold | Economic Rationale |
| :--- | :---: | :--- |
| **1. Dollar Headwind Easing** | `DXY < 200W SMA` | Broad USD weakness below its rolling ~4-year mean removes the primary FX translation headwind on bullion. |
| **2. Real Yield Stabilization** | `10Y TIPS` 30D delta `<= 0 bps` | Gold carries zero nominal coupon; falling or stabilizing real Treasury yields reduce the opportunity cost of holding physical metal. |
| **3. Dual Miner Leadership** | `GDX / GLD > 0.216` **AND** `GDX / SPY` 20D change `> 0%` | Gold mining equities are high-beta operating claims on bullion margins. Requiring miners to hold structural support against bullion **and** outperform broad equities over 20 sessions filters out fragile metal-only bounces. |

## 3. The `2013` Secular Rotation Trap & Structural Box Floor (`TRIM_ALERT`)

In `2013`, after gold broke below its `100W SMA`, bullion staged a `+20.7%` counter-trend rally while U.S. equities pushed to new highs — trapping investors who scaled aggressively beneath long-term trend resistance before a multi-year drawdown resumed.

The engine continuously monitors two defensive exit flags that shift both gold steps to **`🚨 TRIM ALERT`**:

1. **`2013` Secular Rotation Trap:** Triggered when `Gold < 100W SMA` **AND** the `Gold / SPY` relative-strength ratio is below its `100W` moving average **AND** `SPY` sits within `-5.0%` of its 52-week high (indicating capital rotating out of defensive bullion back into strong equities).
2. **Structural Box Floor Break:** Triggered on a weekly close below `$3,500/oz` on `GC=F` (or `~$322` equivalent on `GLD` if futures are unavailable).

## 4. Vehicle Selection & IRS Collectibles Tax Friction (`GLDM` vs. `GLD`)

Physical-bullion grantor trusts (`GLD`, `GLDM`) have two practical frictions that matter over multi-year holding horizons:

- **Expense-Ratio Bullion Dilution:** Grantor trusts sell a fraction of their underlying gold bar inventory periodically to pay management fees. `GLDM` (`0.10%` annual ER) reduces annual fee drag by `75%` relative to `GLD` (`0.40%` annual ER), making `GLDM` the default buy-and-hold execution ticker while `GLD` / `GC=F` supply deeper multi-year price history for `100W` SMAs.
- **IRS `28%` Collectibles Tax Rate:** In standard U.S. taxable brokerage accounts, gains on physically backed gold grantor trusts held longer than one year are taxed by the IRS as **collectibles** (up to **`28%`** maximum federal long-term capital gains rate vs. `20%` for qualifying common equities). Holding physical gold ETFs inside tax-advantaged accounts (IRA / Roth IRA) eliminates that `800 bps` federal tax wedge.

---

# MODULE 4: Sleeve 3 — Volatility, Credit, Holiday Microstructure & OpEx Plumbing

Sleeve 3 operates strictly as an **indicator and veto layer at v1**. Standalone volatility ETPs (`UVXY`, `VXX`, `SVIX`) are intentionally excluded from execution due to futures-curve contango decay (on long-vol products) and acute left-tail gap risk (on short-vol products).

## 1. Priority-1 Formal Backstop Vetoes

| Plumbing Gauge | Threshold / Band | Operational Impact | Why It Matters |
| :--- | :---: | :--- | :--- |
| **`^VIX / ^VIX3M` Term Structure** | `>= 1.05` (`BACKWARDATION_PANIC`) | **VETOES `SPY` `T1`** | Short-dated 30D implied vol trading meaningfully above 3-month vol reflects acute demand for immediate crash protection; equities frequently remain unstable until the term structure flattens (`< 1.05`). |
| **US High-Yield OAS (`HY OAS`)** | `>= 400 bps` entry veto; `> 450 bps` `T1` invalidation; `>= 500 bps` washout watch | **VETOES `SPY` `T1` & `T2`** | Corporate credit sits senior to equity in the capital structure. Widening high-yield spreads (`>= 400 bps`) signal tightening refinancing conditions where equity dip-buying faces elevated default and earnings-revision risk. |
| **Holiday Half-Days & Thin Volume** | NYSE half-day (`Black Friday`, `Jul 3`, `Dec 24`) **OR** `SPY` vol `< 0.60x` 20D avg | **VETOES `SPY` `T1` & `T2`** | Options market makers strip non-trading calendar days out of short-dated option implied volatility ahead of holidays, creating a mechanical `VIX` compression artifact that often resets higher on Monday's full-liquidity open. Thin books also invalidate moving-average reclaim signals. |

## 2. Contextual Regime Modifiers

- **OpEx Calendar Window (`Dec OpEx → Jan` Unpinning):** Between mid-November and mid-January, the radar highlights the next `VIXOpEx` (Wednesday 30 days prior to the following month's 3rd Friday), Monthly OpEx (3rd Friday), and Quarterly OpEx. Large year-end institutional collar and short-put dealer inventories can mechanically cushion downside into December OpEx before expiring and unpinning price discovery in January.
- **FINRA Margin Leverage (`Rule 4521(d)`):** Ratios `>= 3.00x` free credit balances indicate elevated retail and institutional margin leverage — not a timing trigger by itself (due to the ~3-week reporting lag), but an amplifier that can accelerate forced liquidation cascades once trend breaks begin.
- **Cross-Index Dispersion (`QQQ` vs. `IWM`):** Compares 52-week drawdown and 20-day annualized realized volatility between mega-cap growth (`QQQ`) and domestic small caps (`IWM`) to distinguish narrow index-concentration air-pockets from broad domestic credit stress.

---

# MODULE 5: Operational Hygiene — Atomic Option `2` Dual-Publish & Public Privacy

To prevent **stale-page drift** (forgetting to run a rare-regime engine separately while `Morning_Briefing` and `PORTFOLIO.html` refresh daily), the Tactical Dip & Pullback Radar is wired directly into **Option `2`** (`scripts/reconcile_portfolio.py --reconcile --publish`):

1. **Exact Penny Synchronization:** Option `2` reconciles Engine 3 positions and updates `portfolio_tracker.sqlite` first, then immediately runs the read-only tactical snapshot against that freshly reconciled ledger so the cash balance, NAV, and pending `T2`/`T3` order encumbrances match `PORTFOLIO.html` and `TACTICAL_DIP.html` identically.
2. **Fault Isolation:** The tactical refresh runs inside an isolated wrapper (`refresh_tactical_dip_for_portfolio`). If Yahoo Finance is unreachable or an external series fails, the radar falls back to verified local cache (`data_lake/tactical_dip_cache.json`) or fails closed (`DATA_UNAVAILABLE_VETO`) without ever blocking or corrupting Engine 3 portfolio reconciliation.
3. **Public vs. Local Privacy Boundary:** Any automated Option `2` publish or `--publish` run enforces `gold_held_usd = 0.0` so the public GitHub Pages site strictly reflects the paper `$100K` model portfolio. Ad-hoc local runs via **Option `8`** (`scripts/run_tactical_dip_radar.py --gold-held-usd <amt>`) remain available locally for personal sizing without touching public pages.

---

<details markdown="1">
<summary>📋 <b>Quick-Reference State Machine &amp; Fail-Closed Guardrails (Click to Expand)</b></summary>

| Overall Posture Badge | Triggering Condition | Operator Meaning |
| :--- | :--- | :--- |
| **`DATA_UNAVAILABLE_VETO`** | `SPY` or `^VIX` feed missing / empty | Fail-closed halt — never interpolate or fabricate prices; verify data feeds. |
| **`DEFENSIVE_VETO_ACTIVE`** | `T1` invalidation triggered, `HY OAS >= 400 bps`, or `VIX/VIX3M >= 1.05` | Credit or acute vol backwardation veto is active; preserve dry powder. |
| **`HOLIDAY_THIN_BOOK_WAIT`** | Scheduled NYSE half-day or `SPY` vol `< 0.60x` 20D avg | Liquidity/vol-decay artifact active; wait for full-volume session reset. |
| **`CONFIRMED_RECLAIM_DEPLOY`** | `SPY` `T2` Core Confirmation (`50%`) is `READY` | Full-liquidity Friday weekly close reclaimed `200D SMA` with benign credit. |
| **`SCOUT_TOE_DIP_READY`** | `SPY` `T1` Scout (`20%`) is `READY` (while `T2` remains `LOCKED`) | Full-liquidity vol de-escalation or `100W SMA` defense confirmed for starter scout. |
| **`PATIENT_DRY_POWDER_WATCH`** | No vetoes active, no `SPY` `T1`/`T2` triggers met | Normal patience posture; keep dry powder compounding in MMF sweep. |

</details>

---
*Manual maintained natively by Antigravity V3 Core — Synchronized with `models/tactical_dip_model.py`, `strategies/tactical_dip_engine.py`, and `reporting/tactical_dip_report.py`.*
