# 🗄️ Open SEC XBRL Data Lake & Wide-Net Market Scanner
**Generated:** 2026-11-22 21:26 UTC | **Coverage:** `5,341` Active `10-K`/`10-Q` Operating Companies (`68` Normalized Columns) | **Quotes:** `2026-11-22 19:42:29 UTC` (`Fresh`)

[☕ Daily Morning Briefing](https://bobmahalo.github.io/morning-briefing/) | [📈 $100K Model Portfolio](https://bobmahalo.github.io/morning-briefing/PORTFOLIO.html) | [🎯 Tactical Dip Radar](https://bobmahalo.github.io/morning-briefing/TACTICAL_DIP.html) | [🗂️ Single Stock Directory](https://bobmahalo.github.io/Single-Stock-Scan/)  
[🎓 Master Curriculum](https://bobmahalo.github.io/morning-briefing/CURRICULUM.html) | [🔬 SSR Executive Curriculum](https://bobmahalo.github.io/morning-briefing/SSR_CURRICULUM.html) | [📘 Tactical Dip Curriculum](https://bobmahalo.github.io/morning-briefing/TACTICAL_CURRICULUM.html) | [🗄️ Open SEC Data Lake](https://bobmahalo.github.io/morning-briefing/DATA_LAKE.html)

> **🏛️ True Stock Ownership & Custody Education:** Holding shares in broker "Street Name" means you only hold a beneficial entitlement while Cede & Co. holds legal title. Learn how Direct Registration (DRS) protects your shares from broker insolvency and short-lending at **[WhyDRS.org](https://www.whydrs.org)** ([Advocacy](https://www.whydrs.org/advocacy) | [Free Resources](https://www.whydrs.org/free-resources)).

> **Disclaimer:** *This report and open dataset are for educational and informational purposes only and do not constitute financial advice. The author is not a licensed financial advisor. All investments carry risk, and you should conduct your own due diligence before making any financial decisions.*

## 1. Centralized SEC XBRL Data Lake (Direct Download & Query Endpoints)

Instead of burning paid API tokens querying slow-moving quarterly balance sheets one ticker at a time, this repository compiles the SEC EDGAR nightly bulk archives (`companyfacts.zip` + `submissions.zip`, `~2.8 GB` raw XBRL) through a deterministic CPA tag-fallback normalizer into a compact **`~2.6 MB`** dataset covering **`5,341` `10-K`/`10-Q` companies** across **`68` columns**. `SIC 6000–6799` Financials & REITs are retained in the master table (`Is_Financial_Or_REIT = True`) while excluded from operating Hunting Buckets and Stage 1 (alongside stale or deregistered/regime-shifted filers) and surfaced separately in `Financial_REIT_Signals.csv` (`219` pinned signals). Updated every weekend.

| Dataset Artifact | Scope & Row Count | Format | Direct Download / Query Link | Raw GitHub Endpoint (For Scripts & Bots) |
| :--- | :--- | :---: | :---: | :---: |
| **Master Universe (All Scanned Filers)** | `5,341` rows × `68` cols | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Master_Universe_All_Stocks.csv) | [`raw/.../Master_Universe_All_Stocks.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Master_Universe_All_Stocks.csv) |
| **Master Universe SQLite Database** | `5,341` rows (`master_universe` table) | `SQLite3` | [📥 Download SQLite](https://bobmahalo.github.io/morning-briefing/data/master_universe.sqlite) | [`raw/.../master_universe.sqlite`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/master_universe.sqlite) |
| **Non-Dilutive Operating Hunting Buckets** | `955` fresh operating rows (`>= 1` bucket, non-Fin/REIT) | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Hunting_Buckets_Sub5_and_DeepValue.csv) | [`raw/.../Hunting_Buckets_Sub5_and_DeepValue.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Hunting_Buckets_Sub5_and_DeepValue.csv) |
| **Stage 1 Forensic Convergence Shortlist** | `15` fresh operating multi-bucket survivors | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Stage1_Convergence_Shortlist.csv) | [`raw/.../Stage1_Convergence_Shortlist.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Stage1_Convergence_Shortlist.csv) |
| **Financials & REITs Pinned Signals** | `219` fresh `SIC 6000–6799` buyback/insider signals | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Financial_REIT_Signals.csv) | [`raw/.../Financial_REIT_Signals.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Financial_REIT_Signals.csv) |
| **CPA XBRL Tag Fallback Dictionary** | Ranked `us-gaap` aliases & derived identities | `YAML` | [📥 View YAML](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml) | [`raw/.../xbrl_aliases.yaml`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/xbrl_aliases.yaml) |

<details markdown="1">
<summary>⚡ <b>Quick-Start Code Snippets: Query All `5,341` Stocks in 1 Line (Python, SQLite, Google Sheets — Zero API Tokens)</b></summary>

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
> Every weekend, the bulk scanner rebuilds all `5,341` rows from scratch out of the SEC EDGAR bulk archives. If a contributor manually edits a CSV, the next weekend refresh will overwrite it—and manual CSV edits cannot be audited for lookahead bias or unit errors.

| Contribution Type | Where It Lives in the Pipeline | How to Propose an Upgrade | Community Benefit |
| :--- | :--- | :--- | :--- |
| **1. Missing CPA XBRL Tag Fallback** | [`xbrl_aliases.yaml`](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml) | Identify a ticker where a standard GAAP line item shows `NR` due to an unusual CPA taxonomy tag and submit the `us-gaap:TagName` rank order. | Eliminates blank cells across all filers using that accounting convention. |
| **2. New Un-Opinionated Fundamental Column** | `models/wide_net_scoreboard.py` | Propose a deterministic accounting ratio or balance-sheet metric built from SEC `10-K`/`10-Q` line items (e.g., Interest Coverage, Cash Conversion Cycle, Gross Profitability). | Once verified by `pytest`, our weekend engine compiles and hosts your column across all `5,341` stocks automatically every week. |
| **3. Custom Strategy Sieve / Factor Idea** | Community Discussion / PR | Use Columns `1–60` (pure fundamentals & forensics) to test your own risk-tolerance rules, then share high-signal mathematical sieves for review. | Shared alpha discovery without duplicating `2.8 GB` SEC data pulls. |

</details>

---

## 2. Wide-Net Market Scanner: Universe Health & 4 Hunting Buckets

- **Total Operating `10-K`/`10-Q` Companies Scanned:** `5,341` (`4,697` non-dilutive operating filers + `644` quarantined by Step A Dilution Sieve)
- **Companies with Live Exchange Price:** `4,354` (`1,187` trading at `<= $5.00/sh`)
- **Stage 1 Multi-Bucket Forensic Survivors:** `15` companies passing all binary solvency, dilution, and F-Score gates

### Summary of the 4 Hunting Buckets

| Hunting Bucket | Total Qualifiers | Sub-$5.00 (`<= $5`) | `$5.01 - $20.00` | `> $20.00` |
| :--- | ---: | ---: | ---: | ---: |
| **1. Net Cash Floor / Graham Net-Net (`Bucket_1_Net_Cash_Floor`)** | **400** | `191` | `144` | `65` |
| **2. High-FCF Deep Value Turnaround (`Bucket_2_High_FCF_Turnaround`)** | **148** | `37` | `48` | `63` |
| **3. Cannibal Share Buybacks (`Bucket_3_Cannibal_Buybacks`)** | **308** | `8` | `51` | `249` |
| **4. C-Suite / Cluster Insider Buying (`Bucket_4_Cluster_Insider_Buy`)** | **339** | `130` | `97` | `102` |

## Bucket 1: Net Cash Floor & Graham Net-Nets (`Bucket_1_Net_Cash_Floor`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **MBIO** | MUSTANG BIO, INC. | `$0.37` | $2.49M | `$2.12` | `$1.41` | `$0.98` | **NR** | `7.92%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **APRE** | Aprea Therapeutics, Inc. | `$0.49` | $6.95M | `$2.67` | `$2.43` | `$2.40` | **NR** | `124.88%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **INHD** | INNO HOLDINGS INC. | `$2.82` | $7.11M | `$13.10` | `$21.38` | `$22.07` | **NR** | `-67.47%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **AUUD** | AUDDIA INC. | `$0.19` | $1.33M | `$0.87` | `$0.81` | `$1.24` | **NR** | `122.92%` | `4/9` | `1_NET_CASH_FLOOR` |
| **CDT** | CDT Equity Inc. | `$0.27` | $0.51M | `$0.90` | `$-9.44` | `$71.78` | **NR** | `16.62%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **REVB** | REVELATION BIOSCIENCES, INC. | `$3.68` | $2.52M | `$12.17` | `$9.48` | `$10.58` | **NR** | `-88.46%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MSAI** | MultiSensor AI Holdings, Inc | `$2.84` | $6.30M | `$9.15` | `$10.17` | `$12.05` | **NR** | `-95.78%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **CTNT** | CHEETAH NET SUPPLY CHAIN SER | `$1.56` | $4.17M | `$4.83` | `$32.40` | `$32.67` | **NR** | `66.91%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **APVO** | Aptevo Therapeutics Inc. | `$0.41` | $1.43M | `$1.24` | `$0.06` | `$1.11` | **NR** | `-79.44%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **AIFA** | All In FutureTech Alliance,  | `$2.94` | $18.88M | `$8.75` | `$3.08` | `$4.26` | **-52.47%** | `-83.11%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PLRX** | PLIANT THERAPEUTICS, INC. | `$0.62` | $38.43M | `$1.83` | `$1.63` | `$2.04` | **-173.77%** | `0.88%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PHUN** | Phunware, Inc. | `$1.47` | $30.39M | `$4.17` | `$3.94` | `$3.96` | **NR** | `2.42%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PEW** | GrabAGun Digital Holdings In | `$1.30` | $38.47M | `$3.25` | `$2.84` | `$3.38` | **-47.56%** | `-1.41%` | `4/9` | `1_NET_CASH_FLOOR` |
| **FBIO** | Fortress Biotech, Inc. | `$1.77` | $59.73M | `$4.11` | `$3.18` | `$4.74` | **NR** | `1.95%` | `4/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **XLO** | Xilio Therapeutics, Inc. | `$7.51` | $53.05M | `$16.45` | `$8.48` | `$9.66` | **-108.62%** | `-86.54%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **XPON** | Expion Energy, Inc. | `$2.10` | $2.13M | `$4.54` | `$0.73` | `$6.01` | **NR** | `-89.52%` | `5/9` | `1_NET_CASH_FLOOR` |
| **BCYC** | BICYCLE THERAPEUTICS PLC | `$3.05` | $213.44M | `$6.52` | `$6.80` | `$7.22` | **-82.94%** | `0.98%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **SRXH** | SRX Global Inc. | `$1.01` | $20.57M | `$1.89` | `$3.10` | `$3.11` | **NR** | `3,258.64%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **QNT** | Quantinuum Inc. | `$27.96` | $1,029.12M | `$51.73` | `$51.99` | `$-8.62` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **MSN** | EMERSON RADIO CORP | `$0.27` | $5.72M | `$0.48` | `$0.72` | `$0.74` | **-65.04%** | `0.00%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **SCYX** | SCYNEXIS INC | `$2.60` | $25.93M | `$4.56` | `$4.16` | `$5.93` | **NR** | `-76.28%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MRLN** | Merlin, Inc. | `$0.88` | $91.06M | `$1.54` | `$1.21` | `$-0.25` | **NR** | `45.22%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **TVRD** | Tvardi Therapeutics, Inc. | `$0.95` | $12.64M | `$1.65` | `$1.13` | `$1.14` | **NR** | `42.45%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **OPAL** | OPAL Fuels Inc. | `$1.41` | $41.79M | `$2.45` | `$-11.57` | `$-0.54` | **-44.55%** | `4.82%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **LABT** | Lakewood-Amedex Biotherapeut | `$0.21` | $1.91M | `$0.36` | `$0.32` | `$0.33` | **NR** | `243.62%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **IMA** | ImageneBio, Inc. | `$3.98` | $49.58M | `$6.71` | `$9.33` | `$10.29` | **NR** | `11.40%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **ALDX** | Aldeyra Therapeutics, Inc. | `$0.72` | $43.56M | `$1.15` | `$0.58` | `$0.58` | **NR** | `0.32%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **ABOS** | Acumen Pharmaceuticals, Inc. | `$0.19` | $13.98M | `$0.30` | `$0.47` | `$0.48` | **NR** | `19.40%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **RNA** | Atrium Therapeutics, Inc. | `$6.98` | $150.57M | `$10.73` | `$9.23` | `$9.50` | **-41.28%** | `-0.40%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **KAPA** | Kairos Pharma, LTD. | `$0.45` | $2.11M | `$0.67` | `$0.61` | `$0.81` | **NR** | `-77.50%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **JANX** | Janux Therapeutics, Inc. | `$10.29` | $629.58M | `$15.12` | `$14.50` | `$14.90` | **-8.60%** | `1.72%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MYPS** | PLAYSTUDIOS, Inc. | `$5.18` | $62.39M | `$7.59` | `$6.29` | `$8.07` | **32.50%** | `-4.18%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **EROC** | ERock, Inc. | `$7.25` | $349.26M | `$10.61` | `$2.11` | `NR` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **GTBP** | GT Biopharma, Inc. | `$3.18` | $6.80M | `$4.64` | `$3.65` | `$3.65` | **NR** | `-79.91%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **IVDA** | Iveda Solutions, Inc. | `$0.18` | $2.41M | `$0.25` | `$0.34` | `$0.36` | **NR** | `127.32%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **NNDM** | Nano Dimension Ltd. | `$1.12` | $222.02M | `$1.56` | `$1.98` | `$2.78` | **NR** | `-4.32%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **INVE** | INVE Technologies, Inc. | `$2.65` | $63.23M | `$3.60` | `$3.38` | `$5.49` | **NR** | `0.44%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **JTAI** | Jet.AI Inc. | `$0.59` | $2.10M | `$0.77` | `$-0.12` | `$7.33` | **NR** | `-8.80%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **ELOX** | Eloxx Pharmaceuticals, Inc. | `$10.66` | $43.56M | `$13.77` | `$10.05` | `$10.05` | **NR** | `1,787.34%` | `2/9` | `1_NET_CASH_FLOOR` |
| **RXST** | RxSight, Inc. | `$4.61` | $193.29M | `$5.83` | `$5.47` | `$6.08` | **9.65%** | `1.98%` | `NR/9` | `1_NET_CASH_FLOOR` |

## Bucket 2: High-FCF Deep Value Turnarounds (`Bucket_2_High_FCF_Turnaround`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **PAAI** | Paradium.AI, Inc. | `$0.46` | $21.81M | `$-1.88` | `$-1.79` | `$-1.14` | **179.98%** | `0.31%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **AMS** | AMERICAN SHARED HOSPITAL SER | `$1.02` | $6.81M | `$0.44` | `$-1.32` | `$3.19` | **101.52%** | `2.02%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **FLUX** | Flux Power Holdings, Inc. | `$0.23` | $5.15M | `$-0.07` | `$-0.17` | `$-0.05` | **96.34%** | `2.92%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **MKTW** | MARKETWISE, INC. | `$20.07` | $58.91M | `$7.34` | `$-124.76` | `$-23.43` | **88.46%** | `12.97%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**CRMD**](https://bobmahalo.github.io/Single-Stock-Scan/CRMD.html) | CorMedix Inc. | `$5.08` | $404.05M | `$4.42` | `$0.59` | `$1.05` | **76.19%** | `0.95%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **EBS** | Emergent BioSolutions Inc. | `$5.16` | $265.30M | `$-6.57` | `$-2.41` | `$1.18` | **71.01%** | `-2.10%` | `7/9` | `2_HIGH_FCF_TURNAROUND` |
| **CMTL** | COMTECH TELECOMMUNICATIONS C | `$1.07` | $32.25M | `$0.74` | `$-6.36` | `$-4.55` | **68.80%** | `1.50%` | `5/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **XRX** | Xerox Holdings Corp | `$0.86` | $114.56M | `$-0.54` | `$-40.97` | `$-20.89` | **66.34%** | `4.04%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **KODK** | EASTMAN KODAK CO | `$7.98` | $778.05M | `$2.04` | `$-0.18` | `$6.41` | **59.76%** | `20.97%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **TTEC** | TTEC Holdings, Inc. | `$2.82` | $139.26M | `$0.42` | `$-13.71` | `NR` | **56.45%** | `1.72%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**CRWS**](https://bobmahalo.github.io/Single-Stock-Scan/CRWS.html) | CROWN CRAFTS INC | `$2.36` | $25.66M | `$-1.25` | `$2.00` | `$3.26` | **54.69%** | `1.58%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PLTK** | Playtika Holding Corp. | `$2.51` | $960.51M | `$-5.00` | `$-7.61` | `$-6.27` | **50.11%** | `1.76%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**DXC**](https://bobmahalo.github.io/Single-Stock-Scan/DXC.html) | DXC Technology Co | `$13.33` | $2,072.42M | `$-13.47` | `$-25.16` | `$16.27` | **49.70%** | `-10.72%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **PAGP** | PLAINS GP HOLDINGS LP | `$25.87` | $5,124.88M | `$3.34` | `$3.02` | `NR` | **44.31%** | `0.11%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **COLL** | COLLEGIUM PHARMACEUTICAL, IN | `$25.21` | $783.41M | `$4.48` | `$-38.22` | `$-33.21` | **42.93%** | `-1.69%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**DLTH**](https://bobmahalo.github.io/Single-Stock-Scan/DLTH.html) | DULUTH HOLDINGS INC. | `$3.91` | $142.25M | `$-1.71` | `$-0.99` | `$4.88` | **40.45%** | `4.98%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **SENEA** | Seneca Foods Corp | `$34.57` | $236.36M | `$-0.87` | `$46.62` | `$117.32` | **38.56%** | `-1.61%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **SSTK** | Shutterstock, Inc. | `$2.36` | $87.52M | `$-0.63` | `$-11.46` | `$-0.68` | **34.99%** | `4.43%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **PBF** | PBF Energy Inc. | `$61.58` | $7,559.34M | `$-0.95` | `$-8.95` | `$64.81` | **34.72%** | `4.07%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **UFI** | UNIFI INC | `$5.62` | $104.47M | `$1.08` | `$3.31` | `NR` | **33.46%** | `1.24%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **VSNT** | Versant Media Group, Inc. | `$35.60` | $4,931.95M | `$-12.72` | `$-10.94` | `$-0.65` | **33.25%** | `-3.91%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **TBLA** | Taboola.com Ltd. | `$1.85` | $528.73M | `$-0.09` | `$-0.13` | `$1.31` | **33.08%** | `-6.50%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **DK** | Delek US Holdings, Inc. | `$60.25` | $3,652.00M | `$-34.77` | `$-41.51` | `NR` | **32.90%** | `0.94%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **MYPS** | PLAYSTUDIOS, Inc. | `$5.18` | $62.39M | `$7.59` | `$6.29` | `$8.07` | **32.50%** | `-4.18%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| [**NRDS**](https://bobmahalo.github.io/Single-Stock-Scan/NRDS.html) | NERDWALLET, INC. | `$7.02` | $454.19M | `$1.03` | `$2.01` | `$3.11` | **32.14%** | `-15.86%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **AERT** | Aeries Technology, Inc. | `$4.02` | $25.48M | `$-0.52` | `$-2.71` | `$-0.26` | **32.05%** | `7.19%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **PARR** | PAR PACIFIC HOLDINGS, INC. | `$64.36` | $3,222.95M | `$-2.48` | `$5.56` | `$43.80` | **31.86%** | `-0.43%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **LCUT** | LIFETIME BRANDS, INC | `$7.20` | $165.49M | `$-4.42` | `$9.99` | `$3.49` | **30.66%** | `1.45%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **IMXI** | International Money Express, | `$5.36` | $161.98M | `$0.63` | `$1.08` | `$3.18` | **29.43%** | `1.69%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **IPM** | INTELLIGENT PROTECTION MANAG | `$1.63` | $14.73M | `$0.71` | `$-0.11` | `$0.47` | **29.07%** | `-0.55%` | `5/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **DSP** | Viant Technology Inc. | `$11.00` | $233.45M | `$7.64` | `$7.99` | `$3.88` | **28.81%** | `10.66%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **JVA** | COFFEE HOLDING CO INC | `$5.04` | $28.77M | `$0.17` | `$4.29` | `$5.43` | **27.73%** | `0.00%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **IMMR** | IMMERSION CORP | `$6.71` | $222.81M | `$4.17` | `$5.82` | `$6.92` | **27.44%** | `2.11%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **HBB** | Hamilton Beach Brands Holdin | `$29.51` | $397.09M | `$3.90` | `$10.43` | `$15.88` | **27.00%** | `-0.38%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **PMTS** | CPI Card Group Inc. | `$25.91` | $301.39M | `$-21.98` | `$-17.96` | `$-6.75` | **26.99%** | `2.15%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **VHI** | VALHI INC /DE/ | `$15.67` | $443.79M | `$6.97` | `$30.15` | `$24.45` | **26.72%** | `0.07%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **ADT** | ADT Inc. | `$9.88` | $7,221.30M | `$-8.77` | `$-15.53` | `$-8.38` | **26.69%** | `NR` | `7/9` | `2_HIGH_FCF_TURNAROUND` |
| **MSGM** | Motorsport Games Inc. | `$3.73` | $20.01M | `$0.96` | `$0.47` | `$0.34` | **26.26%** | `-1.67%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **HCAT** | Health Catalyst, Inc. | `$1.29` | $98.24M | `$0.83` | `$0.54` | `$1.11` | **26.17%** | `7.67%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **YELP** | YELP INC | `$18.56` | $1,011.39M | `$1.80` | `$-0.31` | `$4.26` | **26.01%** | `-11.38%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |

## Bucket 3: Cannibal Buybacks (`Bucket_3_Cannibal_Buybacks`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **AMCX** | AMC Global Media Inc. | `$8.90` | $372.44M | `$-31.01` | `$-35.26` | `$12.86` | **25.80%** | `-25.64%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **BTMD** | biote Corp. | `$0.84` | $23.16M | `$-4.23` | `$-4.29` | `$-2.72` | **31.99%** | `-25.32%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **IBTA** | Ibotta, Inc. | `$53.99` | $1,260.61M | `$5.34` | `$5.21` | `$10.21` | **6.46%** | `-20.52%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **FOUR** | Shift4 Payments, Inc. | `$37.95` | $2,844.12M | `$-48.68` | `$-67.53` | `$-17.16` | **21.94%** | `-20.08%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **PAYC** | Paycom Software, Inc. | `$240.02` | $10,809.25M | `$-13.98` | `$-21.99` | `$13.95` | **6.10%** | `-19.97%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **YEXT** | Yext, Inc. | `$7.16` | $708.19M | `$-1.36` | `$-2.52` | `$-0.76` | **7.48%** | `-19.68%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **PRKS** | United Parks & Resorts Inc. | `$39.23` | $1,782.27M | `$-51.76` | `$-64.88` | `$-13.19` | **8.43%** | `-16.71%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **ZD** | ZIFF DAVIS, INC. | `$49.68` | $1,644.52M | `$20.04` | `$8.40` | `$18.25` | **6.60%** | `-16.21%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **PINS** | PINTEREST, INC. | `$16.88` | $9,835.17M | `$-1.00` | `$1.18` | `$4.37` | **12.83%** | `-16.11%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| [**NRDS**](https://bobmahalo.github.io/Single-Stock-Scan/NRDS.html) | NERDWALLET, INC. | `$7.02` | $454.19M | `$1.03` | `$2.01` | `$3.11` | **32.14%** | `-15.86%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **PD** | PagerDuty, Inc. | `$15.78` | $1,240.70M | `$-2.28` | `$-1.68` | `$1.03` | **10.21%** | `-15.65%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **BFAM** | BRIGHT HORIZONS FAMILY SOLUT | `$49.79` | $2,386.49M | `$-35.42` | `$-50.00` | `$-22.54` | **10.61%** | `-15.25%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **DBX** | DROPBOX, INC. | `$33.80` | $7,608.38M | `$0.16` | `$-16.59` | `$-11.89` | **12.03%** | `-15.09%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **DIN** | Dine Brands Global, Inc. | `$36.63` | $450.37M | `$-126.16` | `$-143.12` | `$-86.47` | **11.86%** | `-14.76%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **PGNY** | Progyny, Inc. | `$35.45` | $2,610.80M | `$1.24` | `$2.75` | `$5.35` | **6.88%** | `-14.57%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| [**HOG**](https://bobmahalo.github.io/Single-Stock-Scan/HOG.html) | HARLEY-DAVIDSON, INC. | `$32.69` | $3,301.44M | `$-3.41` | `$2.82` | `$29.39` | **9.45%** | `-14.52%` | `8/9` | `1_NET_CASH_FLOOR | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **CHTR** | CHARTER COMMUNICATIONS, INC. | `$133.18` | $15,574.66M | `$-905.82` | `$-987.46` | `$-160.46` | **25.23%** | `-14.26%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **BILL** | BILL Holdings, Inc. | `$64.11` | $5,505.96M | `$-6.14` | `$6.49` | `$8.80` | **7.51%** | `-14.25%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CRM** | Salesforce, Inc. | `$183.41` | $150,946.43M | `$-40.62` | `$-59.73` | `$-32.82` | **10.04%** | `-13.55%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **MIDD** | MIDDLEBY Corp | `$134.69` | $5,866.49M | `$-39.36` | `$-26.32` | `$-18.52` | **6.34%** | `-13.53%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CPRI** | Capri Holdings Ltd | `$18.50` | $1,911.97M | `$-13.17` | `$-19.09` | `$-6.61` | **9.62%** | `-13.26%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **IIIV** | i3 Verticals, Inc. | `$19.94` | $592.34M | `$-0.05` | `$-6.13` | `$-5.60` | **9.00%** | `-13.10%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **SMPL** | Simply Good Foods Co | `$11.97` | $1,039.74M | `$-2.50` | `$-1.74` | `$-0.61` | **15.09%** | `-13.01%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **CARS** | Cars.com Inc. | `$12.36` | $643.40M | `$-7.58` | `$-6.77` | `$-4.06` | **23.40%** | `-12.94%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **ETSY** | ETSY INC | `$78.72` | $6,786.13M | `$23.50` | `$-14.41` | `$-8.30` | **8.73%** | `-12.66%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **TENB** | Tenable Holdings, Inc. | `$44.09` | $4,607.74M | `$-3.31` | `$-9.45` | `$-7.84` | **6.09%** | `-12.43%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **AN** | AUTONATION, INC. | `$176.06` | $5,631.02M | `$-12.80` | `$-44.16` | `$-12.65` | **0.41%** | `-12.31%` | `5/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **ZG** | ZILLOW GROUP, INC. | `$27.57` | $6,211.66M | `$2.28` | `$3.01` | `$5.11` | **5.04%** | `-12.07%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CROX** | Crocs, Inc. | `$157.31` | $7,193.01M | `$-32.80` | `$-41.73` | `$-8.13` | **10.48%** | `-11.92%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **FCN** | FTI CONSULTING, INC | `$203.47` | $5,545.41M | `$-36.68` | `$-21.74` | `$2.62` | **6.38%** | `-11.73%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **YELP** | YELP INC | `$18.56` | $1,011.39M | `$1.80` | `$-0.31` | `$4.26` | **26.01%** | `-11.38%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **HGV** | Hilton Grand Vacations Inc. | `$44.65` | $3,385.48M | `NR` | `NR` | `$-8.97` | **13.97%** | `-11.36%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| [**PYPL**](https://bobmahalo.github.io/Single-Stock-Scan/PYPL.html) | PayPal Holdings, Inc. | `$56.37` | $46,824.21M | `$-4.77` | `$-1.91` | `$10.25` | **13.45%** | `-11.22%` | `8/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **UTMD** | UTAH MEDICAL PRODUCTS INC | `$70.96` | $202.20M | `$29.80` | `$33.48` | `$37.00` | **5.37%** | `-11.05%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **DVA** | DAVITA INC. | `$156.29` | $9,830.64M | `$-33.83` | `$-200.57` | `$-132.91` | **13.16%** | `-10.91%` | `7/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| [**DXC**](https://bobmahalo.github.io/Single-Stock-Scan/DXC.html) | DXC Technology Co | `$13.33` | $2,072.42M | `$-13.47` | `$-25.16` | `$16.27` | **49.70%** | `-10.72%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| [**ZUMZ**](https://bobmahalo.github.io/Single-Stock-Scan/ZUMZ.html) | Zumiez Inc | `$13.21` | $202.52M | `$-11.54` | `$-3.40` | `$16.20` | **12.38%** | `-10.63%` | `8/9` | `1_NET_CASH_FLOOR | 3_CANNIBAL_BUYBACKS` |
| **GDDY** | GoDaddy Inc. | `$102.13` | $12,385.79M | `NR` | `NR` | `$-38.78` | **14.08%** | `-10.26%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CVEO** | Civeo Corp | `$33.09` | $341.99M | `$-19.77` | `$-16.46` | `$6.95` | **8.63%** | `-10.23%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **DHX** | DHI GROUP, INC. | `$4.01` | $170.33M | `$-0.83` | `$-1.66` | `$-1.08` | **13.07%** | `-9.93%` | `4/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |

## Bucket 4: Cluster & C-Suite Insider Buying (`Bucket_4_Cluster_Insider_Buy`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **PBLS** | Parabilis Medicines, Inc. | `$27.62` | $3,414.26M | `$3.89` | `$6.09` | `$8.13` | **NR** | `6,021.17%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **MAIR** | Madison Air Solutions Corp | `$23.20` | $12,297.68M | `$4.73` | `$-1.88` | `$-0.85` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BRVE** | Braveheart Bio, Inc. | `$19.27` | $1,731.80M | `$1.34` | `$3.81` | `$5.54` | **NR** | `1,765.60%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SMMT** | Summit Therapeutics Inc. | `$10.57` | $8,453.50M | `$0.76` | `$0.67` | `$0.70` | **-6.23%** | `7.43%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ROL** | ROLLINS INC | `$37.97` | $18,148.99M | `$-0.56` | `$-2.84` | `$-1.39` | **3.70%** | `-1.36%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| [**GME**](https://bobmahalo.github.io/Single-Stock-Scan/GME.html) | GameStop Corp. | `$26.97` | $13,606.39M | `$1.03` | `$1.83` | `$12.17` | **5.06%** | `12.70%` | `6/9` | `4_CLUSTER_INSIDER_BUY` |
| **KARD** | Kardigan, Inc. | `$12.52` | $1,171.84M | `$0.71` | `$4.36` | `$5.83` | **NR** | `643.69%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ADRX** | ADARx Pharmaceuticals, Inc. | `$14.16` | $1,574.50M | `$8.04` | `$5.07` | `$5.17` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **DPC** | DPC Holdings PLC | `$34.20` | $5,109.24M | `$1.37` | `$1.93` | `$4.42` | **NR** | `32.56%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SCTX** | Scribe Therapeutics, Inc. | `$13.22` | $250.35M | `$8.81` | `$6.13` | `$6.61` | **NR** | `496.86%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **LFTO** | Liftoff Mobile, Inc. | `$23.66` | $4,009.05M | `$-5.92` | `$-7.45` | `$-6.47` | **NR** | `25.65%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **LILA** | Liberty Latin America Ltd. | `$9.38` | $1,826.29M | `$-0.25` | `$-46.82` | `$-13.43` | **NR** | `-6.26%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ATTO** | Attovia Therapeutics, Inc. | `$15.58` | $712.20M | `$2.44` | `$8.54` | `$8.70` | **NR** | `654.04%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **LYEL** | Lyell Immunopharma, Inc. | `$13.58` | $333.87M | `$1.94` | `$4.27` | `$7.84` | **-41.92%** | `15.87%` | `2/9` | `4_CLUSTER_INSIDER_BUY` |
| **ETRA** | Electra Therapeutics, Inc. | `$8.94` | $562.03M | `$4.05` | `$6.19` | `$6.25` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **AVO** | Mission Produce, Inc. | `$11.30` | $990.77M | `$-4.88` | `$-4.62` | `$5.65` | **-0.23%** | `24.16%` | `8/9` | `4_CLUSTER_INSIDER_BUY` |
| **AVR** | Anteris Technologies Global  | `$5.09` | $496.24M | `$2.06` | `$2.07` | `$2.33` | **-18.84%** | `136.65%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| [**LRN**](https://bobmahalo.github.io/Single-Stock-Scan/LRN.html) | Stride, Inc. | `$76.24` | $3,205.80M | `$2.83` | `$21.29` | `$33.67` | **15.74%** | `-4.13%` | `7/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **FUN** | Six Flags Entertainment Corp | `$11.84` | $1,211.35M | `$-47.59` | `$-53.15` | `$-22.78` | **NR** | `0.82%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **QTTB** | Q32 Bio Inc. | `$8.48` | $253.75M | `$9.51` | `$9.41` | `$9.61` | **-13.22%** | `143.20%` | `3/9` | `4_CLUSTER_INSIDER_BUY` |
| **SUJA** | SUJA LIFE, INC. | `$6.35` | $151.06M | `NR` | `NR` | `NR` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **MSM** | MSC INDUSTRIAL DIRECT CO INC | `$107.28` | $5,992.19M | `$-2.61` | `$4.23` | `$11.31` | **3.76%** | `0.12%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **CGON** | CG Oncology, Inc. | `$81.90` | $7,315.22M | `$0.21` | `$10.66` | `$10.98` | **-2.59%** | `10.73%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BLSM** | BlossomHill Therapeutics, In | `$14.41` | $458.02M | `$7.08` | `NR` | `$6.64` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **QNT** | Quantinuum Inc. | `$27.96` | $1,029.12M | `$51.73` | `$51.99` | `$-8.62` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **RAPP** | Rapport Therapeutics, Inc. | `$23.59` | $1,398.41M | `$6.51` | `$6.41` | `$6.60` | **-8.67%** | `24.38%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **NTSK** | Netskope Inc | `$24.80` | $10,045.14M | `$0.46` | `$-0.42` | `$0.19` | **-0.70%** | `274.71%` | `6/9` | `4_CLUSTER_INSIDER_BUY` |
| **ET** | Energy Transfer LP | `NR` | NR | `$-20.26` | `$-19.03` | `NR` | **NR** | `0.32%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **CV** | CapsoVision, Inc | `$6.31` | $338.28M | `NR` | `NR` | `$0.49` | **-8.65%** | `14.44%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **UBER** | Uber Technologies, Inc | `$65.61` | $133,968.93M | `$-4.01` | `$-11.87` | `$7.69` | **7.78%** | `-1.73%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| **FBIN** | Fortune Brands Innovations,  | `$47.28` | $5,601.53M | `$-19.94` | `$-15.91` | `NR` | **9.90%** | `-1.38%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **AMR** | Alpha Metallurgical Resource | `$135.48` | $1,715.45M | `$24.91` | `$7.16` | `$114.49` | **NR** | `-1.52%` | `4/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **PMTS** | CPI Card Group Inc. | `$25.91` | $301.39M | `$-21.98` | `$-17.96` | `$-6.75` | **26.99%** | `2.15%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **TUSK** | MAMMOTH ENERGY SERVICES, INC | `$3.22` | $154.97M | `$0.19` | `$0.62` | `$5.43` | **-92.18%** | `-0.14%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **ANGX** | Angel Studios, Inc. | `$4.18` | $792.42M | `$0.22` | `$-0.90` | `NR` | **NR** | `20.76%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ACDC** | ProFrac Holding Corp. | `$2.94` | $536.35M | `$-5.48` | `$-6.42` | `$0.71` | **-2.96%** | `0.69%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **CDNL** | Cardinal Infrastructure Grou | `$5.18` | $106.69M | `NR` | `NR` | `$1.53` | **-11.04%** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BSX** | BOSTON SCIENTIFIC CORP | `$43.00` | $62,327.35M | `$-0.67` | `$1.51` | `$0.02` | **5.34%** | `-2.22%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **GLOO** | Gloo Holdings, Inc. | `$2.56` | $215.29M | `$-0.01` | `$-0.52` | `$-0.24` | **-30.79%** | `923.44%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **LWAY** | Lifeway Foods, Inc. | `$19.54` | $295.22M | `$0.43` | `$-0.08` | `$4.52` | **-11.94%** | `-0.79%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |

---

<details markdown="1">
<summary><b>📖 Open SEC Data Lake Methodology, `68`-Column Schema Dictionary & Forensic Formulas (Click to Expand)</b></summary>

### 1. Why a Normalized SEC XBRL Data Lake?
Publicly traded U.S. operating companies file quarterly (`10-Q`) and annual (`10-K`) financial statements with the SEC using XBRL (`us-gaap` taxonomy). Because different CPA firms use different XBRL tags for identical economic concepts, raw SEC queries frequently return blank cells (`NR`). Our ingestion layer maps ranked tag hierarchies and derived accounting identities ([`xbrl_aliases.yaml`](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml)) across **`5,341` active `10-K`/`10-Q` operating companies**, computes discrete Q4 values ($\text{FY} - \text{YTD}_3$), applies 1,000x share-unit scaling guards, and exports **`68` standardized columns**.

### 2. Schema Separation: Un-Opinionated Building Blocks vs. Strategy Buckets

| Column Group | Column Names / Examples | Intended Use Case |
| :--- | :--- | :--- |
| **Identity & Classification (`Cols 1–8`)** | `Ticker`, `CIK`, `Company_Name`, `Exchange`, `SIC_Code`, `SIC_Description`, `Is_Financial_Or_REIT`, `Latest_Period_End` | Universe filtering, sector/SIC peer benchmarking, and filing freshness checks. |
| **Market Pricing & Enterprise Scale (`Cols 9–13`)** | `Share_Price`, `Google_Sheets_Live_Price_Formula`, `Shares_Outstanding_M`, `Market_Cap_M`, `Enterprise_Value_M` | Live valuation multiples and Google Sheets integration. |
| **Per-Share Liquidation Floors & Yields (`Cols 14–24`)** | `Net_Cash_Ex_Debt_Per_Share`, `Graham_NCAV_Per_Share`, `Tangible_Book_Per_Share`, `FCF_Per_Share_TTM`, `FCF_to_Price_Yield_Pct`, `EBIT_to_EV_Yield_Pct` | Downside floor anchoring and inverted yield ranking (avoids negative-denominator P/E distortion). |
| **Raw TTM Flow & Balance Sheet Totals (`Cols 25–39`)** | `Revenue_TTM_M`, `Operating_Income_TTM_M`, `Net_Income_TTM_M`, `Operating_Cash_Flow_TTM_M`, `Free_Cash_Flow_TTM_M`, `Total_Cash_M`, `Total_Debt_M`, `Total_Liabilities_M`, `Stock_Buybacks_TTM_M`, `Stock_Issued_TTM_M`, `Dividends_Paid_TTM_M` | Raw dollar building blocks ($M) so external quants can construct any custom formula without re-parsing SEC filings. |
| **Efficiency, Growth & Share Dilution (`Cols 40–50`)** | `Gross_Margin_TTM_Pct`, `Operating_Margin_TTM_Pct`, `ROIC_TTM_Pct`, `ROIC_5Y_Median_Pct`, `Current_Ratio`, `Revenue_5Y_CAGR_Pct`, `Share_Count_1Y_Change_Pct`, `Share_Count_5Y_CAGR_Pct`, `Shareholder_Yield_Pct` | Quality compounder screening, capital allocation audits, and cannibal buyback tracking. |
| **Forensic Accounting & Insider Flow (`Cols 51–60`)** | `Piotroski_F_Score`, `Altman_Z_Score`, `Altman_Zone`, `Beneish_M_Score`, `SBC_Pct_OCF_TTM`, `Insider_Open_Market_Buys_12M`, `Insider_C_Suite_Buyers_12M`, `Insider_Net_Buy_USD_12M` | Solvency verification, earnings manipulation screening, and OpenInsider Form 4 cluster tracking. |
| **Optional Strategy Sieves (`Cols 61–68`)** | `Is_Dilution_Vampire` (`644` flagged), `Bucket_1_Net_Cash_Floor` (`400`), `Bucket_2_High_FCF_Turnaround` (`148`), `Bucket_3_Cannibal_Buybacks` (`308`), `Bucket_4_Cluster_Insider_Buy` (`339`), `Buckets_Count` | Optional deep-value hunting buckets feeding our `15`-stock Stage 1 Convergence Shortlist. |

### 3. Core Mathematical & Forensic Formulas

| Metric | Exact Mathematical Formula | Institutional Interpretation |
| :--- | :--- | :--- |
| **Net Cash (Ex-Debt) / Share** | $$\frac{\text{Cash \& ST Investments} - \text{Total Debt}}{N_{\text{diluted}}}$$ | Hard net cash cushion per share after extinguishing 100% of funded debt. |
| **Graham NCAV / Share** | $$\frac{\text{Current Assets} - \text{Total Liabilities} - \text{Preferred Stock}}{N_{\text{diluted}}}$$ | Benjamin Graham Net-Net liquidation floor (strict arbitrage requires $P \le 0.67 \times \text{NCAV}$). |
| **Tangible Book Value (TBV) / Share** | $$\frac{\text{Stockholders' Equity} - \text{Goodwill} - \text{Intangibles}}{N_{\text{diluted}}}$$ | Physical net worth per share stripping out M&A accounting goodwill. |
| **Altman Z-Score (5-Factor)** | $$Z = 1.2 X_1 + 1.4 X_2 + 3.3 X_3 + 0.6 X_4 + 0.999 X_5$$ | Solvency index across Operating Universe (`> 2.99` Safe, `1.81–2.99` Grey, `< 1.81` Distress). |
| **Step A Dilution Quarantine** | `Share_Count_1Y_Change_Pct > 10%` or (`FCF < 0` & `Stock_Issued > 5% MCap`) | Quarantines `{vampires:,}` chronic equity diluters (`Is_Dilution_Vampire = True`). |

</details>
