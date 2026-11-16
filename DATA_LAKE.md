# 🗄️ Open SEC XBRL Data Lake & Wide-Net Market Scanner
**Generated:** 2026-11-16 17:34 UTC | **Coverage:** `5,387` Active `10-K`/`10-Q` Operating Companies (`68` Normalized Columns) | **Quotes:** `2026-11-16 17:24:15 UTC` (`Fresh`)

[☕ Daily Morning Briefing](https://bobmahalo.github.io/morning-briefing/) | [📈 $100K Model Portfolio](https://bobmahalo.github.io/morning-briefing/PORTFOLIO.html) | [🗄️ Open SEC Data Lake](https://bobmahalo.github.io/morning-briefing/DATA_LAKE.html) | [🏛️ S&P 1500 Screen](https://bobmahalo.github.io/morning-briefing/SP1500_SCREEN.html) | [🎓 Master Curriculum](https://bobmahalo.github.io/morning-briefing/CURRICULUM.html) | [🔬 SSR Executive Curriculum](https://bobmahalo.github.io/morning-briefing/SSR_CURRICULUM.html) | [🗂️ Single Stock Directory](https://bobmahalo.github.io/Single-Stock-Scan/)

> **🏛️ True Stock Ownership & Custody Education:** Holding shares in broker "Street Name" means you only hold a beneficial entitlement while Cede & Co. holds legal title. Learn how Direct Registration (DRS) protects your shares from broker insolvency and short-lending at **[WhyDRS.org](https://www.whydrs.org)** ([Advocacy](https://www.whydrs.org/advocacy) | [Free Resources](https://www.whydrs.org/free-resources)).

> **Disclaimer:** *This report and open dataset are for educational and informational purposes only and do not constitute financial advice. The author is not a licensed financial advisor. All investments carry risk, and you should conduct your own due diligence before making any financial decisions.*

## 1. Centralized SEC XBRL Data Lake (Direct Download & Query Endpoints)

Instead of burning paid API tokens querying slow-moving quarterly balance sheets one ticker at a time, this repository compiles the SEC EDGAR nightly bulk archives (`companyfacts.zip` + `submissions.zip`, `~2.8 GB` raw XBRL) through a deterministic CPA tag-fallback normalizer into a compact **`~2.6 MB`** dataset covering **`5,387` `10-K`/`10-Q` companies** across **`68` columns**. `SIC 6000–6799` Financials & REITs are retained in the master table (`Is_Financial_Or_REIT = True`) while excluded from operating Hunting Buckets and Stage 1 (alongside stale or deregistered/regime-shifted filers) and surfaced separately in `Financial_REIT_Signals.csv` (`204` pinned signals). Updated every weekend.

| Dataset Artifact | Scope & Row Count | Format | Direct Download / Query Link | Raw GitHub Endpoint (For Scripts & Bots) |
| :--- | :--- | :---: | :---: | :---: |
| **Master Universe (All Scanned Filers)** | `5,387` rows × `68` cols | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Master_Universe_All_Stocks.csv) | [`raw/.../Master_Universe_All_Stocks.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Master_Universe_All_Stocks.csv) |
| **Master Universe SQLite Database** | `5,387` rows (`master_universe` table) | `SQLite3` | [📥 Download SQLite](https://bobmahalo.github.io/morning-briefing/data/master_universe.sqlite) | [`raw/.../master_universe.sqlite`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/master_universe.sqlite) |
| **Non-Dilutive Operating Hunting Buckets** | `896` fresh operating rows (`>= 1` bucket, non-Fin/REIT) | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Hunting_Buckets_Sub5_and_DeepValue.csv) | [`raw/.../Hunting_Buckets_Sub5_and_DeepValue.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Hunting_Buckets_Sub5_and_DeepValue.csv) |
| **Stage 1 Forensic Convergence Shortlist** | `9` fresh operating multi-bucket survivors | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Stage1_Convergence_Shortlist.csv) | [`raw/.../Stage1_Convergence_Shortlist.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Stage1_Convergence_Shortlist.csv) |
| **Financials & REITs Pinned Signals** | `204` fresh `SIC 6000–6799` buyback/insider signals | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Financial_REIT_Signals.csv) | [`raw/.../Financial_REIT_Signals.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Financial_REIT_Signals.csv) |
| **CPA XBRL Tag Fallback Dictionary** | Ranked `us-gaap` aliases & derived identities | `YAML` | [📥 View YAML](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml) | [`raw/.../xbrl_aliases.yaml`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/xbrl_aliases.yaml) |

<details markdown="1">
<summary>⚡ <b>Quick-Start Code Snippets: Query All `5,387` Stocks in 1 Line (Python, SQLite, Google Sheets — Zero API Tokens)</b></summary>

### Option A: Python (`pandas`) — Zero Clone Required
```python
import pandas as pd

# Pull the entire normalized SEC operating universe directly over HTTPS:
url = "https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Master_Universe_All_Stocks.csv"
df = pd.read_csv(url)

# Run your own custom screen (Columns 1-60 are pure un-opinionated fundamentals & forensics):
custom_screen = df[
    (df["ROIC_TTM_Pct"] >= 15.0)
    & (df["FCF_to_Price_Yield_Pct"] >= 8.0)
    & (df["Share_Count_1Y_Change_Pct"] <= 0.0)
    & (df["Piotroski_F_Score"] >= 7)
].sort_values("FCF_to_Price_Yield_Pct", ascending=False)
print(custom_screen[["Ticker", "Company_Name", "Share_Price", "FCF_to_Price_Yield_Pct", "ROIC_TTM_Pct"]].head(20))
```

