# 🗄️ Open SEC XBRL Data Lake & Wide-Net Market Scanner
**Generated:** 2026-11-15 18:03 UTC | **Coverage:** `5,387` Active `10-K`/`10-Q` Operating Companies (`68` Normalized Columns)

[☕ Daily Morning Briefing](https://bobmahalo.github.io/morning-briefing/) | [📈 $100K Model Portfolio](https://bobmahalo.github.io/morning-briefing/PORTFOLIO.html) | [🗄️ Open SEC Data Lake](https://bobmahalo.github.io/morning-briefing/DATA_LAKE.html) | [🏛️ S&P 1500 Screen](https://bobmahalo.github.io/morning-briefing/SP1500_SCREEN.html) | [🎓 Master Curriculum](https://bobmahalo.github.io/morning-briefing/CURRICULUM.html) | [🔬 SSR Executive Curriculum](https://bobmahalo.github.io/morning-briefing/SSR_CURRICULUM.html) | [🗂️ Single Stock Directory](https://bobmahalo.github.io/Single-Stock-Scan/)

> **🏛️ True Stock Ownership & Custody Education:** Holding shares in broker "Street Name" means you only hold a beneficial entitlement while Cede & Co. holds legal title. Learn how Direct Registration (DRS) protects your shares from broker insolvency and short-lending at **[WhyDRS.org](https://www.whydrs.org)** ([Advocacy](https://www.whydrs.org/advocacy) | [Free Resources](https://www.whydrs.org/free-resources)).

> **Disclaimer:** *This report and open dataset are for educational and informational purposes only and do not constitute financial advice. The author is not a licensed financial advisor. All investments carry risk, and you should conduct your own due diligence before making any financial decisions.*

## 1. Centralized SEC XBRL Data Lake (Direct Download & Query Endpoints)

Instead of burning paid API tokens querying slow-moving quarterly balance sheets one ticker at a time, this repository compiles the SEC EDGAR nightly bulk archives (`companyfacts.zip` + `submissions.zip`, `~2.8 GB` raw XBRL) through a deterministic CPA tag-fallback normalizer into a compact **`~2.6 MB`** dataset covering **`5,387` active `10-K`/`10-Q` operating companies** across **`68` columns** (Financials and REITs in `SIC 6000–6799` are excluded due to non-standard working capital and debt structures). Updated every weekend.

| Dataset Artifact | Scope & Row Count | Format | Direct Download / Query Link | Raw GitHub Endpoint (For Scripts & Bots) |
| :--- | :--- | :---: | :---: | :---: |
| **Master Universe (All Operating Filers)** | `5,387` rows × `68` cols | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Master_Universe_All_Stocks.csv) | [`raw/.../Master_Universe_All_Stocks.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Master_Universe_All_Stocks.csv) |
| **Master Universe SQLite Database** | `5,387` rows (`master_universe` table) | `SQLite3` | [📥 Download SQLite](https://bobmahalo.github.io/morning-briefing/data/master_universe.sqlite) | [`raw/.../master_universe.sqlite`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/master_universe.sqlite) |
| **Non-Dilutive Hunting Bucket Qualifiers** | `1,080` rows (`>= 1` bucket, non-dilutive) | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Hunting_Buckets_Sub5_and_DeepValue.csv) | [`raw/.../Hunting_Buckets_Sub5_and_DeepValue.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Hunting_Buckets_Sub5_and_DeepValue.csv) |
| **Stage 1 Forensic Convergence Shortlist** | `11` multi-bucket forensic survivors | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Stage1_Convergence_Shortlist.csv) | [`raw/.../Stage1_Convergence_Shortlist.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Stage1_Convergence_Shortlist.csv) |
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

- **Total Operating `10-K`/`10-Q` Companies Scanned:** `5,387` (`4,740` non-dilutive operating filers + `647` quarantined by Step A Dilution Sieve)
- **Companies with Live Exchange Price:** `4,356` (`1,139` trading at `<= $5.00/sh`)
- **Stage 1 Multi-Bucket Forensic Survivors:** `11` companies passing all binary solvency, dilution, and F-Score gates

### Summary of the 4 Hunting Buckets

| Hunting Bucket | Total Qualifiers | Sub-$5.00 (`<= $5`) | `$5.01 - $20.00` | `> $20.00` |
| :--- | ---: | ---: | ---: | ---: |
| **1. Net Cash Floor / Graham Net-Net (`Bucket_1_Net_Cash_Floor`)** | **378** | `180` | `141` | `57` |
| **2. High-FCF Deep Value Turnaround (`Bucket_2_High_FCF_Turnaround`)** | **130** | `32` | `43` | `55` |
| **3. Cannibal Share Buybacks (`Bucket_3_Cannibal_Buybacks`)** | **380** | `11` | `56` | `313` |
| **4. C-Suite / Cluster Insider Buying (`Bucket_4_Cluster_Insider_Buy`)** | **400** | `122` | `124` | `137` |

## Bucket 1: Net Cash Floor & Graham Net-Nets (`Bucket_1_Net_Cash_Floor`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **APRE** | Aprea Therapeutics, Inc. | `$0.50` | $7.03M | `$2.67` | `$2.43` | `$2.40` | **NR** | `124.88%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MBIO** | MUSTANG BIO, INC. | `$0.39` | $2.65M | `$2.12` | `$1.41` | `$0.98` | **NR** | `7.92%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **INHD** | INNO HOLDINGS INC. | `$3.07` | $7.74M | `$13.10` | `$21.38` | `$22.07` | **NR** | `-67.47%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **ABOS** | Acumen Pharmaceuticals, Inc. | `$0.21` | $15.38M | `$0.73` | `$0.47` | `$0.48` | **NR** | `19.40%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **REVB** | REVELATION BIOSCIENCES, INC. | `$3.56` | $2.43M | `$12.17` | `$9.48` | `$10.58` | **NR** | `-88.46%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **JTAI** | Jet.AI Inc. | `$0.88` | $3.13M | `$2.84` | `$2.01` | `$11.21` | **NR** | `9.08%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MSAI** | MultiSensor AI Holdings, Inc | `$2.84` | $6.30M | `$9.15` | `$10.17` | `$12.05` | **NR** | `-95.78%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **LABT** | Lakewood-Amedex Biotherapeut | `$0.60` | $1.42M | `$1.89` | `$1.78` | `$1.83` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **CTNT** | CHEETAH NET SUPPLY CHAIN SER | `$1.60` | $4.28M | `$4.83` | `$32.40` | `$32.67` | **NR** | `66.91%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PHUN** | Phunware, Inc. | `$1.73` | $35.40M | `$4.48` | `$4.30` | `$4.33` | **NR** | `1.37%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **APVO** | Aptevo Therapeutics Inc. | `$1.24` | $2.23M | `$3.10` | `$1.29` | `$3.35` | **NR** | `-45.19%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **SRXH** | SRX Global Inc. | `$0.79` | $16.03M | `$1.89` | `$3.10` | `$3.11` | **NR** | `3,258.64%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PARA** | Parabolic Technologies, Inc. | `$0.16` | $0.26M | `$0.37` | `$-10.62` | `$-10.57` | **NR** | `1,594.79%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **PLRX** | PLIANT THERAPEUTICS, INC. | `$0.82` | $50.57M | `$1.83` | `$1.63` | `$2.04` | **-132.07%** | `0.88%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **FBIO** | Fortress Biotech, Inc. | `$1.84` | $62.09M | `$4.11` | `$3.18` | `$4.74` | **NR** | `1.95%` | `4/9` | `1_NET_CASH_FLOOR` |
| **MRLN** | Merlin, Inc. | `$0.77` | $79.82M | `$1.54` | `$1.21` | `$-0.25` | **NR** | `45.22%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **XLO** | Xilio Therapeutics, Inc. | `$8.50` | $60.04M | `$16.45` | `$8.48` | `$9.66` | **-95.97%** | `-86.54%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **TVRD** | Tvardi Therapeutics, Inc. | `$0.86` | $11.49M | `$1.65` | `$1.13` | `$1.14` | **NR** | `42.45%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **AIFA** | All In FutureTech Alliance,  | `$3.94` | $25.30M | `$7.47` | `$3.27` | `$4.30` | **-39.15%** | `-83.11%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **ALDX** | Aldeyra Therapeutics, Inc. | `$0.61` | $36.73M | `$1.15` | `$0.58` | `$0.58` | **NR** | `0.32%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **BCYC** | BICYCLE THERAPEUTICS PLC | `$3.48` | $243.49M | `$6.52` | `$6.80` | `$7.22` | **-72.71%** | `0.98%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **IVDA** | Iveda Solutions, Inc. | `$0.19` | $2.39M | `$0.35` | `$0.41` | `$0.43` | **NR** | `330.69%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MSN** | EMERSON RADIO CORP | `$0.29` | $6.09M | `$0.53` | `$0.77` | `$0.79` | **-61.11%** | `0.00%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **OPAL** | OPAL Fuels Inc. | `$1.36` | $40.31M | `$2.45` | `$-11.57` | `$-0.54` | **-46.19%** | `4.82%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **PEW** | GrabAGun Digital Holdings In | `$1.87` | $55.34M | `$3.25` | `$2.84` | `$3.38` | **-33.06%** | `-1.41%` | `4/9` | `1_NET_CASH_FLOOR` |
| **QNT** | Quantinuum Inc. | `$29.85` | $1,098.69M | `$51.73` | `$51.99` | `$-8.62` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **AIDX** | 20/20 Biolabs, Inc. | `$0.18` | $2.36M | `$0.31` | `$0.17` | `$0.11` | **NR** | `2.70%` | `5/9` | `1_NET_CASH_FLOOR` |
| **IMA** | ImageneBio, Inc. | `$4.07` | $50.70M | `$6.71` | `$9.33` | `$10.29` | **NR** | `11.40%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MYPS** | PLAYSTUDIOS, Inc. | `$4.66` | $56.13M | `$7.59` | `$6.29` | `$8.07` | **36.12%** | `-4.18%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **EROC** | ERock, Inc. | `$6.67` | $321.08M | `$10.61` | `$2.11` | `NR` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **AUUD** | AUDDIA INC. | `$0.58` | $4.01M | `$0.87` | `$0.81` | `$1.24` | **NR** | `122.92%` | `4/9` | `1_NET_CASH_FLOOR` |
| **KAPA** | Kairos Pharma, LTD. | `$0.46` | $2.14M | `$0.67` | `$0.61` | `$0.81` | **NR** | `-77.50%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **INVE** | INVE Technologies, Inc. | `$2.55` | $60.87M | `$3.60` | `$3.38` | `$5.49` | **NR** | `0.44%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **SCYX** | SCYNEXIS INC | `$3.33` | $33.09M | `$4.56` | `$4.16` | `$5.93` | **NR** | `-76.28%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **VTGN** | Vistagen Therapeutics, Inc. | `$0.17` | $7.67M | `$0.22` | `$0.30` | `$0.32` | **NR** | `16.94%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **GDC** | GD Culture Group Ltd | `$1.12` | $4.66M | `$1.50` | `$8.61` | `$117.21` | **NR** | `-75.22%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **YARW** | Yarrow Bioscience, Inc. | `$13.55` | $206.43M | `$17.97` | `$17.55` | `$17.56` | **NR** | `-8.58%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **KROS** | Keros Therapeutics, Inc. | `$9.46` | $185.65M | `$12.45` | `$13.22` | `$14.22` | **-26.00%** | `-35.59%` | `6/9` | `1_NET_CASH_FLOOR` |
| **RXST** | RxSight, Inc. | `$4.53` | $189.73M | `$5.83` | `$5.47` | `$6.08` | **9.83%** | `1.98%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **RNA** | Atrium Therapeutics, Inc. | `$8.39` | $180.98M | `$10.73` | `$9.23` | `$9.50` | **-34.34%** | `-0.40%` | `NR/9` | `1_NET_CASH_FLOOR` |

## Bucket 2: High-FCF Deep Value Turnarounds (`Bucket_2_High_FCF_Turnaround`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **TTEC** | TTEC Holdings, Inc. | `$1.47` | $72.35M | `$0.42` | `$-13.71` | `NR` | **108.67%** | `1.72%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **PAAI** | Paradium.AI, Inc. | `$0.83` | $39.52M | `$-1.88` | `$-1.79` | `$-1.14` | **99.31%** | `0.31%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **AMS** | AMERICAN SHARED HOSPITAL SER | `$1.19` | $7.91M | `$0.44` | `$-1.32` | `$3.19` | **87.38%** | `2.02%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **MKTW** | MARKETWISE, INC. | `$21.73` | $63.76M | `$7.34` | `$-124.76` | `$-23.43` | **81.72%** | `12.97%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**CRMD**](https://bobmahalo.github.io/Single-Stock-Scan/CRMD.html) | CorMedix Inc. | `$5.22` | $415.58M | `$4.42` | `$0.59` | `$1.05` | **74.08%** | `0.95%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **FLUX** | Flux Power Holdings, Inc. | `$0.31` | $6.81M | `$-0.07` | `$-0.17` | `$-0.05` | **72.91%** | `2.92%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **WETH** | Wetouch Technology Inc. | `$0.77` | $10.30M | `$9.51` | `$10.02` | `$11.12` | **68.63%** | `2.82%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **KODK** | EASTMAN KODAK CO | `$7.42` | $723.94M | `$2.04` | `$-0.18` | `$6.41` | **64.23%** | `20.97%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **EBS** | Emergent BioSolutions Inc. | `$5.83` | $300.01M | `$-6.57` | `$-2.41` | `$1.18` | **62.80%** | `-2.10%` | `7/9` | `2_HIGH_FCF_TURNAROUND` |
| **CMTL** | COMTECH TELECOMMUNICATIONS C | `$1.18` | $35.56M | `$0.74` | `$-6.36` | `$-4.55` | **62.39%** | `1.50%` | `5/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PLTK** | Playtika Holding Corp. | `$2.29` | $874.41M | `$-5.00` | `$-7.61` | `$-6.27` | **55.04%** | `1.76%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **XRX** | Xerox Holdings Corp | `$1.10` | $146.53M | `$-0.54` | `$-40.97` | `$-20.89` | **51.87%** | `4.04%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| [**CRWS**](https://bobmahalo.github.io/Single-Stock-Scan/CRWS.html) | CROWN CRAFTS INC | `$2.55` | $27.72M | `$-1.07` | `$2.45` | `$3.26` | **50.61%** | `1.58%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| [**DXC**](https://bobmahalo.github.io/Single-Stock-Scan/DXC.html) | DXC Technology Co | `$15.19` | $2,360.82M | `$6.21` | `$-25.16` | `$16.27` | **43.63%** | `-10.72%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **PAGP** | PLAINS GP HOLDINGS LP | `$26.41` | $5,230.86M | `$3.34` | `$3.02` | `NR` | **43.42%** | `0.11%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **COLL** | COLLEGIUM PHARMACEUTICAL, IN | `$25.08` | $779.37M | `$4.48` | `$-38.22` | `$-33.21` | **43.15%** | `-1.69%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **SCOR** | COMSCORE, INC. | `$3.29` | $49.88M | `$1.08` | `$-3.99` | `$-6.31` | **39.58%** | `202.79%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| [**DLTH**](https://bobmahalo.github.io/Single-Stock-Scan/DLTH.html) | DULUTH HOLDINGS INC. | `$4.07` | $148.07M | `$-1.68` | `$-0.99` | `$4.88` | **38.86%** | `4.98%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **MYPS** | PLAYSTUDIOS, Inc. | `$4.66` | $56.13M | `$7.59` | `$6.29` | `$8.07` | **36.12%** | `-4.18%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **VSNT** | Versant Media Group, Inc. | `$34.06` | $4,718.60M | `$-12.72` | `$-10.94` | `$-0.65` | **34.76%** | `-3.91%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **DK** | Delek US Holdings, Inc. | `$62.44` | $3,784.44M | `$-34.77` | `$-41.51` | `NR` | **31.75%** | `0.94%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **UFI** | UNIFI INC | `$5.95` | $110.60M | `$1.08` | `$3.31` | `NR` | **31.61%** | `1.24%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PBF** | PBF Energy Inc. | `$68.50` | $8,408.82M | `$-0.95` | `$-8.95` | `$64.81` | **31.22%** | `4.07%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PARR** | PAR PACIFIC HOLDINGS, INC. | `$68.93` | $3,451.80M | `$-2.48` | `$5.56` | `$43.80` | **29.75%** | `-0.43%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **JVA** | COFFEE HOLDING CO INC | `$4.82` | $27.52M | `$0.17` | `$4.29` | `$5.43` | **28.99%** | `0.00%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **VHI** | VALHI INC /DE/ | `$14.54` | $411.93M | `$6.97` | `$30.15` | `$24.45` | **28.79%** | `0.07%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **LCUT** | LIFETIME BRANDS, INC | `$7.76` | $178.47M | `$-4.42` | `$9.99` | `$3.49` | **28.43%** | `1.45%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PMTS** | CPI Card Group Inc. | `$24.62` | $286.39M | `$-21.98` | `$-17.96` | `$-6.75` | **28.40%** | `2.15%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **IPM** | INTELLIGENT PROTECTION MANAG | `$1.67` | $15.09M | `$0.71` | `$-0.11` | `$0.47` | **28.38%** | `-0.55%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **IMMR** | IMMERSION CORP | `$6.63` | $220.16M | `$4.17` | `$5.82` | `$6.92` | **27.77%** | `2.11%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **SSTK** | Shutterstock, Inc. | `$3.04` | $112.71M | `$-0.63` | `$-11.46` | `$-0.68` | **27.17%** | `4.43%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **CRI** | CARTERS INC | `$32.59` | $1,195.63M | `$-19.84` | `$-5.42` | `$15.76` | **26.74%** | `0.67%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **SBGI** | Sinclair, Inc. | `$14.21` | $1,029.69M | `$6.94` | `$-51.70` | `$-23.09` | **25.44%** | `4.02%` | `3/9` | `2_HIGH_FCF_TURNAROUND` |
| **SKYW** | SKYWEST INC | `$79.68` | $3,030.56M | `$-45.52` | `$-64.77` | `$73.88` | **25.19%** | `-5.16%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **DSP** | Viant Technology Inc. | `$12.65` | $268.47M | `$7.64` | `$7.99` | `$3.88` | **25.06%** | `10.66%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **HBB** | Hamilton Beach Brands Holdin | `$32.07` | $431.53M | `$3.90` | `$10.43` | `$15.88` | **24.84%** | `-0.38%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **MBLY** | Mobileye Global Inc. | `$5.12` | $1,292.31M | `$5.09` | `$5.76` | `$9.19` | **24.53%** | `16.85%` | `NR/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **TDC** | TERADATA CORP /DE/ | `$32.90` | $3,007.06M | `$4.65` | `$-2.83` | `$1.95` | **24.38%** | `-1.93%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **AERT** | Aeries Technology, Inc. | `$5.33` | $33.79M | `$-0.52` | `$-2.71` | `$-0.26` | **24.17%** | `7.19%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |
| **QRHC** | Quest Resource Holding Corp | `$1.04` | $22.11M | `$-0.05` | `$-2.55` | `$-2.30` | **23.92%** | `1.87%` | `NR/9` | `2_HIGH_FCF_TURNAROUND` |

## Bucket 3: Cannibal Buybacks (`Bucket_3_Cannibal_Buybacks`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **IIIV** | i3 Verticals, Inc. | `$19.37` | $378.56M | `$-5.95` | `$-8.35` | `$-7.95` | **13.19%** | `-42.41%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **AMCX** | AMC Global Media Inc. | `$8.43` | $352.77M | `$-31.01` | `$-35.26` | `$12.86` | **27.24%** | `-25.64%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **BTMD** | biote Corp. | `$1.03` | $28.38M | `$-4.23` | `$-4.29` | `$-2.72` | **26.11%** | `-25.32%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **EIG** | Employers Holdings, Inc. | `$47.29` | $829.35M | `NR` | `NR` | `$41.96` | **5.38%** | `-21.98%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **IBTA** | Ibotta, Inc. | `$57.92` | $1,352.38M | `$5.34` | `$5.21` | `$10.21` | **6.02%** | `-20.52%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **FBLA** | FB Bancorp, Inc. /MD/ | `$16.79` | $264.76M | `NR` | `NR` | `$17.26` | **15.53%** | `-20.51%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **FOUR** | Shift4 Payments, Inc. | `$43.05` | $3,226.71M | `$-48.68` | `$-67.53` | `$-17.16` | **19.34%** | `-20.08%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **PAYC** | Paycom Software, Inc. | `$249.91` | $11,254.64M | `$-13.98` | `$-21.99` | `$13.95` | **5.86%** | `-19.97%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **YEXT** | Yext, Inc. | `$7.64` | $756.15M | `$-1.36` | `$-2.52` | `$-0.76` | **7.01%** | `-19.68%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **PRKS** | United Parks & Resorts Inc. | `$37.73` | $1,714.12M | `$-51.76` | `$-64.88` | `$-13.19` | **8.76%** | `-16.71%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **ZD** | ZIFF DAVIS, INC. | `$54.36` | $1,799.44M | `$20.04` | `$8.40` | `$18.25` | **6.03%** | `-16.21%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **PINS** | PINTEREST, INC. | `$19.75` | $11,507.38M | `$-1.00` | `$1.18` | `$4.37` | **10.97%** | `-16.11%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| [**NRDS**](https://bobmahalo.github.io/Single-Stock-Scan/NRDS.html) | NERDWALLET, INC. | `$11.54` | $746.64M | `$1.03` | `$2.01` | `$3.11` | **19.55%** | `-15.86%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **PD** | PagerDuty, Inc. | `$16.20` | $1,274.13M | `$-2.28` | `$-1.68` | `$1.03` | **9.94%** | `-15.65%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **BFAM** | BRIGHT HORIZONS FAMILY SOLUT | `$55.42` | $2,656.34M | `$-35.42` | `$-50.00` | `$-22.54` | **9.54%** | `-15.25%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **DBX** | DROPBOX, INC. | `$35.78` | $8,055.20M | `$0.16` | `$-16.59` | `$-11.89` | **11.36%** | `-15.09%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **PGNY** | Progyny, Inc. | `$34.58` | $2,546.72M | `$1.24` | `$2.75` | `$5.35` | **7.05%** | `-14.57%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| [**HOG**](https://bobmahalo.github.io/Single-Stock-Scan/HOG.html) | HARLEY-DAVIDSON, INC. | `$32.60` | $3,292.35M | `$6.64` | `$8.98` | `$29.39` | **9.47%** | `-14.52%` | `8/9` | `1_NET_CASH_FLOOR | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **CHTR** | CHARTER COMMUNICATIONS, INC. | `$125.69` | $14,699.33M | `$-905.82` | `$-987.46` | `$-160.46` | **26.73%** | `-14.26%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **BILL** | BILL Holdings, Inc. | `$50.87` | $4,368.44M | `$-6.14` | `$6.49` | `$8.80` | **9.47%** | `-14.25%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CRM** | Salesforce, Inc. | `$222.80` | $183,364.40M | `$-40.62` | `$-59.73` | `$-32.82` | **8.26%** | `-13.55%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **MIDD** | MIDDLEBY Corp | `$130.49` | $5,683.56M | `$-39.36` | `$-26.32` | `$-18.52` | **6.55%** | `-13.53%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CPRI** | Capri Holdings Ltd | `$21.18` | $2,189.46M | `$-13.17` | `$-19.09` | `$-6.61` | **8.40%** | `-13.26%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **SMPL** | Simply Good Foods Co | `$12.61` | $1,094.90M | `$-2.50` | `$-1.74` | `$-0.61` | **14.33%** | `-13.01%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **CARS** | Cars.com Inc. | `$13.46` | $700.94M | `$-7.58` | `$-6.77` | `$-4.06` | **21.48%** | `-12.94%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **ETSY** | ETSY INC | `$91.19` | $7,861.11M | `$23.50` | `$-14.41` | `$-8.30` | **7.54%** | `-12.66%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **FCNCA** | FIRST CITIZENS BANCSHARES IN | `$2,301.89` | $25,897.46M | `NR` | `NR` | `$1,849.69` | **9.53%** | `-12.44%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **TENB** | Tenable Holdings, Inc. | `$44.24` | $4,623.94M | `$-3.31` | `$-9.45` | `$-7.84` | **6.06%** | `-12.43%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **AN** | AUTONATION, INC. | `$187.38` | $5,993.08M | `$-12.80` | `$-44.16` | `$-12.65` | **0.38%** | `-12.31%` | `5/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **AMG** | AFFILIATED MANAGERS GROUP, I | `$351.06` | $8,667.28M | `NR` | `NR` | `$-51.71` | **13.26%** | `-12.23%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **ZG** | ZILLOW GROUP, INC. | `$31.16` | $7,020.50M | `$2.28` | `$3.01` | `$5.11` | **4.46%** | `-12.07%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **WRLD** | WORLD ACCEPTANCE CORP | `$148.47` | $658.59M | `NR` | `NR` | `$76.37` | **42.28%** | `-11.95%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **CROX** | Crocs, Inc. | `$153.22` | $7,005.99M | `$-32.80` | `$-41.73` | `$-8.13` | **10.76%** | `-11.92%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **FCN** | FTI CONSULTING, INC | `$196.37` | $5,351.90M | `$-36.68` | `$-21.74` | `$2.62` | **6.61%** | `-11.73%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **FUSB** | FIRST US BANCSHARES, INC. | `$16.43` | $83.75M | `NR` | `NR` | `NR` | **10.57%** | `-11.61%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **YELP** | YELP INC | `$20.68` | $1,126.91M | `$1.80` | `$-0.31` | `$4.26` | **23.34%** | `-11.38%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **HGV** | Hilton Grand Vacations Inc. | `$43.79` | $3,320.28M | `NR` | `NR` | `$-8.97` | **14.25%** | `-11.36%` | `NR/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| [**PYPL**](https://bobmahalo.github.io/Single-Stock-Scan/PYPL.html) | PayPal Holdings, Inc. | `$58.91` | $48,938.23M | `$-4.77` | `$-1.91` | `$10.25` | **12.87%** | `-11.22%` | `8/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **MTG** | MGIC INVESTMENT CORP | `$29.30` | $5,828.22M | `NR` | `NR` | `$24.36` | **12.14%** | `-11.08%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |
| **UTMD** | UTAH MEDICAL PRODUCTS INC | `$71.10` | $202.60M | `$29.80` | `$33.48` | `$37.00` | **5.36%** | `-11.05%` | `NR/9` | `3_CANNIBAL_BUYBACKS` |

## Bucket 4: Cluster & C-Suite Insider Buying (`Bucket_4_Cluster_Insider_Buy`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **PBLS** | Parabilis Medicines, Inc. | `$27.94` | $3,453.19M | `$3.89` | `$6.09` | `$8.13` | **NR** | `6,021.17%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **MAIR** | Madison Air Solutions Corp | `$21.40` | $11,345.99M | `$4.73` | `$-1.88` | `$-0.85` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BRVE** | Braveheart Bio, Inc. | `$17.42` | $1,565.54M | `$1.34` | `$3.81` | `$5.54` | **NR** | `1,765.60%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SMMT** | Summit Therapeutics Inc. | `$14.39` | $11,512.60M | `$0.76` | `$0.67` | `$0.70` | **-4.58%** | `7.43%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ROL** | ROLLINS INC | `$38.79` | $18,543.38M | `$-0.56` | `$-2.84` | `$-1.39` | **3.62%** | `-1.36%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| [**GME**](https://bobmahalo.github.io/Single-Stock-Scan/GME.html) | GameStop Corp. | `$24.05` | $12,130.73M | `$9.29` | `$1.83` | `$12.17` | **5.67%** | `12.70%` | `7/9` | `4_CLUSTER_INSIDER_BUY` |
| **KARD** | Kardigan, Inc. | `$13.94` | $1,304.75M | `$0.71` | `$4.36` | `$5.83` | **NR** | `643.69%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ADRX** | ADARx Pharmaceuticals, Inc. | `$13.18` | $1,465.53M | `$8.04` | `$5.07` | `$5.17` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **DPC** | DPC Holdings PLC | `$27.22` | $4,066.48M | `$1.37` | `$1.93` | `$4.42` | **NR** | `32.56%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SCTX** | Scribe Therapeutics, Inc. | `$15.52` | $293.82M | `$8.81` | `$6.13` | `$6.61` | **NR** | `496.86%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **LFTO** | Liftoff Mobile, Inc. | `$17.20` | $2,914.44M | `$-5.92` | `$-7.45` | `$-6.47` | **NR** | `25.65%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **LILA** | Liberty Latin America Ltd. | `$8.93` | $1,738.67M | `$-0.25` | `$-46.82` | `$-13.43` | **NR** | `-6.26%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ATTO** | Attovia Therapeutics, Inc. | `$14.98` | $685.00M | `$2.44` | `$8.54` | `$8.70` | **NR** | `654.04%` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **LYEL** | Lyell Immunopharma, Inc. | `$14.68` | $360.92M | `$1.94` | `$4.27` | `$7.84` | **-38.78%** | `15.87%` | `2/9` | `4_CLUSTER_INSIDER_BUY` |
| **ETRA** | Electra Therapeutics, Inc. | `$7.16` | $450.13M | `$4.05` | `$6.19` | `$6.25` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **AVO** | Mission Produce, Inc. | `$11.59` | $1,016.19M | `$-4.88` | `$-4.62` | `$5.65` | **-0.23%** | `24.16%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **AVR** | Anteris Technologies Global  | `$5.57` | $542.55M | `$2.06` | `$2.07` | `$2.33` | **-17.23%** | `136.65%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| [**LRN**](https://bobmahalo.github.io/Single-Stock-Scan/LRN.html) | Stride, Inc. | `$75.32` | $3,167.12M | `$2.84` | `$21.29` | `$33.67` | **15.93%** | `-4.13%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **FUN** | Six Flags Entertainment Corp | `$9.07` | $928.46M | `$-47.59` | `$-53.15` | `$-22.78` | **NR** | `0.82%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **QTTB** | Q32 Bio Inc. | `$8.86` | $265.13M | `$9.51` | `$9.41` | `$9.61` | **-12.65%** | `143.20%` | `3/9` | `4_CLUSTER_INSIDER_BUY` |
| **PNAQ** | Pinnacle Acquisition Corp | `$9.78` | NR | `NR` | `NR` | `NR` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SUJA** | SUJA LIFE, INC. | `$10.21` | $242.76M | `NR` | `NR` | `NR` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **MSM** | MSC INDUSTRIAL DIRECT CO INC | `$110.56` | $6,175.69M | `$-2.61` | `$4.23` | `$11.31` | **3.65%** | `0.12%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BLSM** | BlossomHill Therapeutics, In | `$12.12` | $385.23M | `$7.08` | `NR` | `$6.64` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **QNT** | Quantinuum Inc. | `$29.85` | $1,098.69M | `$51.73` | `$51.99` | `$-8.62` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **RAPP** | Rapport Therapeutics, Inc. | `$23.78` | $1,409.67M | `$6.51` | `$6.41` | `$6.60` | **-8.60%** | `24.38%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **NTSK** | Netskope Inc | `$21.73` | $8,799.62M | `$0.46` | `$-0.42` | `$0.19` | **-0.80%** | `274.71%` | `6/9` | `4_CLUSTER_INSIDER_BUY` |
| **ET** | Energy Transfer LP | `NR` | NR | `$-20.26` | `$-19.03` | `NR` | **NR** | `0.32%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **GSHD** | Goosehead Insurance, Inc. | `$56.69` | $2,024.40M | `$-9.69` | `$-14.28` | `$-4.50` | **3.94%** | `-7.37%` | `5/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **BGDE** | Big Digital Energy, Inc. | `$2.58` | $16.56M | `$0.16` | `$-4.12` | `$1.31` | **NR** | `-71.93%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| **STWD** | STARWOOD PROPERTY TRUST, INC | `$12.89` | $4,693.84M | `NR` | `NR` | `$14.12` | **NR** | `-1.71%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **CV** | CapsoVision, Inc | `$6.25` | $334.79M | `NR` | `NR` | `$0.49` | **-8.74%** | `14.44%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **UBER** | Uber Technologies, Inc | `$68.80` | $140,482.59M | `$-4.01` | `$-11.87` | `$7.69` | **7.42%** | `-1.73%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| **FBIN** | Fortune Brands Innovations,  | `$47.02` | $5,570.73M | `$-19.94` | `$-15.91` | `NR` | **9.96%** | `-1.38%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **AMR** | Alpha Metallurgical Resource | `$142.96` | $1,810.17M | `$25.97` | `$7.16` | `$114.49` | **NR** | `-1.52%` | `4/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **PMTS** | CPI Card Group Inc. | `$24.62` | $286.39M | `$-21.98` | `$-17.96` | `$-6.75` | **28.40%** | `2.15%` | `NR/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **TUSK** | MAMMOTH ENERGY SERVICES, INC | `$2.95` | $141.98M | `$0.19` | `$0.62` | `$5.43` | **-100.62%** | `-0.14%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **GLXY** | Galaxy Digital Inc. | `$12.97` | $3,317.05M | `$17.51` | `$-8.09` | `$7.08` | **NR** | `15.46%` | `2/9` | `4_CLUSTER_INSIDER_BUY` |
| **ACDC** | ProFrac Holding Corp. | `$2.67` | $486.27M | `$-5.48` | `$-6.42` | `$0.71` | **-3.27%** | `0.69%` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **CDNL** | Cardinal Infrastructure Grou | `$12.55` | $258.60M | `NR` | `NR` | `$1.53` | **-4.55%** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |

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
| **Optional Strategy Sieves (`Cols 61–68`)** | `Is_Dilution_Vampire` (`647` flagged), `Bucket_1_Net_Cash_Floor` (`378`), `Bucket_2_High_FCF_Turnaround` (`130`), `Bucket_3_Cannibal_Buybacks` (`380`), `Bucket_4_Cluster_Insider_Buy` (`400`), `Buckets_Count` | Optional deep-value hunting buckets feeding our `11`-stock Stage 1 Convergence Shortlist. |

### 3. Core Mathematical & Forensic Formulas

| Metric | Exact Mathematical Formula | Institutional Interpretation |
| :--- | :--- | :--- |
| **Net Cash (Ex-Debt) / Share** | $$\frac{\text{Cash \& ST Investments} - \text{Total Debt}}{N_{\text{diluted}}}$$ | Hard net cash cushion per share after extinguishing 100% of funded debt. |
| **Graham NCAV / Share** | $$\frac{\text{Current Assets} - \text{Total Liabilities} - \text{Preferred Stock}}{N_{\text{diluted}}}$$ | Benjamin Graham Net-Net liquidation floor (strict arbitrage requires $P \le 0.67 \times \text{NCAV}$). |
| **Tangible Book Value (TBV) / Share** | $$\frac{\text{Stockholders' Equity} - \text{Goodwill} - \text{Intangibles}}{N_{\text{diluted}}}$$ | Physical net worth per share stripping out M&A accounting goodwill. |
| **Altman Z-Score (5-Factor)** | $$Z = 1.2 X_1 + 1.4 X_2 + 3.3 X_3 + 0.6 X_4 + 0.999 X_5$$ | Solvency index across Operating Universe (`> 2.99` Safe, `1.81–2.99` Grey, `< 1.81` Distress). |
| **Step A Dilution Quarantine** | `Share_Count_1Y_Change_Pct > 10%` or (`FCF < 0` & `Stock_Issued > 5% MCap`) | Quarantines `{vampires:,}` chronic equity diluters (`Is_Dilution_Vampire = True`). |

</details>