### Option B: Google Sheets — Live Auto-Updating Sheet
Paste this into cell `A1` of any blank Google Sheet to import the Stage 1 Forensic Shortlist (or replace with `Master_Universe_All_Stocks.csv`):
```text
=IMPORTDATA("https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Stage1_Convergence_Shortlist.csv")
```

### Option C: Local SQLite Query (`master_universe.sqlite`)
```sql
SELECT Ticker, Company_Name, Share_Price, Market_Cap_M, FCF_to_Price_Yield_Pct, Net_Cash_Ex_Debt_Per_Share, Piotroski_F_Score
FROM master_universe
WHERE Is_Dilution_Vampire = 0
  AND Net_Cash_to_Price_Yield_Pct >= 30.0
  AND Piotroski_F_Score >= 6
ORDER BY FCF_to_Price_Yield_Pct DESC;
```

</details>

<details markdown="1">
<summary>🤝 <b>Community Formula & CPA XBRL Tag Bounty ("Contribute Rules, Never Raw Data")</b></summary>

> **Why Contributors Submit Rules Instead of Mutated CSVs:**  
> Every weekend, the bulk scanner rebuilds all `5,387` rows from scratch out of the SEC EDGAR bulk archives. If a contributor manually edits a CSV, the next weekend refresh will overwrite it—and manual CSV edits cannot be audited for lookahead bias or unit errors.

| Contribution Type | Where It Lives in the Pipeline | How to Propose an Upgrade | Community Benefit |
| :--- | :--- | :--- | :--- |
| **1. Missing CPA XBRL Tag Fallback** | [`xbrl_aliases.yaml`](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml) | Identify a ticker where a standard GAAP line item shows `NR` due to an unusual CPA taxonomy tag and submit the `us-gaap:TagName` rank order. | Eliminates blank cells across all filers using that accounting convention. |
| **2. New Un-Opinionated Fundamental Column** | `models/wide_net_scoreboard.py` | Propose a deterministic accounting ratio or balance-sheet metric built from SEC `10-K`/`10-Q` line items (e.g., Interest Coverage, Cash Conversion Cycle, Gross Profitability). | Once verified by `pytest`, our weekend engine compiles and hosts your column across all `5,387` stocks automatically every week. |
| **3. Custom Strategy Sieve / Factor Idea** | Community Discussion / PR | Use Columns `1–60` (pure fundamentals & forensics) to test your own risk-tolerance rules, then share high-signal mathematical sieves for review. | Shared alpha discovery without duplicating `2.8 GB` SEC data pulls. |

</details>

---

## 2. Wide-Net Market Scanner: Universe Health & 4 Hunting Buckets

- **Total Operating `10-K`/`10-Q` Companies Scanned:** `5,387` (`4,739` non-dilutive operating filers + `648` quarantined by Step A Dilution Sieve)
- **Companies with Live Exchange Price:** `4,341` (`1,127` trading at `<= $5.00/sh`)
- **Stage 1 Multi-Bucket Forensic Survivors:** `9` companies passing all binary solvency, dilution, and F-Score gates

### Summary of the 4 Hunting Buckets

| Hunting Bucket | Total Qualifiers | Sub-$5.00 (`<= $5`) | `$5.01 - $20.00` | `> $20.00` |
| :--- | ---: | ---: | ---: | ---: |
| **1. Net Cash Floor / Graham Net-Net (`Bucket_1_Net_Cash_Floor`)** | **367** | `173` | `134` | `60` |
| **2. High-FCF Deep Value Turnaround (`Bucket_2_High_FCF_Turnaround`)** | **130** | `32` | `42` | `56` |
| **3. Cannibal Share Buybacks (`Bucket_3_Cannibal_Buybacks`)** | **305** | `9` | `46` | `250` |
| **4. C-Suite / Cluster Insider Buying (`Bucket_4_Cluster_Insider_Buy`)** | **294** | `102` | `82` | `100` |

## Bucket 1: Net Cash Floor & Graham Net-Nets (`Bucket_1_Net_Cash_Floor`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **APVO** | Aptevo Therapeutics Inc. | `$0.59` | $1.07M | `$3.10` | `$1.29` | `$3.35` | **NR** | `-45.19%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MBIO** | MUSTANG BIO, INC. | `$0.42` | $2.86M | `$2.12` | `$1.41` | `$0.98` | **NR** | `7.92%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **INHD** | INNO HOLDINGS INC. | `$2.65` | $6.68M | `$13.10` | `$21.38` | `$22.07` | **NR** | `-67.47%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PARA** | Parabolic Technologies, Inc. | `$0.10` | $0.17M | `$0.37` | `$-10.62` | `$-10.57` | **NR** | `1,594.79%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **JTAI** | Jet.AI Inc. | `$0.83` | $2.96M | `$2.84` | `$2.01` | `$11.21` | **NR** | `9.08%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **CTNT** | CHEETAH NET SUPPLY CHAIN SER | `$1.61` | $4.30M | `$4.83` | `$32.40` | `$32.67` | **NR** | `66.91%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MSAI** | MultiSensor AI Holdings, Inc | `$3.15` | $6.99M | `$9.15` | `$10.17` | `$12.05` | **NR** | `-95.78%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **REVB** | REVELATION BIOSCIENCES, INC. | `$4.19` | $2.86M | `$12.17` | `$9.48` | `$10.58` | **NR** | `-88.46%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PLRX** | PLIANT THERAPEUTICS, INC. | `$0.70` | $43.21M | `$1.83` | `$1.63` | `$2.04` | **-154.58%** | `0.88%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PHUN** | Phunware, Inc. | `$1.73` | $35.40M | `$4.48` | `$4.30` | `$4.33` | **NR** | `1.37%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **AUUD** | AUDDIA INC. | `$0.36` | $2.49M | `$0.87` | `$0.81` | `$1.24` | **NR** | `122.92%` | `4/9` | `1_NET_CASH_FLOOR` |
| **CDT** | CDT Equity Inc. | `$0.40` | $0.31M | `$0.89` | `$-26.28` | `$131.05` | **NR** | `-74.31%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **FBIO** | Fortress Biotech, Inc. | `$1.88` | $63.44M | `$4.11` | `$3.18` | `$4.74` | **NR** | `1.95%` | `4/9` | `1_NET_CASH_FLOOR` |
| **PEW** | GrabAGun Digital Holdings In | `$1.50` | $44.24M | `$3.25` | `$2.84` | `$3.38` | **-41.36%** | `-1.41%` | `4/9` | `1_NET_CASH_FLOOR` |
| **AIFA** | All In FutureTech Alliance,  | `$3.54` | $22.73M | `$7.47` | `$3.27` | `$4.30` | **-43.58%** | `-83.11%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **XLO** | Xilio Therapeutics, Inc. | `$7.99` | $56.44M | `$16.45` | `$8.48` | `$9.66` | **-102.10%** | `-86.54%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **OPAL** | OPAL Fuels Inc. | `$1.22` | $36.01M | `$2.45` | `$-11.57` | `$-0.54` | **-51.70%** | `4.82%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **SRXH** | SRX Global Inc. | `$0.96` | $19.45M | `$1.89` | `$3.10` | `$3.11` | **NR** | `3,258.64%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **BCYC** | BICYCLE THERAPEUTICS PLC | `$3.37` | $235.83M | `$6.52` | `$6.80` | `$7.22` | **-75.07%** | `0.98%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **IMA** | ImageneBio, Inc. | `$3.47` | $43.22M | `$6.71` | `$9.33` | `$10.29` | **NR** | `11.40%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **ALDX** | Aldeyra Therapeutics, Inc. | `$0.64` | $38.86M | `$1.15` | `$0.58` | `$0.58` | **NR** | `0.32%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **MSN** | EMERSON RADIO CORP | `$0.30` | $6.27M | `$0.53` | `$0.77` | `$0.79` | **-59.34%** | `0.00%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **IVDA** | Iveda Solutions, Inc. | `$0.20` | $2.52M | `$0.35` | `$0.41` | `$0.43` | **NR** | `330.69%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **LONA** | LeonaBio, Inc. | `$3.47` | $32.69M | `$5.36` | `$3.34` | `$3.57` | **NR** | `-76.11%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MYPS** | PLAYSTUDIOS, Inc. | `$4.93` | $59.38M | `$7.59` | `$6.29` | `$8.07` | **34.14%** | `-4.18%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **AIDX** | 20/20 Biolabs, Inc. | `$0.20` | $2.61M | `$0.31` | `$0.17` | `$0.11` | **NR** | `2.70%` | `5/9` | `1_NET_CASH_FLOOR` |
| **QNT** | Quantinuum Inc. | `$35.40` | $1,302.96M | `$51.73` | `$51.99` | `$-8.62` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **KAPA** | Kairos Pharma, LTD. | `$0.46` | $2.16M | `$0.67` | `$0.61` | `$0.81` | **NR** | `-77.50%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **RNA** | Atrium Therapeutics, Inc. | `$7.51` | $162.00M | `$10.73` | `$9.23` | `$9.50` | **-38.37%** | `-0.40%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **SCYX** | SCYNEXIS INC | `$3.21` | $31.95M | `$4.56` | `$4.16` | `$5.93` | **NR** | `-76.28%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **ABOS** | Acumen Pharmaceuticals, Inc. | `$0.21` | $15.48M | `$0.30` | `$0.47` | `$0.48` | **NR** | `19.40%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **TVRD** | Tvardi Therapeutics, Inc. | `$1.18` | $15.77M | `$1.65` | `$1.13` | `$1.14` | **NR** | `42.45%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MRLN** | Merlin, Inc. | `$1.13` | $116.59M | `$1.54` | `$1.21` | `$-0.25` | **NR** | `45.22%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **INVE** | INVE Technologies, Inc. | `$2.66` | $63.47M | `$3.60` | `$3.38` | `$5.49` | **NR** | `0.44%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **JANX** | Janux Therapeutics, Inc. | `$11.37` | $695.66M | `$15.12` | `$14.50` | `$14.90` | **-7.79%** | `1.72%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **GDC** | GD Culture Group Ltd | `$1.15` | $4.79M | `$1.50` | `$8.61` | `$117.21` | **NR** | `-75.22%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **EROC** | ERock, Inc. | `$8.41` | $405.14M | `$10.61` | `$2.11` | `NR` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **NNDM** | Nano Dimension Ltd. | `$1.24` | $245.81M | `$1.56` | `$1.98` | `$2.78` | **NR** | `-4.32%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **VTGN** | Vistagen Therapeutics, Inc. | `$0.18` | $8.34M | `$0.22` | `$0.30` | `$0.32` | **NR** | `16.94%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **KROS** | Keros Therapeutics, Inc. | `$10.30` | $202.13M | `$12.45` | `$13.22` | `$14.22` | **-23.88%** | `-35.59%` | `6/9` | `1_NET_CASH_FLOOR` |

## Bucket 2: High-FCF Deep Value Turnarounds (`Bucket_2_High_FCF_Turnaround`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **PAAI** | Paradium.AI, Inc. | `$0.62` | $29.35M | `$-1.88` | `$-1.79` | `$-1.14` | **133.73%** | `0.31%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **AMS** | AMERICAN SHARED HOSPITAL SER | `$1.08` | $7.21M | `$0.44` | `$-1.32` | `$3.19` | **95.88%** | `2.02%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **MKTW** | MARKETWISE, INC. | `$20.46` | $60.05M | `$7.34` | `$-124.76` | `$-23.43` | **86.77%** | `12.97%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**CRMD**](https://bobmahalo.github.io/Single-Stock-Scan/CRMD.html) | CorMedix Inc. | `$4.66` | $370.65M | `$4.42` | `$0.59` | `$1.05` | **83.06%** | `0.95%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **FLUX** | Flux Power Holdings, Inc. | `$0.31` | $6.79M | `$-0.07` | `$-0.17` | `$-0.05` | **73.17%** | `2.92%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **WETH** | Wetouch Technology Inc. | `$0.80` | $10.71M | `$9.51` | `$10.02` | `$11.12` | **66.04%** | `2.82%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **EBS** | Emergent BioSolutions Inc. | `$5.79` | $297.44M | `$-6.57` | `$-2.41` | `$1.18` | **63.34%** | `-2.10%` | `7/9` | `2_HIGH_FCF_TURNAROUND` |
| **XRX** | Xerox Holdings Corp | `$0.92` | $121.93M | `$-0.54` | `$-40.97` | `$-20.89` | **62.33%** | `4.04%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **CMTL** | COMTECH TELECOMMUNICATIONS C | `$1.20` | $36.16M | `$0.74` | `$-6.36` | `$-4.55` | **61.35%** | `1.50%` | `5/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **KODK** | EASTMAN KODAK CO | `$8.12` | $792.19M | `$2.04` | `$-0.18` | `$6.41` | **58.70%** | `20.97%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **TTEC** | TTEC Holdings, Inc. | `$2.95` | $145.68M | `$0.42` | `$-13.71` | `NR` | **53.96%** | `1.72%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**CRWS**](https://bobmahalo.github.io/Single-Stock-Scan/CRWS.html) | CROWN CRAFTS INC | `$2.52` | $27.40M | `$-1.07` | `$2.45` | `$3.26` | **51.21%** | `1.58%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PLTK** | Playtika Holding Corp. | `$2.64` | $1,010.26M | `$-5.00` | `$-7.61` | `$-6.27` | **47.64%** | `1.76%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**DXC**](https://bobmahalo.github.io/Single-Stock-Scan/DXC.html) | DXC Technology Co | `$14.72` | $2,289.31M | `$6.21` | `$-25.16` | `$16.27` | **44.99%** | `-10.72%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **PAGP** | PLAINS GP HOLDINGS LP | `$26.37` | $5,223.93M | `$3.34` | `$3.02` | `NR` | **43.47%** | `0.11%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **SCOR** | COMSCORE, INC. | `$3.00` | $45.55M | `$1.08` | `$-3.99` | `$-6.31` | **43.34%** | `202.79%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **COLL** | COLLEGIUM PHARMACEUTICAL, IN | `$25.32` | $786.83M | `$4.48` | `$-38.22` | `$-33.21` | **42.74%** | `-1.69%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**DLTH**](https://bobmahalo.github.io/Single-Stock-Scan/DLTH.html) | DULUTH HOLDINGS INC. | `$3.96` | $144.07M | `$-1.68` | `$-0.99` | `$4.88` | **39.94%** | `4.98%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **MYPS** | PLAYSTUDIOS, Inc. | `$4.93` | $59.38M | `$7.59` | `$6.29` | `$8.07` | **34.14%** | `-4.18%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **VSNT** | Versant Media Group, Inc. | `$35.94` | $4,979.06M | `$-12.72` | `$-10.94` | `$-0.65` | **32.94%** | `-3.91%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**NRDS**](https://bobmahalo.github.io/Single-Stock-Scan/NRDS.html) | NERDWALLET, INC. | `$7.46` | $482.66M | `$1.03` | `$2.01` | `$3.11` | **30.25%** | `-15.86%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **PBF** | PBF Energy Inc. | `$71.26` | $8,747.63M | `$-0.95` | `$-8.95` | `$64.81` | **30.01%** | `4.07%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **DK** | Delek US Holdings, Inc. | `$68.47` | $4,150.25M | `$-34.77` | `$-41.51` | `NR` | **28.95%** | `0.94%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **AERT** | Aeries Technology, Inc. | `$4.50` | $28.53M | `$-0.52` | `$-2.71` | `$-0.26` | **28.63%** | `7.19%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **LCUT** | LIFETIME BRANDS, INC | `$7.77` | $178.59M | `$-4.42` | `$9.99` | `$3.49` | **28.41%** | `1.45%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **SSTK** | Shutterstock, Inc. | `$2.91` | $107.92M | `$-0.63` | `$-11.46` | `$-0.68` | **28.38%** | `4.43%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **UFI** | UNIFI INC | `$6.65` | $123.62M | `$1.08` | `$3.31` | `NR` | **28.28%** | `1.24%` | `6/9` | `2_HIGH_FCF_TURNAROUND` |
| **PMTS** | CPI Card Group Inc. | `$24.93` | $289.99M | `$-21.98` | `$-17.96` | `$-6.75` | **28.05%** | `2.15%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **PARR** | PAR PACIFIC HOLDINGS, INC. | `$73.12` | $3,661.88M | `$-2.48` | `$5.56` | `$43.80` | **28.04%** | `-0.43%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **JVA** | COFFEE HOLDING CO INC | `$5.07` | $28.94M | `$0.17` | `$4.29` | `$5.43` | **27.57%** | `0.00%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **TBLA** | Taboola.com Ltd. | `$2.23` | $637.34M | `$-0.09` | `$-0.13` | `$1.31` | **27.44%** | `-6.50%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **IPM** | INTELLIGENT PROTECTION MANAG | `$1.73` | $15.63M | `$0.71` | `$-0.11` | `$0.47` | **27.39%** | `-0.55%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **ADT** | ADT Inc. | `$9.89` | $7,224.95M | `$-8.77` | `$-15.53` | `$-8.38` | **26.68%** | `NR` | `7/9` | `2_HIGH_FCF_TURNAROUND` |
| **DSP** | Viant Technology Inc. | `$11.92` | $252.98M | `$7.64` | `$7.99` | `$3.88` | **26.59%** | `10.66%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **IMMR** | IMMERSION CORP | `$6.94` | $230.45M | `$4.17` | `$5.82` | `$6.92` | **26.53%** | `2.11%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **HBB** | Hamilton Beach Brands Holdin | `$31.15` | $419.15M | `$3.90` | `$10.43` | `$15.88` | **25.58%** | `-0.38%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **CRI** | CARTERS INC | `$34.29` | $1,258.19M | `$-19.84` | `$-5.42` | `$15.76` | **25.41%** | `0.67%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **PXED** | Phoenix Education Partners,  | `$19.09` | $700.16M | `$2.63` | `$2.98` | `$6.98` | **25.11%** | `1.99%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **IMXI** | International Money Express, | `$6.29` | $190.08M | `$0.63` | `$1.08` | `$3.18` | **25.08%** | `1.69%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **MSGM** | Motorsport Games Inc. | `$3.91` | $20.98M | `$0.96` | `$0.47` | `$0.34` | **25.05%** | `-1.67%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |

## Bucket 3: Cannibal Buybacks (`Bucket_3_Cannibal_Buybacks`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **IIIV** | i3 Verticals, Inc. | `$18.91` | $369.57M | `$-5.95` | `$-8.35` | `$-7.95` | **13.51%** | `-42.41%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **AMCX** | AMC Global Media Inc. | `$9.50` | $397.55M | `$-31.01` | `$-35.26` | `$12.86` | **24.17%** | `-25.64%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **BTMD** | biote Corp. | `$1.06` | $29.20M | `$-4.23` | `$-4.29` | `$-2.72` | **25.37%** | `-25.32%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **IBTA** | Ibotta, Inc. | `$57.55` | $1,343.74M | `$5.34` | `$5.21` | `$10.21` | **6.06%** | `-20.52%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **FOUR** | Shift4 Payments, Inc. | `$44.78` | $3,356.36M | `$-48.68` | `$-67.53` | `$-17.16` | **18.59%** | `-20.08%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **PAYC** | Paycom Software, Inc. | `$248.68` | $11,199.25M | `$-13.98` | `$-21.99` | `$13.95` | **5.89%** | `-19.97%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **YEXT** | Yext, Inc. | `$7.66` | $758.18M | `$-1.36` | `$-2.52` | `$-0.76` | **6.99%** | `-19.68%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **PRKS** | United Parks & Resorts Inc. | `$40.16` | $1,824.76M | `$-51.76` | `$-64.88` | `$-13.19` | **8.23%** | `-16.71%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **ZD** | ZIFF DAVIS, INC. | `$51.49` | $1,704.44M | `$20.04` | `$8.40` | `$18.25` | **6.37%** | `-16.21%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **PINS** | PINTEREST, INC. | `$19.16` | $11,166.53M | `$-1.00` | `$1.18` | `$4.37` | **11.30%** | `-16.11%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| [**NRDS**](https://bobmahalo.github.io/Single-Stock-Scan/NRDS.html) | NERDWALLET, INC. | `$7.46` | $482.66M | `$1.03` | `$2.01` | `$3.11` | **30.25%** | `-15.86%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **PD** | PagerDuty, Inc. | `$15.96` | $1,254.86M | `$-2.28` | `$-1.68` | `$1.03` | **10.09%** | `-15.65%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **BFAM** | BRIGHT HORIZONS FAMILY SOLUT | `$52.67` | $2,524.77M | `$-35.42` | `$-50.00` | `$-22.54` | **10.03%** | `-15.25%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **DBX** | DROPBOX, INC. | `$33.53` | $7,547.60M | `$0.16` | `$-16.59` | `$-11.89` | **12.13%** | `-15.09%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **DIN** | Dine Brands Global, Inc. | `$37.01` | $455.04M | `$-126.16` | `$-143.12` | `$-86.47` | **11.74%** | `-14.76%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **PGNY** | Progyny, Inc. | `$36.18` | $2,664.56M | `$1.24` | `$2.75` | `$5.35` | **6.74%** | `-14.57%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| [**HOG**](https://bobmahalo.github.io/Single-Stock-Scan/HOG.html) | HARLEY-DAVIDSON, INC. | `$32.40` | $3,271.65M | `$6.64` | `$8.98` | `$29.39` | **9.53%** | `-14.52%` | `8/9` | `1_NET_CASH_FLOOR | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **CHTR** | CHARTER COMMUNICATIONS, INC. | `$138.39` | $16,183.94M | `$-905.82` | `$-987.46` | `$-160.46` | **24.28%** | `-14.26%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **BILL** | BILL Holdings, Inc. | `$54.49` | $4,679.77M | `$-6.14` | `$6.49` | `$8.80` | **8.84%** | `-14.25%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CRM** | Salesforce, Inc. | `$217.88` | $179,315.24M | `$-40.62` | `$-59.73` | `$-32.82` | **8.45%** | `-13.55%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **MIDD** | MIDDLEBY Corp | `$135.16` | $5,886.96M | `$-39.36` | `$-26.32` | `$-18.52` | **6.32%** | `-13.53%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CPRI** | Capri Holdings Ltd | `$21.46` | $2,217.88M | `$-13.17` | `$-19.09` | `$-6.61` | **8.30%** | `-13.26%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **SMPL** | Simply Good Foods Co | `$12.57` | $1,091.85M | `$-2.50` | `$-1.74` | `$-0.61` | **14.37%** | `-13.01%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **CARS** | Cars.com Inc. | `$12.72` | $662.41M | `$-7.58` | `$-6.77` | `$-4.06` | **22.73%** | `-12.94%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **ETSY** | ETSY INC | `$89.04` | $7,675.77M | `$23.50` | `$-14.41` | `$-8.30` | **7.72%** | `-12.66%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **TENB** | Tenable Holdings, Inc. | `$40.76` | $4,259.73M | `$-3.31` | `$-9.45` | `$-7.84` | **6.58%** | `-12.43%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **AN** | AUTONATION, INC. | `$177.73` | $5,684.44M | `$-12.80` | `$-44.16` | `$-12.65` | **0.40%** | `-12.31%` | `5/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **ZG** | ZILLOW GROUP, INC. | `$30.11` | $6,783.93M | `$2.28` | `$3.01` | `$5.11` | **4.61%** | `-12.07%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CROX** | Crocs, Inc. | `$163.72` | $7,486.10M | `$-32.80` | `$-41.73` | `$-8.13` | **10.07%** | `-11.92%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **FCN** | FTI CONSULTING, INC | `$202.65` | $5,523.06M | `$-36.68` | `$-21.74` | `$2.62` | **6.40%** | `-11.73%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **YELP** | YELP INC | `$20.34` | $1,108.39M | `$1.80` | `$-0.31` | `$4.26` | **23.73%** | `-11.38%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **HGV** | Hilton Grand Vacations Inc. | `$43.91` | $3,329.38M | `NR` | `NR` | `$-8.97` | **14.21%** | `-11.36%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| [**PYPL**](https://bobmahalo.github.io/Single-Stock-Scan/PYPL.html) | PayPal Holdings, Inc. | `$59.28` | $49,241.42M | `$-4.77` | `$-1.91` | `$10.25` | **12.79%** | `-11.22%` | `8/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **UTMD** | UTAH MEDICAL PRODUCTS INC | `$71.97` | $205.08M | `$29.80` | `$33.48` | `$37.00` | **5.30%** | `-11.05%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **DVA** | DAVITA INC. | `$174.48` | $10,974.79M | `$-33.83` | `$-200.57` | `$-132.91` | **11.79%** | `-10.91%` | `7/9` | `3_CANNIBAL_BUYBACKS` |
| [**DXC**](https://bobmahalo.github.io/Single-Stock-Scan/DXC.html) | DXC Technology Co | `$14.72` | $2,289.31M | `$6.21` | `$-25.16` | `$16.27` | **44.99%** | `-10.72%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| [**ZUMZ**](https://bobmahalo.github.io/Single-Stock-Scan/ZUMZ.html) | Zumiez Inc | `$14.00` | $214.63M | `$-11.54` | `$-3.40` | `$16.20` | **11.68%** | `-10.63%` | `NR/9` | `1_NET_CASH_FLOOR | 3_CANNIBAL_BUYBACKS` |
| **GDDY** | GoDaddy Inc. | `$114.26` | $13,856.85M | `NR` | `NR` | `$-38.78` | **12.58%** | `-10.26%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CVEO** | Civeo Corp | `$35.81` | $370.16M | `$-19.77` | `$-16.46` | `$6.95` | **7.98%** | `-10.23%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **DHX** | DHI GROUP, INC. | `$4.40` | $186.89M | `$-0.83` | `$-1.66` | `$-1.08` | **11.91%** | `-9.93%` | `4/9` | `3_CANNIBAL_BUYBACKS` |

## Bucket 4: Cluster & C-Suite Insider Buying (`Bucket_4_Cluster_Insider_Buy`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **PBLS** | Parabilis Medicines, Inc. | `$28.43` | $3,513.75M | `$3.89` | `$6.09` | `$8.13` | **NR** | `6,021.17%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **MAIR** | Madison Air Solutions Corp | `$23.79` | $12,613.14M | `$4.73` | `$-1.88` | `$-0.85` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BRVE** | Braveheart Bio, Inc. | `$19.62` | $1,763.26M | `$1.34` | `$3.81` | `$5.54` | **NR** | `1,765.60%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SMMT** | Summit Therapeutics Inc. | `$14.15` | $11,316.66M | `$0.76` | `$0.67` | `$0.70` | **-4.66%** | `7.43%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ROL** | ROLLINS INC | `$38.88` | $18,586.40M | `$-0.56` | `$-2.84` | `$-1.39` | **3.61%** | `-1.36%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| [**GME**](https://bobmahalo.github.io/Single-Stock-Scan/GME.html) | GameStop Corp. | `$25.86` | $13,043.87M | `$1.03` | `$1.83` | `$12.17` | **5.27%** | `12.70%` | `6/9` | `4_CLUSTER_INSIDER_BUY` |
| **KARD** | Kardigan, Inc. | `$13.82` | $1,293.52M | `$0.71` | `$4.36` | `$5.83` | **NR** | `643.69%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ADRX** | ADARx Pharmaceuticals, Inc. | `$14.20` | $1,578.95M | `$8.04` | `$5.07` | `$5.17` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **DPC** | DPC Holdings PLC | `$34.25` | $5,116.71M | `$1.37` | `$1.93` | `$4.42` | **NR** | `32.56%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SCTX** | Scribe Therapeutics, Inc. | `$16.36` | $309.82M | `$8.81` | `$6.13` | `$6.61` | **NR** | `496.86%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **LFTO** | Liftoff Mobile, Inc. | `$24.44` | $4,141.22M | `$-5.92` | `$-7.45` | `$-6.47` | **NR** | `25.65%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **LILA** | Liberty Latin America Ltd. | `$9.84` | $1,915.85M | `$-0.25` | `$-46.82` | `$-13.43` | **NR** | `-6.26%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ATTO** | Attovia Therapeutics, Inc. | `$15.13` | $691.63M | `$2.44` | `$8.54` | `$8.70` | **NR** | `654.04%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **LYEL** | Lyell Immunopharma, Inc. | `$14.30` | $351.57M | `$1.94` | `$4.27` | `$7.84` | **-39.81%** | `15.87%` | `2/9` | `4_CLUSTER_INSIDER_BUY` |
| **ETRA** | Electra Therapeutics, Inc. | `$8.84` | $555.74M | `$4.05` | `$6.19` | `$6.25` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **AVO** | Mission Produce, Inc. | `$11.83` | $1,037.24M | `$-4.88` | `$-4.62` | `$5.65` | **-0.22%** | `24.16%` | `8/9` | `4_CLUSTER_INSIDER_BUY` |
| **AVR** | Anteris Technologies Global  | `$5.42` | $528.41M | `$2.06` | `$2.07` | `$2.33` | **-17.69%** | `136.65%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| [**LRN**](https://bobmahalo.github.io/Single-Stock-Scan/LRN.html) | Stride, Inc. | `$75.81` | $3,187.93M | `$2.84` | `$21.29` | `$33.67` | **15.83%** | `-4.13%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **FUN** | Six Flags Entertainment Corp | `$11.56` | $1,183.21M | `$-47.59` | `$-53.15` | `$-22.78` | **NR** | `0.82%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **QTTB** | Q32 Bio Inc. | `$8.71` | $260.64M | `$9.51` | `$9.41` | `$9.61` | **-12.87%** | `143.20%` | `3/9` | `4_CLUSTER_INSIDER_BUY` |
| **SUJA** | SUJA LIFE, INC. | `$7.04` | $167.47M | `NR` | `NR` | `NR` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **MSM** | MSC INDUSTRIAL DIRECT CO INC | `$118.50` | $6,619.20M | `$-2.61` | `$4.23` | `$11.31` | **3.40%** | `0.12%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BLSM** | BlossomHill Therapeutics, In | `$14.02` | $445.62M | `$7.08` | `NR` | `$6.64` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **QNT** | Quantinuum Inc. | `$35.40` | $1,302.96M | `$51.73` | `$51.99` | `$-8.62` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **RAPP** | Rapport Therapeutics, Inc. | `$26.15` | $1,550.16M | `$6.51` | `$6.41` | `$6.60` | **-7.82%** | `24.38%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **NTSK** | Netskope Inc | `$21.75` | $8,809.75M | `$0.46` | `$-0.42` | `$0.19` | **-0.80%** | `274.71%` | `6/9` | `4_CLUSTER_INSIDER_BUY` |
| **ET** | Energy Transfer LP | `NR` | NR | `$-20.26` | `$-19.03` | `NR` | **NR** | `0.32%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **CV** | CapsoVision, Inc | `$6.03` | $323.27M | `NR` | `NR` | `$0.49` | **-9.06%** | `14.44%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **UBER** | Uber Technologies, Inc | `$69.67` | $142,259.04M | `$-4.01` | `$-11.87` | `$7.69` | **7.33%** | `-1.73%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| **FBIN** | Fortune Brands Innovations,  | `$48.05` | $5,692.76M | `$-19.94` | `$-15.91` | `NR` | **9.74%** | `-1.38%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **AMR** | Alpha Metallurgical Resource | `$153.96` | $1,949.45M | `$24.91` | `$7.16` | `$114.49` | **NR** | `-1.52%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **PMTS** | CPI Card Group Inc. | `$24.93` | $289.99M | `$-21.98` | `$-17.96` | `$-6.75` | **28.05%** | `2.15%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **TUSK** | MAMMOTH ENERGY SERVICES, INC | `$3.26` | $156.90M | `$0.19` | `$0.62` | `$5.43` | **-91.05%** | `-0.14%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **ACDC** | ProFrac Holding Corp. | `$3.15` | $573.69M | `$-5.48` | `$-6.42` | `$0.71` | **-2.77%** | `0.69%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **CDNL** | Cardinal Infrastructure Grou | `$6.46` | $133.06M | `NR` | `NR` | `$1.53` | **-8.85%** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BSX** | BOSTON SCIENTIFIC CORP | `$44.35` | $64,284.14M | `$-0.67` | `$1.51` | `$0.02` | **5.18%** | `-2.22%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **GLOO** | Gloo Holdings, Inc. | `$2.90` | $243.88M | `$-0.01` | `$-0.52` | `$-0.24` | **-27.18%** | `923.44%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **LWAY** | Lifeway Foods, Inc. | `$21.72` | $328.15M | `$0.43` | `$-0.08` | `$4.52` | **-10.74%** | `-0.79%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| [**APTV**](https://bobmahalo.github.io/Single-Stock-Scan/APTV.html) | Aptiv PLC | `$38.75` | $7,844.17M | `$-24.70` | `$-15.92` | `$15.01` | **NR** | `-6.32%` | `7/9` | `4_CLUSTER_INSIDER_BUY` |
| **OTLK** | Outlook Therapeutics, Inc. | `$0.41` | $100.54M | `$0.05` | `$-0.06` | `$-0.04` | **NR** | `448.06%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |

---

<details markdown="1">
<summary><b>📖 Open SEC Data Lake Methodology, `68`-Column Schema Dictionary & Forensic Formulas (Click to Expand)</b></summary>

### 1. Why a Normalized SEC XBRL Data Lake?
Publicly traded U.S. operating companies file quarterly (`10-Q`) and annual (`10-K`) financial statements with the SEC using XBRL (`us-gaap` taxonomy). Because different CPA firms use different XBRL tags for identical economic concepts, raw SEC queries frequently return blank cells (`NR`). Our ingestion layer maps ranked tag hierarchies and derived accounting identities ([`xbrl_aliases.yaml`](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml)) across **`5,387` active `10-K`/`10-Q` operating companies**, computes discrete Q4 values ($\text{FY} - \text{YTD}_3$), applies 1,000x share-unit scaling guards, and exports **`68` standardized columns**.

### 2. Schema Separation: Un-Opinionated Building Blocks vs. Strategy Buckets

| Column Group | Column Names / Examples | Intended Use Case |
| :--- | :--- | :--- |
| **Identity & Classification (`Cols 1–8`)** | `Ticker`, `CIK`, `Company_Name`, `Exchange`, `SIC_Code`, `SIC_Description`, `Is_Financial_Or_REIT`, `Latest_Period_End` | Universe filtering, sector/SIC peer benchmarking, and filing freshness checks. |
| **Market Pricing & Enterprise Scale (`Cols 9–13`)** | `Share_Price`, `Google_Sheets_Live_Price_Formula`, `Shares_Outstanding_M`, `Market_Cap_M`, `Enterprise_Value_M` | Live valuation multiples and Google Sheets integration. |
| **Per-Share Liquidation Floors & Yields (`Cols 14–24`)** | `Net_Cash_Ex_Debt_Per_Share`, `Graham_NCAV_Per_Share`, `Tangible_Book_Per_Share`, `FCF_Per_Share_TTM`, `FCF_to_Price_Yield_Pct`, `EBIT_to_EV_Yield_Pct` | Downside floor anchoring and inverted yield ranking (avoids negative-denominator P/E distortion). |
| **Raw TTM Flow & Balance Sheet Totals (`Cols 25–39`)** | `Revenue_TTM_M`, `Operating_Income_TTM_M`, `Net_Income_TTM_M`, `Operating_Cash_Flow_TTM_M`, `Free_Cash_Flow_TTM_M`, `Total_Cash_M`, `Total_Debt_M`, `Total_Liabilities_M`, `Stock_Buybacks_TTM_M`, `Stock_Issued_TTM_M`, `Dividends_Paid_TTM_M` | Raw dollar building blocks ($M) so external quants can construct any custom formula without re-parsing SEC filings. |
| **Efficiency, Growth & Share Dilution (`Cols 40–50`)** | `Gross_Margin_TTM_Pct`, `Operating_Margin_TTM_Pct`, `ROIC_TTM_Pct`, `ROIC_5Y_Median_Pct`, `Current_Ratio`, `Revenue_5Y_CAGR_Pct`, `Share_Count_1Y_Change_Pct`, `Share_Count_5Y_CAGR_Pct`, `Shareholder_Yield_Pct` | Quality compounder screening, capital allocation audits, and cannibal buyback tracking. |
| **Forensic Accounting & Insider Flow (`Cols 51–60`)** | `Piotroski_F_Score`, `Altman_Z_Score`, `Altman_Zone`, `Beneish_M_Score`, `SBC_Pct_OCF_TTM`, `Insider_Open_Market_Buys_12M`, `Insider_C_Suite_Buyers_12M`, `Insider_Net_Buy_USD_12M` | Solvency verification, earnings manipulation screening, and OpenInsider Form 4 cluster tracking. |
| **Optional Strategy Sieves (`Cols 61–68`)** | `Is_Dilution_Vampire` (`648` flagged), `Bucket_1_Net_Cash_Floor` (`367`), `Bucket_2_High_FCF_Turnaround` (`130`), `Bucket_3_Cannibal_Buybacks` (`305`), `Bucket_4_Cluster_Insider_Buy` (`294`), `Buckets_Count` | Optional deep-value hunting buckets feeding our `9`-stock Stage 1 Convergence Shortlist. |

### 3. Core Mathematical & Forensic Formulas

| Metric | Exact Mathematical Formula | Institutional Interpretation |
| :--- | :--- | :--- |
| **Net Cash (Ex-Debt) / Share** | $$\frac{\text{Cash \& ST Investments} - \text{Total Debt}}{N_{\text{diluted}}}$$ | Hard net cash cushion per share after extinguishing 100% of funded debt. |
| **Graham NCAV / Share** | $$\frac{\text{Current Assets} - \text{Total Liabilities} - \text{Preferred Stock}}{N_{\text{diluted}}}$$ | Benjamin Graham Net-Net liquidation floor (strict arbitrage requires $P \le 0.67 \times \text{NCAV}$). |
| **Tangible Book Value (TBV) / Share** | $$\frac{\text{Stockholders' Equity} - \text{Goodwill} - \text{Intangibles}}{N_{\text{diluted}}}$$ | Physical net worth per share stripping out M&A accounting goodwill. |
| **Altman Z-Score (5-Factor)** | $$Z = 1.2 X_1 + 1.4 X_2 + 3.3 X_3 + 0.6 X_4 + 0.999 X_5$$ | Solvency index across Operating Universe (`> 2.99` Safe, `1.81–2.99` Grey, `< 1.81` Distress). |
| **Step A Dilution Quarantine** | `Share_Count_1Y_Change_Pct > 10%` or (`FCF < 0` & `Stock_Issued > 5% MCap`) | Quarantines `{vampires:,}` chronic equity diluters (`Is_Dilution_Vampire = True`). |

</details>
